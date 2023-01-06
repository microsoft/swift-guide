# Concurrency

In general, follow the concurrency section in the [official guidelines](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html).

## Convention

Use a task to manage synchronous access to a property populated by an an asynchronous function within an Actor. For more in-depth discussions, watch [WWDC21 - Protect mutable state with Swift actors](https://developer.apple.com/wwdc21/10133).

## Rationale
Even though Actors are helpful for sharing information between concurrent code, asynchronous functions in Actors does not guarantee the state of Actor properties after an asynchronous call.

## Examples

### Bad: when calling the function retrieveURL() across different threads, it's possible that multiple downloads are executed which is inefficient and unnecessary. If the download function always downloads to the same directory, the returned URL might point to an invalid file because another thread has overwritten the url with partially downloaded contents.

``` swift
actor BuildToolExecutable {

	func retrieveURL() async throws -> URL {
		if cachedURL == nil {
			// When the following line executes, the function does not continue executing until
			// the download finishes. During this time, a different thread could call the function
			// and download the same executable again.
			let url = try await downloadExecutable()
			cachedURL = url
		}

		return cachedURL
	}

	private var cachedURL: URL? = nil
}

```

### Good: Initialize the cache with a task that downloads the executable asynchronously. Subsequent requests of URL() function will wait for the asynchronous task to finish if queued before the cache is populated or use the cached value after the task finishes.

``` swift
actor BuildToolExecutable {

	/// Checks the cache for the url of the executable
	/// - Returns: the cached url if available, or wait for the url retrieval task to finish and return the result of the task
	func URL() async throws -> URL {
		switch cache {
		case let .ready(url):
			return url
		case let .inProgress(urlRetrievalTask):
			let url = try await urlRetrievalTask.value
			cache = .ready(url)
			return url
		}
	}
	
}

	private func retrieveURL() async throws -> URL {
		return = try await downloadExecutable()
	}

	private var cache: CacheEntry = .inProgress(Task { try await retrieveURL() })

	private enum CacheEntry {
		case inProgress(Task<URL, Error>)
		case ready(URL)
	}
}


```

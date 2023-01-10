# Concurrency

In general, follow the concurrency section in the [official guidelines](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html).

## Convention

Use a task to manage synchronous access to a property populated by an asynchronous function within an Actor. For more in-depth discussions of the provided example, watch [WWDC21 - Protect mutable state with Swift actors](https://developer.apple.com/wwdc21/10133).

## Rationale
Even though Actors are helpful for sharing information between concurrent code, asynchronous functions in Actors do not guarantee the state of Actor properties after an asynchronous call.

## Examples

### Bad: when calling the function image(from:url:) across different threads, it's possible that multiple downloads are executed which is inefficient and unnecessary. If the download function always downloads to the same file path, the file path might contain partially downloaded contents.

``` swift
actor ImageDownloader {

	func image(from url: URL) async throws -> UIImage {
		if let cached = cache[url] {
			return cached
		}

		// When the following line executes, the function does not continue executing until
		// the download finishes. During this time, a different thread could call the function
		// and download the same image again.
		let imageFilePath = try await downloadImage(from: url)

		// The image file might not contain the full downloaded contents.
		let image = UIImage(contentsOfFile: imageFilePath)

		cache[url] = image
		return image!
	}

	private var cache: [URL: UIImage] = [:]
}

```

### Good: Use a task that downloads the executable asynchronously. Subsequent requests of the same image will wait for the asynchronous task to finish if queued before the cache is populated or use the cached value after the task finishes.

``` swift
actor ImageDownloader {

	/// Checks the cache for the image corresponding to the url
	/// - Returns: the cached image if available, or wait for the task to finish and return the result of the task
	func image(from url: URL) async throws -> UIImage {
		if let cached = cache[url] {
				switch cached {
				case .ready(let image):
					 return image
				case .inProgress(let task):
					 return try await task.value
				}
		  }

		  let task = Task {
				let imageFilePath = try await downloadImage(from: url)
				return UIImage(contentsOfFile: imageFilePath)!
		  }

		  cache[url] = .inProgress(task)

		  do {
				let image = try await task.value
				cache[url] = .ready(image)
				return image
		  } catch {
				cache[url] = nil
				throw error
		  }
	
}

	private var cache: [URL: CacheEntry] = [:]

	private enum CacheEntry {
		case inProgress(Task<UIImage, Error>)
		case ready(UIImage)
	}
}

```

# Contributing to the Swift Coding Guidelines

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## How to contribute

### Proposing new guidelines

These guidelines are not exhaustive. If you have a proposal for a new convention to be added to the guidelines, please create an issue in this repository to track it. Be sure to add "Convention:", "Rationale:", and "Example:" sections in the template and provide a short succinct title with the recommended page title. The title shouldn't contain the convention itself, but should explain the area of code the convention refers to. For example, a title might say `Immutability` instead of `Use constants over variables whenever possible`.

### Improve existing guidelines

There are several areas through which existing rules can be improved.
* Spelling, grammatical, and tonal errors
* Improving wording for conciseness or clarity
* Better or more realistic example code

For issues of these types, please submit a pull request with the proposed improvement and the guideline maintainers will review the changes.

### Contributing new guidelines
Pick a new unimplemented task from issues in this repository and write the conventions in a new markdown file. Follow the recommended [format and tone](#format-and-tone) for the document and don't forget to [update the table of contents as well](#updating-table-of-contents). Submit a pull request with the new proposed conventions and the guideline maintainers will review the proposal.


## Format and tone

Follow the format and tone of existing guidelines in the repository. The tone of the writing should be impersonal, third person, and succinct. Each page should include a title, an optional general introduction of the page, and the three following sections.

### Convention

Conventions should be direct and easy to follow. It is acceptable for conventions to allow for exceptions. Do not explain the reasoning for conventions in this section, simply state the convention that code should follow. This section may contain multiple conventions for a given area of code.

### Rationale

Rationale should describe why the convention is preferable to the alternative. Links to external sites are allowed and encouraged so long as the sites are trustworthy and the URLs are unlikely to change or go away. Official Swift Language guide is generally preferred. If possible use real world examples where following the convention would have prevented issues.

### Examples

Examples should be written in valid Swift snippets and not written in pseudo-code. If good and bad examples are easily mixed, use a single block of code and annotate the good examples with `// bad: explanation of the convention this fails to follow` or `// good: optional explanation of the convention this follows`. Prefer to have bad examples come before good examples and prefer to have individual examples of bad and good paired for easy comparison. For more contextual conventions that require more complex code snippets, break up the examples section into two blocks of code, one titled `Bad` followed by one titled `Good`.

## Updating table of contents

There should be no links to empty pages from either the [README.md](README.md) file or the category table of content pages. Empty pages may exist in the repository as long as no active page links to it. When adding a new convention, the contributor is responsible for adding links in the category table of contents as well as to [README.md](README.md).


## Test changes in GitHub Pages locally with Jekyll

### Prerequisites
Local testing with Jekyll requires `Ruby 2.5+` and `Bundler`; please refer to [Testing Your Github Pages site locally with Jekyll](https://help.github.com/en/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll) for more details on the installation.

### Test steps

* cd into the repository

    `$ cd /path/to/swift-guide`

* Install the required `gems`

    `$ bundle install`

* Run the server

    `$ bundle exec jekyll serve`

* Open a browser of your choice and visit the locally served website at `http://localhost:4000`

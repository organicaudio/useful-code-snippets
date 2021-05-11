[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/organicaudio/technotes)

# USEFUL CODE SNIPPETS [WIP]

### Public Page:
[http://organicaudio.github.io/useful-code-snippets/](http://organicaudio.github.io/useful-code-snippets/)


## TO DO:
1) Once complete merge the follow repos into this one and apply structure

[https://github.com/organicaudio/iOS-Shortcuts-Reference](https://github.com/organicaudio/iOS-Shortcuts-Reference)
[https://github.com/organicaudio/code-snippets-macos](https://github.com/organicaudio/code-snippets-macos)
[https://github.com/organicaudio/shortcuts-ios-repo](https://github.com/organicaudio/shortcuts-ios-repo)


2) Complete the Markdown formatting of this doc and prune the contents where appropriate to remove deprecated paths or repetative methods
[https://github.com/organicaudio/useful-code-snippets/blob/master/docs/ios/Reference:%20iOS%20App%20URL%20Scheme%20Names%20%26%20Paths%20for%20Shortcuts.md](https://github.com/organicaudio/useful-code-snippets/blob/master/docs/ios/Reference:%20iOS%20App%20URL%20Scheme%20Names%20%26%20Paths%20for%20Shortcuts.md)


### Site theme / backend
[https://github.com/organicaudio/useful-code-snippets](https://github.com/organicaudio/useful-code-snippets) (this one)
[https://github.com/organicaudio/devtools-snippets](https://github.com/organicaudio/devtools-snippets)


--------------------------------------------------------------------------------------------------------------------------------------------

## Based on MkDocs & Material Theme

Builds every time you push a change to the master branch. 

Uses the Github Action [Deploy MkDocs](https://github.com/marketplace/actions/deploy-mkdocs) to build the page and put the build artifacts to [gh-pages](https://github.com/CrowdSalat/technotes/tree/gh-pages) branch. Afterwards [github pages](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages) is used to host the page under: [**http://crowdsalat.github.io/technotes**](http://crowdsalat.github.io/technotes).

## Install

``sudo pip3 install mkdocs``

``sudo pip3 install mkdocs-material``

sudo might be necessary to add mkdocs on the path. If you want to change color or the navigation refer to [mkdocs martial setup guide](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.
* `mkdocs gh-deploy --clean` - Builds the site and push the generated artefacts to gh-pages branch of the repo

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


# progress-keeper

[![Build Status](https://travis-ci.org/atufkas/progress-keeper.svg?branch=master)](https://travis-ci.org/atufkas/progress-keeper)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)

Track, transform and present changelog entries.

+++ **Note**: Project is currently in the state of an early stage
concept under active development.  API may change frequently. Feel free
to ask, comment and contribute, I'd be happy to receive help and support! +++


## Introduction

This project aims to address the problem of generating user as well as
developer friendly changelog catalogues supporting various formats,
generated from various sources. One major goal is to **aggregate and
present structured change log information based on relevance for a
specific audience**. The implementation and specification of formats
follows some best practices, recommendations and proposals like the
[Conventional Commits Specification](https://conventionalcommits.org/).


## Concepts + API

The project is under active development. New features, concepts and
breaking changes are introduced frequently. Currently this library provides:

- a definition for an "intermediate JSON changelog format" looking like this:
    ``` json
    {
      "name": "PK Sample-App",
      "desc": "The app with forms that make you happy!",
      "releases": [
        {
          "version": "1.0",
          "date": "2018-01-30 12:12",
          "remarks": "Now our app is ready for production.",
          "changelog": [
            {
              "date": "2018-01-26",
              "type": "feat",
              "desc": "Added a batch mode for editing multiple records at once.",
              "audience": "*"
            },
            {
              "date": "2018-01-17",
              "type": "fix(ui)",
              "desc": "Validation failed when whitespace was transmitted via form value.",
              "audience": "*"
            }
          ]
        },
        {
          "version": "0.2.0",
          "date": "2018-01-24 17:30",
          "remarks": "This version introduces this release log, updates internal dependencies and adds support for docker.",
          "changelog": [
            {
              "date": "2018-01-23",
              "type": "code",
              "desc": "Set platform dependency to PHP >= 5.6.0.",
              "audience": "dev"
            }
          ]
        }
      ]
    }
    ```


- a **changelog model** that reflects a structure of the form: Changelog
-> Releases -> Log Entries
    - `atufkas\ProgressKeeper\Changelog`
    - `atufkas\ProgressKeeper\Release\Release`
    - `atufkas\ProgressKeeper\LogEntry\LogEntry`

- a **source format reader interface** with implementations for:
    - JSON: `atufkas\ProgressKeeper\Reader\JsonReader`
    - Markdown: `atufkas\ProgressKeeper\Reader\MarkdownReader`

- a **target format presenter interface** with implementations for:
     - HTML: `atufkas\ProgressKeeper\Presenter\HtmlPresenter`
     - Markdown: `atufkas\ProgressKeeper\Presenter\MarkdownPresenter`

- **simple factory methods** allowing for generating a changelog from a given source file and source format
    - as internal Changelog PHP object: `atufkas\ProgressKeeperKeeperFactory::getChangelog`
    - in target presentation format (by passing target format as additional argument): `atufkas\ProgressKeeperKeeperFactory::getConvertedChangelog`

- a **very basic CLI command** `./bin/progress-keeper` passing command line arguments to
    - `atufkas\ProgressKeeperKeeperFactory::getConvertedChangelog`


## Installation

This is a PHP 5.6+ composer based project. A composer.phar archive bundle is included.

Clone project

    $ git clone https://github.com/atufkas/progress-keeper
    $ cd progress-keeper
    
Install dependencies
    
    $ php ./composer.phar install


## Testing

Run tests by calling composer defined script
    
    $ php ./composer.phar test

...or just directly run PHPUnit

    $ ./vendor/bin/phpunit


## Contributing

No big deal, go ahead! Just follow current (PHP) coding standards and of course
write tests. Feel free to improve or critzize existing code or ideas, ask if
unsure about something or just generate an issue or pull request.
I'll to my best to review them as soon as possible.

When adding a feature or making a change, use progress-keeper to generate
own changelogs by adding a log entry to `./pk-changelog.json` and generate
new Markdows and HTML versions of the whole changelog by running:

    $ php ./composer.phar pre-commit

    
## Related to + heavily inspired by

* [keep a changelog](https://github.com/olivierlacan/keep-a-changelog) - If you build software, keep a changelog.
* [Conventional Commits Specification](https://conventionalcommits.org/)
* [Angular: "Commit Message Guidelines"](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#commit)
* [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog) - Generate a changelog from git metadata
* [commitizen](https://github.com/commitizen/cz-cli) - Simple commit conventions for internet citizens
* [commitlint](https://github.com/marionebl/commitlint) - Lint commit messages

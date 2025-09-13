# Aerium Improvement Proposals (AIPs)

![AIP](./assets/readme/aip.png)

AIPs, or Aerium Improvement Proposals, define standards and guidelines to
improve the Aerium project.
AIPs are designed to be a transparent and collaborative way to propose and
discuss changes to the Aerium network.
The [AIP-1](https://aip.aerium.dev/AIPs/aip-1) defines the proposal workflows.

The [status page](https://aip.aerium.dev) tracks and lists all AIPs in this repository.

## Running Locally

To get started, install [Jekyll](https://jekyllrb.com/docs/installation/), first.
Additionally, make sure to install [Yarn](https://yarnpkg.com/)
for efficient dependency management, including [Bootstrap](https://getbootstrap.com/).

Now, clone this repository and run it locally using the following commands:

```zsh
git clone git@github.com:aerium-network/aip.git
cd aip
yarn install ## To install bootstrap
bundle install
bundle exec jekyll serve
```

## Markdown

Markdown is a lightweight markup language that uses plain text formatting syntax to convert text into HTML,
making it easy to read and write for web content.

### Linting

Markdown linting helps ensure consistent style and formatting, detects syntax errors, improves readability,
and maintains best practices in Markdown documents.

To lint Markdown files, you can use the `mdl` ([MarkdownLint](https://github.com/DavidAnson/markdownlint)) command-line tool.
This tool checks your Markdown files against a set of rules and provides feedback on any issues found.

To install `mdl`, first you need to install [Ruby](https://www.ruby-lang.org/en/documentation/installation/).
Once you ensure Ruby installed on your system, you can install `mdl` by running:

```sh
gem install mdl
```

Then you can lint your Markdown files with the following command:

```sh
mdl --style=config/.mdlrc.rb ./AIPs
```

This command will check all documents in the `AIPs` folder for any linting issues and output them in the terminal.

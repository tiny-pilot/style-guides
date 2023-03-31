# style-guides

This page defines TinyPilot's coding conventions for various programming languages.

## General

TinyPilot's style guides mostly inherit from other established style guides and make changes where we've felt the parent guide lacks specificity or makes a choice that's poorly suited for TinyPilot's work.

## Pull requests

Pull requests (PRs)

Focus on the why rather than the how.

Should introduce the reader to

If there were implementation decisions, include them.

### Titles

* Aim for fewer than 80 characters
  * This is a soft limit, but it's better to be succinct
  * In some views (including on Github), exceeding 80 characters screws up the PR link
* Use imperative mood ("Refactor input handling") rather than descriptive ("Refactors input handling")
* Use sentence casing.
* Omit trailing punctuation.
* Omit prefixes like "(chore)" or "(fix)".

### Descriptions

Pull request descriptions

The PR description can introduce the reader . The PR description is a description of the *change* rather than the code. If there's context the reader needs to understand the code, the code itself should provide that context. After the code is merged, it should make sense to people who haven't read the pull request description.

Can omit when trivial.

Include "Fixes XX"

The reader should understand everything in the PR description. If we're linking to external resources, quote the relevant parts (the external links could disappear). If we're linking to a bug, don't force the reader to read the full bug. Summarize what they need to know. Link to specific headers in external docs.

Revise PR descriptions to match implementation.

## Python

- Base Guide: [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)

## HTML/CSS

- Base Guide: [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)

## Shell

- Base Guide: [Google Shell](https://google.github.io/styleguide/shellguide.html)

### Shellcheck

All repositories with shell scripts should enable shellcheck to run automatically in CI. See [the `check_bash` job](https://github.com/tiny-pilot/tinypilot/blob/master/.circleci/config.yml) in `tiny-pilot/tinypilot` for an example.

### Options

All bash scripts should default to these options unless there's a strong need to exclude any of them.

```bash
# Exit on first failure.
set -e

# Echo commands to stdout.
set -x

# Exit on unset variable.
set -u
```

### Comments

Comments begin with a capital letter and end with trailing punctuation.

```bash
# Our contract with FooVendor requires us to wait five seconds before each
# request.
TIMEOUT_SECONDS=5
```

### Variable names

Variable names should be all uppercase.

```bash
WELCOME_MESSAGE="Hello, world!"
```

```bash
for URL in "${URLS[@]}"; do
  wget "${URL}"
done
```

### Error messages

* Print error messages to stderr.
* Error messages don't have any prefixes like "ERROR:" or "WARNING:".
* Use sentence casing to capitalize error messages.
* Omit trailing punctuation on error messages.

```bash
echo 'Mount mode must be either FLASH or CDROM' >&2
```

## JavaScript

TinyPilot doesn't have well-defined conventions for JavaScript. We are "loosely inspired" by [Google's JavaScript style guide](https://google.github.io/styleguide/jsguide.html), but don't observe it strictly.

The convention is to try to be consistent with existing code in the TinyPilot repos.

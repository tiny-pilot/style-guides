# style-guides

This page defines TinyPilot's conventions for various programming languages.

TinyPilot team members and contributors should follow these conventions when contributing to any TinyPilot-owned repository.

## General

TinyPilot's style guides mostly inherit from other established style guides and make changes where we've felt the parent guide lacks specificity or makes a choice that's poorly suited for TinyPilot's work.

## Github pull requests

### Pull request titles

The pull request (PR) title should summarize the change to make it easy for other developers to quickly scan through the change history for the repo or a file/folder.

* Aim for fewer than 80 characters.
  * This is a soft limit, but it's better to be succinct.
  * In some views (including on Github), exceeding 80 characters screws up the PR link.
* Use imperative mood ("**Refactor** input handling") rather than descriptive ("**Refactors** input handling").
* Use sentence casing ("Refactor input handling") rather than title casing ("Refactor Input Handling").
* Omit trailing punctuation.
* Omit prefixes like "(chore)" or "(fix)".
* Omit Markdown formatting characters such as backticks.
  * Github renders Markdown in PR titles, but not all git clients do.
  * Use Markdown in PR descriptions because it has better cost:benefit ratio there. In the description, Markdown allows links and embedded media, whereas the most we'd want in the title is backticked titles, which isn't so useful when rendered and adds clutter for git clients that don't render Markdown.

### Pull request descriptions

The PR description should introduce the reader to the change and provide them with the context they need to review it.

Write the pull request description so that it makes sense to anyone on the team, even if you have a particular reviewer in mind. Other people might want to read the PR that don't have the reviewer's context, and you yourself will eventually forget the extra context you had when you wrote the code.

#### What to include

The PR description should give a reviewer everything they need to review the PR effectively.

The reviewer should be able to review the PR without clicking external links in the PR description. The description should quote and summarize relevant details from external resources and link to them so that the reviewer can explore further if they choose. If you're linking to a bug, summarize the relevant details of the bug. If you're linking to external documentation, quote the relevant section and link back to the original (linking to the specific header if possible).

If you're changing the UI, considering including a screenshot or short video demo. Visuals should supplement a clear written description of the changes rather than substituting it.

If you considered other implementation options, explain why you chose a particular implementation over other possible candidates.

For trivial PRs, the description is optional, but it's usually helpful to include a description.

#### Focus on the "why" rather than the "how"

The PR description should focus on the *change* rather than the code. It should answer the question, "Why are we making this change right now?"

If there's context the reader needs to understand the code, the code itself should provide that context either through naming, structure, or code comments. After the code is merged, the code needs to make sense to people who haven't read the pull request description.

##### Example bad description

>**Move user.js**
>
>This change moves user.js to the `src/controllers/auth` directory.

This is a poor description because it doesn't give the reader any information about the change beyond what they'd see in the diff.

##### Example good description

>**Move user.js to src/controllers/auth**
>
>When we created `user.js`, most of its callers lived in `src/lib/user`.
>
>We did a lot of restructing as part of the 4.2.x release, so now all of user.js’s clients live in `src/controllers/auth`, so this change moves `user.js` closer to the majority of its clients.

This is a better PR description because it explains the "why" behind the change.

#### Cross-referencing issues

If the PR resolves a Github issue, make the first line of the description `Resolves #XXX`, where `XXX` is the number of the Github issue it resolves. The `Resolves #XXX` [has special meaning](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword) within Github, as merging the PR will auto-close the associated issue.

If the PR is related to an issue but doesn't fix it, add a line that says `Related #XXX` so that Github cross-references the PR from the associated bug.

#### Revise the description to match the implementation

When we squash and merge the commit, the PR title and description become the commit message. The commit message is a permanent part of the source history, so we want it to be accurate when we merge the PR.

If changes during the code review process make the original PR description obsolete, remember to update the PR description to match the code.

### Drafts vs. non-drafts

Mark the PR as a "draft" when it's not ready to be merged in. You can request a review on a draft PR, but the implication is that you're seeking only preliminary, high-level feedback.

Click the PR's "Ready for Review" button on a draft PR when you feel the code is ready to be merged. Your reviewer will likely have feedback, but removing the "draft" state means that you've made the code as good as you can make it, and you'd be comfortable merging it in if your reviewer has no notes.

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

# Echo commands before executing them, by default to stderr.
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

Constant variables and exported environment variables should be uppercase.

```bash
readonly WELCOME_MESSAGE='Hello, world!'
```

```bash
WELCOME_MESSAGE="$(echo 'Hello, World!')"
readonly WELCOME_MESSAGE
export WELCOME_MESSAGE
```

```bash
print() {
  local -r MESSAGE=$1
  echo "${MESSAGE}"
}
```

Non-constant variables, such as the ones in loops, should be lowercase.

```bash
for value in 1 2 3; do
  echo "Hello "${value}" times"
done
```

### Command-line flags

If a bash script calls another application that accepts command-line flags, use long flag names where available.

```bash
# BAD - uses short flag names.
grep -i -o -m 2 -r '<span.*</span>' ./

# GOOD - uses long flag names.
grep \
  --ignore-case \
  --only-matching \
  --max-count=2 \
  --recursive \
  '<span.*</span>' \
  ./
```

Make exceptions for flags where the short flags are extremely common and the long names are used rarely:

* `mkdir -p`

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

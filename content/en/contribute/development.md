---
title: Development
description: Contribute to the development of Hugo.
categories: []
keywords: []
---

## Introduction

You can contribute to the Hugo project by:

- Answering questions on the [forum]
- Improving the [documentation]
- Monitoring the [issue queue]
- Creating or improving [themes]
- Squashing [bugs]

Please submit documentation issues and pull requests to the [documentation repository].

If you have an idea for an enhancement or new feature, create a new topic on the [forum] in the "Feature" category. This will help you to:

- Determine if the capability already exists
- Measure interest
- Refine the concept

If there is sufficient interest, [create a proposal]. Do not submit a pull request until the project lead accepts the proposal.

For a complete guide to contributing to Hugo, see the [Contribution Guide].

[bugs]: https://github.com/gohugoio/hugo/issues?q=is%3Aopen+is%3Aissue+label%3ABug
[contributing]: CONTRIBUTING.md
[create a proposal]: https://github.com/gohugoio/hugo/issues/new?labels=Proposal%2C+NeedsTriage&template=feature_request.md
[documentation repository]: https://github.com/gohugoio/hugoDocs
[documentation]: /documentation
[forum]: https://discourse.gohugo.io
[issue queue]: https://github.com/gohugoio/hugo/issues
[themes]: https://themes.gohugo.io/
[contribution guide]: https://github.com/gohugoio/hugo/blob/master/CONTRIBUTING.md

## Prerequisites

To build the extended or extended/deploy edition from source you must:

1. Install [Git]
1. Install [Go] version 1.23.0 or later
1. Install a C compiler, either [GCC] or [Clang]
1. Update your `PATH` environment variable as described in the [Go documentation]

[Clang]: https://clang.llvm.org/
[GCC]: https://gcc.gnu.org/
[Git]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
[Go documentation]: https://go.dev/doc/code#Command
[Go]: https://go.dev/doc/install

{{< note >}}
See these [detailed instructions](https://discourse.gohugo.io/t/41370) to install GCC on Windows.
{{< /note >}}

## GitHub workflow

{{< note >}}
This section assumes that you have a working knowledge of Go, Git and GitHub, and are comfortable working on the command line.
{{< /note >}}

Use this workflow to create and submit pull requests.

### Step 1

Fork the [project repository].

### Step 2

Clone your fork.

### Step 3

Create a new branch with a descriptive name that includes the corresponding issue number.

For a new feature:

```sh
git checkout -b feat/implement-some-feature-99999
```

For a bug fix:

```sh
git checkout -b fix/fix-some-bug-99999
```

### Step 4

Make changes.

### Step 5

Compile and install.

To compile and install the standard edition:

```text
go install
```

To compile and install the extended edition:

```text
CGO_ENABLED=1 go install -tags extended
```

To compile and install the extended/deploy edition:

```text
CGO_ENABLED=1 go install -tags extended,withdeploy
```

### Step 6

Test your changes:

```text
go test ./...
```

### Step 7

Commit your changes with a descriptive commit message:

- Provide a summary on the first line, typically 50 characters or less, followed by a blank line.
- Optionally, provide a detailed description where each line is 80 characters or less, followed by a blank line.
- Add one or more "Fixes" or "Closes" keywords, each on its own line, referencing the [issues] addressed by this change.

For example:

```sh
git commit -m "tpl/strings: Create wrap function

The strings.Wrap function wraps a string into one or more lines,
splitting the string after the given number of characters, but not
splitting in the middle of a word.

Fixes #99998
Closes #99999"
```

See the [commit message guidelines] for details.

### Step 8

Push the new branch to your fork of the documentation repository.

### Step 9

Visit the [project repository] and create a pull request (PR).

### Step 10

A project maintainer will review your PR and may request changes. You may delete your branch after the maintainer merges your PR.

[commit message guidelines]: https://github.com/gohugoio/hugo/blob/master/CONTRIBUTING.md#git-commit-message-guidelines
[issues]: https://github.com/gohugoio/hugo/issues
[project repository]: https://github.com/gohugoio/hugo/

## Building from source

You can build, install, and test Hugo at any point in its development history. The examples below build and install the extended edition of Hugo.

To build and install the latest release:

```sh
CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@latest
```

To build and install a specific release:

```sh
CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@v0.144.2
```

To build and install at the latest commit on the master branch:

```sh
CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@master
```

To build and install at a specific commit:

```sh
CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@0851c17
```

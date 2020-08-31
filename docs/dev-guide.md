---
title: Developer Guide
layout: docs
---

This topic describes how to contribute to the Tableau Server Client (Python)
project:

<!-- prettier-ignore -->
- TOC
{:toc}

---

## Submit your first patch

This section will get you started with the basic workflow, describing how to
create your own fork of the repository and how to open a pull request (PR) to
add your contributions to the **development** branch.

### Get the source code and set up your branch

1. Make sure you have
   [signed the CLA](https://tableau.github.io/contributing.html).

1. Fork the repository. We follow the "Fork and Pull" model as described
   [here](https://help.github.com/articles/about-collaborative-development-models/).

1. Clone your fork:

   ```shell
   git clone git@github.com:<user-name>/server-client-python.git
   ```

1. Run the tests to make sure everything is peachy:

   ```shell
   python setup.py test
   ```

1. Set up the feature/fix branch (based off the `development` branch). It is
   recommended to use the format issue#-type-description, for example:

   ```shell
   git checkout -b 13-fix-connection-bug development
   ```

For documentation changes, see the documentation section below.

### Code and commit

Here's a quick checklist to follow when coding to ensure a good pull request
(PR):

- Only touch the fewest number of files possible while still accomplishing the
  goal.
- Ensure all indentation is done as 4-spaces and your editor is set to unix line
  endings.
- The code matches PEP8 style guides. Make sure to run
  `pycodestyle tableauserverclient test samples` to catch and fix any style
  issues before submitting your pull request.
- Keep commit messages clean and descriptive.

### Adding features

1. Create an endpoint class for the new feature, following the structure of the
   other endpoints. Each endpoint usually has `get`, `post`, `update`, and
   `delete` operations that require making the url, creating the XML request if
   necessary, sending the request, and creating the target item object based on
   the server response.

1. Create an item class for the new feature, following the structure of the
   other item classes. Each item has properties that correspond to what
   attributes are sent to/received from the server (refer to docs and Postman
   for attributes). Some items also require constants for user input that are
   limited to specific strings. After making all the properties, make the
   parsing method that takes the server response and creates an instances of the
   target item. If the corresponding endpoint class has an update function, then
   parsing is broken into multiple parts (refer to another item like workbook or
   datasource for example).

1. Add testing by getting real xml responses from the server, and asserting that
   all properties are parsed and set correctly.

1. Add a sample to show users how to use the new feature.

### Add tests

All of our tests live under the `test/` folder in the repository. We use
`pytest` and the built-in test runner `python setup.py test`.

Follow the structure of existing tests, especially if new server responses
are going to be mocked.

If a test needs a
static file, like a .twb/.twbx/.xml, it should live under `test/assets/`

Make sure that all tests are passing before submitting your pull request.

### Update the documentation

When adding a new feature or improving existing functionality we ask that you
update the documentation along with your code. See the Updating documentation
section below for details.

### Commit changes to your fork and open a pull request

1. Make a PR as described
   [here](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork)
   against the **development** branch for code changes.

1. Wait for a review and address any feedback. While we try and stay on top of
   all issues and PRs it might take a few days for someone to respond. Politely
   pinging the PR after a few days with no response is OK, we'll try and respond
   with a timeline as soon as we are able.

1. That's it! When the PR has received
   ![](https://github.githubassets.com/images/icons/emoji/unicode/1f680.png){:height="5%"
   width="5%"} (:rocket:'s) from members of the core team they will merge the
   PR.

## Updating documentation

Our documentation is written in Markdown (specifically
[kramdown](https://kramdown.gettalong.org/quickref.html)) and built with Jekyll
on GitHub Pages.

All of the documentation source files can be found in `/docs` folder in the
**gh-pages** branch. The docs are hosted on the following URL:
<https://tableau.github.io/server-client-python>.

If you are just making documentation updates (adding new docs, fixing typos,
improving wording) the easiest method is to use the built-in `Edit this file`
feature (the pencil icon) or the `Edit this page` link.

To make more significant changes or additions, please create a pull request
against the **gh-pages** branch. When submitted along with a code pull request
(as described above), you can include a link in the PR text so it's clear they
go together.

### Running docs locally

To preview and run the documentation locally, these are the steps:

1. Install [Ruby](https://www.ruby-lang.org/en/downloads/) (v2.5.0 or higher)

1. Install [Bundler](https://bundler.io/)

1. Install [Jekyll](https://jekyllrb.com/docs/installation/)

1. Run the Jekyll site locally with `bundle exec jekyll serve`

1. In your browser, connect to <http://127.0.0.1:4000/server-client-python/>

For more details on the steps, see the GitHub Pages topic on
[testing locally](https://docs.github.com/en/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll).
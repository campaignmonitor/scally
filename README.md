<img src="https://dl.dropboxusercontent.com/s/anlzedtpekcnla7/logo.png" width="211">

[Campaign Monitor's](https://www.campaignmonitor.com/) fork of
[Scally](https://github.com/chris-pearce/scally). This fork is primarily for
allowing CM's to make quick updates to Scally without having to wait for the
main Scally version. The idea is everything we add to this fork will make it
back to the main version via a [Pull Request](https://help.github.com/articles/using-pull-requests/).




# Contents

- [Branches](#branches)
  - [master](#master)
  - [working](#working)
  - [Feature branches](#feature-branches)
- [Submitting new code](#submitting-new-code)
  - [Pull Requests](#pull-requests)
    - [PR format](#pr-format)
    - [What your PR should include](#what-your-pr-should-include)
    - [Examples and Guidelines](#examples-and-guidelines)
- [Test files](#test-files)
- [Putting updates back to the main Scally version](#putting-updates-back-to-the-main-scally-version)
- [NPM Package](#npm-package)




## Branches

They're 2 main branches:

- [**master**](https://github.com/campaignmonitor/scally/tree/master) (default)
- [**working**](https://github.com/campaignmonitor/scally/tree/working)

### master

The **master** branch should never be worked on—it's only for rebasing the main
Scally version and should always be up to date with it.

The **master** branch serves as a copy of the main Scally version in case
anything is to happen to it.

We will always get merge conflicts with the following files when rebasing the
**master** branch onto the **working** branch:

- `package.json`
- `.version`
- `README.md`

*We should always keep the forked version*—this is very important.

@chris-pearce will take care of keeping the CM fork in sync with the main
version and rebasing the **master** branch onto the **working** branch just to
keep this with one person.

### working

The **working** branch is the branch we work on—well not directly as all work
needs to happen on a feature branch which is a branch off the **working**
branch (see next section).

### Feature branches

All work needs to happen on feature branches branched off the **working**
branch.

If there's a [GitHub issue](https://github.com/campaignmonitor/scally/issues)
for the work you're doing then name your feature branch like:

```
issue-x
```

Where 'x' is the issue number.




## Submitting new code

Before making a change to the CM fork hit up the other front end developers to
see if it's a worthy change and in line with Scally's principles, architecture,
and naming conventions. A good place for any discussion around this would be
the Front-end Engineering room in HipChat and the [Front-end working group](https://campmon.com/wiki/display/DEV/Front-end+working+group).

It's important you have a good understanding of how Scally works before adding
to the CM fork—there is plenty of [documentation](https://github.com/chris-pearce/scally/blob/master/README.md)
to help with that and a [website](http://scally.chris-pearce.me/) on the way
and asking questions to the other front end developers.

### Pull Requests

Anything that needs to be merged to the **working** branch needs to be
reviewed via a PR.

All PR's need to point to the **working** branch **NOT** the **master**
branch! If GitHub is telling you you cannot merge to the **working** branch
then you'll need to sync up your feature branch with the **working** branch.
Do this via:

```
git fetch --all
git rebase origin/working
```

Do not use `git merge` or `git pull`!

#### PR format

Your PR title should use the same title as its corresponding GitHub issue but
prefixed with the issue number e.g.

> Issue #108: Remove style.scss and style.css from the repo and package json
files

And in the PR description include:

> This fixes #[x]

Where 'x' is the issue number. GitHub will offer an auto-complete menu as soon
as you type '#' where you can choose the corresponding PR.

You should also add a comment in the GitHub issue linking to the PR.

If your work doesn't have a GitHub issue then provide a descriptive title and
description.

#### What your PR should include

- Updated version number in the `package.json` and `.version` files following
  the [Semantic Versioning guidelines](http://semver.org/).
- An addition to the [**CHANGELOG-CM.md**](https://github.com/campaignmonitor/scally/blob/working/CHANGELOG-CM.md)
  following the format of the main Scally [**CHANGELOG.md**](https://github.com/chris-pearce/scally/blob/master/CHANGELOG.md).

#### Examples and Guidelines

For examples of PR's see Scally's main version [closed PR's](https://github.com/chris-pearce/scally/pulls?q=is%3Apr+is%3Aclosed).

Some guidelines to look at:

- [Code Reviews for New setup CSS](https://campmon.com/wiki/display/DEV/Code+Reviews+for+New+setup+CSS)
- [Contributing](https://github.com/chris-pearce/scally#contributing)




## Test files

To test your changes create `test.html` and `test.scss` files in the root,
these files will be ignored by git.

`test.html`:

```html
<!doctype html>
<html class="no-js u-s-p-huge">

  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>CM Scally testing</title>
    <link rel="stylesheet" href="test.css">
  </head>

  <body class="u-s-p-base">

  </body>

</html>
```

The contents of `test.scss` is the entire Scally framework, [see](https://github.com/chris-pearce/scally#sample-master-stylesheet).

Make sure your Sass compiles in both Ruby and LibSass:

- **Ruby Sass:**

  `sass --watch test.scss:test.css --style expanded`
- **LibSass:**

  `npm install node-sass -g`

  `node-sass test.scss test.css`




## Putting updates back to the main Scally version

If we decide an update should go back to the main Scally version—which in most
cases it should—then we'll do this by issuing a PR to the main Scally repo.

The PR should be created by the author of the update using the feature branch
the update was done on, following these [guidelines](https://github.com/chris-pearce/scally#submitting-code-to-scally).




## NPM Package

This fork is available as an npm package: [**cm-scally**](https://www.npmjs.com/package/cm-scally)
so we can easily use Scally in the `createsend.com` app.

We include the npm package in the `createsend.com` app [package.json](https://git.campmon.com/Freshview/createsend.com/blob/master/build/package.json)
and to get the latest version use `npm update cm-scally`.

# How to contribute

Each repository main branch is `master`. This branch always represents the absolute latest changes. A tag is created for each new version release. We follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html) for the tag name.

Fork the repository, make changes, and send us a [Pull request (PR)](#pull-request-style). We will review your changes and apply them to the `master` branch shortly, provided they don't violate our quality standards. To avoid frustration, before sending us your PR, please run full tool build mentioned in the `README.md` file of the repository.

After submitting PR, check CI status checks. If any check with "required" label fails, PR will not be merged.


## <a name="submit"></a> Submission Guidelines


### <a name="submit-issue"></a> Submitting an Issue

Before you submit an issue, please search the issue tracker. An issue for your problem might already exist and the discussion might inform you of workarounds readily available.

We want to fix all the issues as soon as possible, but before fixing a bug, we need to reproduce and confirm it.
In order to reproduce bugs, we require that you provide a minimal reproduction.
Having a minimal reproducible scenario gives us a wealth of important information without going back and forth to you with additional questions.

A minimal reproduction allows us to quickly confirm a bug (or point out a coding problem) as well as confirm that we are fixing the right problem.

We require a minimal reproduction to save maintainers' time and ultimately be able to fix more bugs.
Often, developers find coding problems themselves while preparing a minimal reproduction.
We understand that sometimes it might be hard to extract essential bits of code from a larger codebase, but we really need to isolate the problem before we can fix it.

Unfortunately, we are not able to investigate / fix bugs without a minimal reproduction, so if we don't hear back from you, we are going to close an issue that doesn't have enough info to be reproduced.


### <a name="submit-pr"></a> Submitting a Pull Request (PR)

Before you submit your Pull Request (PR) consider the following guidelines:

1. Search existing PRs for an open or closed PR that relates to your submission.
   You don't want to duplicate existing efforts.

2. Be sure that an issue describes the problem you're fixing, or documents the design for the feature you'd like to add.
   Discussing the design upfront helps to ensure that we're ready to accept your work.

3. [Fork](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) the target repository.

4. In your forked repository, make your changes in a new git branch:

     ```shell
     git checkout -b my-fix-branch master
     ```
   We recommend you to use this pattern `<issue number>-<one or two keywords of the issue title>` for the name of your branch to make it very short
   while ensuring that it remains unique. For example, to resolve issue `Introduce a unit test for class Toto (#3)`, we could use the following branch name :
   ```shell
     3-test-toto
   ```

5. Create your patch, **including appropriate test cases**.

6. Follow our [Coding Rules](#rules).

7. Run the full repository test suite, as described in the README.md file, and ensure that all tests pass.

8. Commit your changes using a descriptive commit message that follows our [commit message conventions](#commit).
   Adherence to these conventions is necessary because release notes are automatically generated from these messages.

     ```shell
     git commit -a
     ```
    Note: the optional commit `-a` command line option will automatically "add" and "rm" edited files.

9. Push your branch to GitHub:

    ```shell
    git push origin my-fix-branch
    ```

10. In GitHub, send a pull request to `endeavourmining/<repository name>::master` following [Our Pull request style](#pull-request-style).

### Reviewing a Pull Request

Follow our [Reviewing Rules](#review-rules).

#### Addressing review feedback

If we ask for changes via code reviews then:

1. Make the required updates to the code.

2. Re-run the repository test suites to ensure tests are still passing.

3. Create a fixup commit and push to your GitHub repository (this will update your Pull Request):

    ```shell
    git commit -a --amend --no-edit
    git push -f
    ```

That's it! Thank you for your contribution!


##### Updating the commit message

A reviewer might often suggest changes to a commit message (for example, to add more context for a change or adhere to our [commit message guidelines](#commit)).
In order to update the commit message of the last commit on your branch:

1. Check out your branch:

    ```shell
    git checkout my-fix-branch
    ```

2. Amend the last commit and modify the commit message:

    ```shell
    git commit --amend
    ```

3. Push to your GitHub repository:

    ```shell
    git push -f
    ```

> NOTE:<br />
> If you need to update the commit message of an earlier commit, you can use `git rebase` in interactive mode.
> See the [git docs](https://git-scm.com/docs/git-rebase#_interactive_mode) for more details.


#### After your pull request is merged

After your pull request is merged, you can safely delete your branch and pull the changes from the master (upstream) repository:

* Delete the remote branch on GitHub either through the GitHub web UI or your local shell as follows:

    ```shell
    git push origin --delete my-fix-branch
    ```

* Check out the master branch:

    ```shell
    git checkout master
    ```

* Delete the local branch:

    ```shell
    git branch -D my-fix-branch
    ```

* Update your local `master` with the latest upstream version:

    ```shell
    git pull --ff upstream master
    ```

## Testing

Refer to the section `Testing` of `CONTRIBUTION.md` file of the GitHub repository.


## Code style

Refer to the section `Code style` of `CONTRIBUTION.md` file of the GitHub repository.


## <a name="rules"></a> Coding Rules
To ensure consistency throughout the source code, keep these rules in mind as you are working:

- All features or bug fixes must be tested by one or more specs (unit-tests).
- All public API methods must be documented.
- All source code files must contain the license terms tagged in the repository `README.md` file.

You will find additional rules in the target repository according to the programming language used. You will also find some tools provided to enforce application of these rules. These tools should be run locally before submitting changes.

## <a name="pull-request-style"></a> Pull request style

Primary PR rule: it's the responsibility of PR author to bring the changes to the master branch.

Other important mandatory rule - it should refer to some ticket. The only exception is a minor fixes.

Pull request should follow [conventionalcommits.org](https://www.conventionalcommits.org/en/v1.0.0/) specificaction
to be ready for squasing as single commit:

Pull request should consist of two mandatory parts:
- "Title" - says **what** is the change, it should be one small and full enough sentence with only necessary information
- "Description" - says **how** this pull request fixes a problem or implements a new feature

### Title

Title format: `<type>[optional scope]: <description>`, where type is one of `conventionalcommits` type, optional scope
could be added as a context, and description should be as small as possible but provide full enough information to
understand what was done (not a process).

According to [git standards](https://git-scm.com/book/en/v2), commit messages uses present simple tence.

Title should not include links or references.

Good PR titles examples:
- fix: maven artifact upload - describes what was done: fix(ed), the what was the fixed: artifact upload, and where: Maven
- feat: GET blobs API for Docker - feat: new feature implemented, what: GET blobs API, where: Docker
- test: add integration test for Maven deploy - done: add(ed), what: integration test for deploy, where: Maven

Bad PR titles:
- Fixed NPE - not clear WHAT was the problem, and where; good title could be: "Fixed NPE on Maven artifact download"
- Added more tests - too vague; good: "Added unit tests for Foo and Bar classes"
- Implementing Docker registry - the process, not the result; good: "Implemented cache layer for Docker proxy"

### Description

Description provides information about **how** the problem from title was fixed.
It should be a short summary of all changes to increase readability of changes before looking to code,
and provide some context.

Description may contain a footers separated by blank line:
```
<body>

<footers>
```
Footer is a colon-separated key-value pair in standard form. It's supposed to be both: human-readable and machine parserable.
Common footers are:
```
Close: #1
Fix: #2
Reviewer: @github
Ref: https://external-tracker/issues/1
```

Each pull-request must include ticket reference (either `Close`, `Fix` or `Ticket`).

Example:
```
Check if the file exists before accessing it and return 404 code if doesn't

Fix: #123
```

Good description describes the solution provided and may have technical details, it isn't just a copy of the title.
Examples of good descriptions:
- Added a new class as storage implementation over S3 blob-storage, implemented `value()` method, throw exceptions on other methods, created unit test for value
- Fixed FileNotFoundException on reading blob content by checking if file exists before reading it. Return 404 code if doesn't exist

### Merging

We merge PR only if all required CI checks passed and after approval of repository maintainers.
If commit messages are not well-formatted or PR consists of many (greater than 3) commits, then
we merge using squash merge, where commit messages consists of two parts:
```
<PR title> (#<PR number>)

<PR description>
[PR: <PR number>]
```

GitHub usually automatically inserts title and description as commit messages.

If PR consists of small amount of well-formatted commits (commit messages follows all the rules of PR best practices),
then PR could be merged with merge commit.

### <a name="review-rules"></a> Review

It's recommended to request review from `@endeavourmining/maintainers` if possible.
When the reviewers starts the review it should assign the PR to themselves,
when the review is completed and some changes are requested, then it should be assigned back to the author.
On approve: if reviewer and repository maintainer are two different persons,
then the PR should be assigned to maintainer, and maintainer can merge it or ask for more comments.

The workflow:
```
<required> (optional)
        PR created |   Review   | Request changes | Fixed changes | Approves changes | Merge |
assignee: <none>  -> <reviewer> ->    (author)    ->  (reviewer)  ->   <maintainer>  -> <none>
```

When addressing review changes, two possible strategies could be used:
- `git commit --ammend` + `git push -f` - in case of changes are minor or obvious, both sides agree
- new commit - in case if author wants to describe review changes and keep it for history,
  e.g. if author doesn't agree with reviewer or maintainer, he|she may want to point that this changes was
  asked by a reviewer. This commit is not going to the master branch, but it will be linked into PR history.

### <a name="rules"></a> Commit style

We use https://www.conventionalcommits.org/en/v1.0.0/ for commit messages, it is:
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Commit styles are similar to PR, PR could be created from commit message: first line goes to the title,
other lines to description:
```
type(some-context): short title

Description of the commit goes
to PR description. It could be multiline `and` include
*markdown* formatting.

Close: #234
Ref: #123
```


## Repository maintaining

Each repository in Endeavour Mining has one responsible maintainer person. Maintainer responsibilities are:
1. Discuss requirements with customers and open-source users via internal and public channels. Discuss deadlines for important changes, and provide releases for milestones.
3. Track all bugs and features via ticket system. Track important changes via pull-requests.
4. Maintain the quality of all contributions in repository, as discussed in this document previously; including code, commits, tickets, PRs, wikis.
5. Keep CI/CD working in repository. Require build, test runs, minimum test-coverage on PR merge via branch-protection rules. Automate releases.
6. Track all changes for release, provide changelogs, release tags and descriptions. Obey [semver](https://semver.org/) convention, update version components properly.
7. Keep dependencies up to date.
8. Perform review process for pull requests.

Maintainers are:
- @baudoliver7 for:
  - endeavourmining/report-bot
  - endeavourmining/excel-validator
  - endeavourming/mail-crawler

- @amgmails for:
  - endeavourmining/ity-fragmentation-opt
  - endeavourmining/ity-fragmentation-webapp
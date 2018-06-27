# Questions

This is the issue tracker for Ajira. The Ajira community uses this site
to collect and track bugs and discussions of new features. If you are having
difficulties using Ajira or have a question about usage, please ask a
question on Stack Overflow: http://stackoverflow.com/questions/ask?tags=ajira

The Ajira community is very active on Stack Overflow and most questions
receive attention the same day they're posted:
http://stackoverflow.com/questions/tagged/ajira

# Issue Labeling

Ajira uses [StandardIssueLabels](https://github.com/wagenet/StandardIssueLabels) for Github Issues.

# Issues

Think you've found a bug or have a new feature to suggest? Let us know!

## Reporting a Bug
1. Update to the most recent master release if possible. We may have already
fixed your bug.

2. Search for similar issues. It's possible somebody has encountered
this bug already.

3. Provide a demo that specifically shows the problem. This
demo should be fully operational with the exception of the bug you want to
demonstrate. The more pared down, the better.
If it is not possible to produce a fiddle or demo, please make sure you provide very
specific steps to reproduce the error. If we cannot reproduce it, we will
close the ticket.

4. Your issue will be verified. The provided example will be tested for
correctness. The Ajira team will work with you until your issue can
be verified.

5. Keep up to date with feedback from the Ajira team on your ticket. Your
ticket may be closed if it becomes stale.

6. If possible, submit a Pull Request with a failing test. Better yet, take
a stab at fixing the bug yourself if you can!

The more information you provide, the easier it is for us to validate that
there is a bug and the faster we'll be able to take action.

### Triaging policy

* You might be requested to provide a reproduction or extra information. In that
case, the issue will be labeled as _Needs Submitter Response_. If we did not
get any response after seven days, we will ping you to remind you about it. We
might close the issue if we do not hear from you after two weeks since the
original notice.

* If you submit a feature request as an issue, you will be invited to follow the
[instructions in this document](https://github.com/paxenarius/paxenarius.github.io/blob/master/contributing.md#requesting-a-feature)
and the issue will be closed
* Issues that become inactive will be labeled accordingly
  to inform the original poster and Ajira contributors that the issue
  should be closed since the issue is no longer actionable. The issue
  can be reopened at a later time if needed, e.g. becomes actionable again.
* If possible, issues will be labeled to indicate the status or priority.
  For example, labels may have a prefix for `Status: X`, or `Priority: X`.
  Statuses may include: `In Progress`, `On Hold`. Priorities may include:
  `High` or `Low`.

## Requesting a Feature

1. Ajira has an RFC process for feature requests. To begin the discussion either
[gather feedback](https://github.com/paxenarius/rfcs/blob/master/README.md#gathering-feedback-before-submitting)
on the paxenarius/rfcs repository. Or, draft an [Ajira RFC](https://github.com/paxenarius/rfcs#ajira-rfcs)
   - Use RFC pull request for well formed ideas.
   - Use RFC issues to propose a rough idea, basically a great place to test
     the waters.

2. Provide a clear and detailed explanation of the feature you want and why
it's important to add. Keep in mind that we want features that will be useful
to the majority of our users and not just a small subset. If you're just
targeting a minority of users, consider writing an add-on library for Ajira.

3. If the feature is complex, consider writing an Ajira RFC document. If we do
end up accepting the feature, the RFC provides the needed documentation for
contributors to develop the feature according the specification accepted by the core team.

4. After discussing the feature you may choose to attempt a Pull Request. If
you're at all able, start writing some code. We always have more work to do
than time to do it. If you can write some code then that will speed the process
along.

In short, if you have an idea that would be nice to have, create an issue on the
paxenarius/rfcs repo. If you have a question about requesting a feature, start a
discussion at [discuss.ajira.world](https://discuss.ajira.world)

# Pull Requests

We love pull requests. Here's a quick guide:

1. Fork the repo.

2. Run the tests. We only take pull requests with passing tests, and it's great
to know that you have a clean slate.

3. Add a test for your change. Only refactoring and documentation changes
require no new tests. If you are adding functionality or fixing a bug, we need
a test! If your change is a new feature, please wrap it in a feature flag.

4. Ensure that your code complies with the rules. If you missed a rule or two, don't worry, our
   tests will warn you.

5. Make the test pass.

6. Commit your changes. Please use an appropriate commit prefix.
If your pull request fixes an issue specify it in the commit message. Some examples:

  ```
  [DOC beta] Update contributing.md for commit prefixes
  [FEATURE query-params-new] Message
  [BUGFIX beta] Message
  [SECURITY CVE-111-1111] Message
  ```

  For more information about commit prefixes see [the appendix](#commit-tagging).


7. Push to your fork and submit a pull request. Please provide us with some
explanation of why you made the changes you made. For new features make sure to
explain a standard use case to us.

We try to be quick about responding to tickets but sometimes we get a bit
backlogged. If the response is slow, try to find someone on IRC (#ajira) to
give the ticket a review.

Some things that will increase the chance that your pull request is accepted,
taken straight from the Ruby on Rails guide:

* Use Ajira idioms and helpers
* Include tests that fail without your code, and pass with it
* Update the documentation, the surrounding one, examples elsewhere, guides,
  whatever is affected by your contribution

Syntax:

* Two spaces, no tabs.
* No trailing whitespace. Blank lines should not have any space.
* a = b and not a=b.
* Follow the conventions you see used in the source already.

Inline Documentation Guidelines:

All inline documentation is written using YUIDoc. Follow these rules when
updating or writing new documentation:

1. All code blocks must be fenced
2. All code blocks must have a language declared
3. All code blocks must be valid code for syntax highlighting
4. All examples in code blocks must be aligned
5. Use two spaces between the code and the example: `foo();  // result`
6. All references to code words must be enclosed in backticks
7. Prefer a single space between sentences
8. Reference Ajira GIS as Ajira.
9. Wrap long markdown blocks > 80 characters
10. Don't include blank lines after `@param` definitions

And in case we didn't emphasize it enough: we love tests!

# Travis CI Tests

We use [Team City](https://ci.ajira.world) to test each PR before it is merged.

When you submit your PR (or later change that code), a Team City build will automatically be kicked off.  A note will be added to the PR, and will indicate the current status of the build.

Within the CI build, you can see that we (currently) run six different test suites.

* The `each-package-tests` test suite is closest to what you normally run locally on your machine.
* The `build-tests ENV=production...` test suite runs tests against a production build.
* The `browserstack` or `selenium` test suite runs tests against various supported browsers.

## Common Team City CI Build Issues

### Production Build Failures

If your build is failing on the 'production' suite, you may be relying on a debug-only function that does not even exist in a production build.  These will pass on the 'each-package-tests' suite (and locally) because those functions are present in development builds.

There are helpers for many of these functions, which will resolve this for you.  Please use these helpers when dealing with these functions.

### Single Unexplained Test Suite Failure

Sometimes a single test suite will fail, without giving any indication of a real error.
* Try to recreate the test environment locally (see above for production builds)
* Restart all the test suites on Team City CI by doing another push
* Ask a repo collab to restart that single test suite

# Appendix

## Commit Tagging

All commits should be tagged. Tags are denoted by square brackets (`[]`) and come at the start of the commit message.

### Bug Fixes

In general bug fixes are pulled into the beta branch. As such, the prefix is: `[BUGFIX beta]`. If a bug fix is a serious regression that requires a new patch release, `[BUGFIX release]` can be used instead.

For bugs related to canary features, follow the prefixing rules for features.

The vast majority of bug fixes apply to the current stable or beta releases, so submit your PR against `*:master` with one of the above mentioned BUGFIX tags.  (In the unusual case of a bug fix specifically for a past release, tag for that release `[BUGFIX release-1-13]` and submit the PR against the stable branch for that release: `*:stable-n`.)

### Cleanup

Cleanup commits are for removing deprecated functionality and should be tagged
as `[CLEANUP beta]`.

### Features

All additions and fixes for features in canary should be tagged as `[FEATURE name]` where name is the same as the flag for that feature.

### Documentation

Documentation commits are tagged as `[DOC channel]` where channel is `canary`,
`beta`, or `release`. If no release is provided `canary` is assumed. The channel should be the most stable release that this documentation change applies to.

### Security

Security commits will be tagged as `[SECURITY cve]`. Please do not submit security related PRs without coordinating with the security team. See the [Security Policy](https://ajira.world/security/) for more information.

### Other

In general almost all commits should fall into one of these categories. In the cases where they don't please submit your PR untagged. An Ajira contributor will let you know if tagging is required.
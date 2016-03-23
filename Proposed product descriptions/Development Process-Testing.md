# KBase Development Process: Testing improvements

## Summary

An initial implementation of basic end-to-end testing for at least one
repository in the project, to start establishing best practices on this front.

## Story/Description

KBase is in serious need of improved testing practices across the project.
This single-sprint effort aims to start paying some fo that technical debt by
showing how to implement automated testing at multiple levels for at least one
repository in the project.

Improved testing practices, once adopted project-wide, will have a significant
impact in improving code quality and reducing the re-appearance of
previously-fixed bugs.  This is a long-overdue, most basic of improvements to
the software engineering standards of the project, so while "now" is already
*late*, late is better than never.

The implementation team should identify a few (no more than three) KBase
repositories where the following should be implemented.  This sprint should be
able to complete the tasks for at least *one* of them in full, but the other
two should be available as stretch goals.

In this case, the "product" consists of completing the following:

* Instrument the repository with a testing code coverage tool that includes
  online per-build reports, such as [codecov](https://codecov.io) or
  [coveralls](https://coveralls.io) (the team should identify the appropriate
  tool to use).

* Add substantial unit tests to the repository and track the resulting code
  coverage. A substantial improvement in test coverage should be achieved by
  the end of the sprint (whether the repo had some tests in the first place or
  not).

* Identify, if necessary, what mocking library to use for unit tests to
  complete.

* Activate Github's TravisCI for the repo, so that new pull requests are
auto-tested before review.

* Add integration testing that executes inside KBase's Jenkins infrastructure.

* Identify at least one bug in that repo that needs fixing, add tests for
the bug and fix it, to demonstrate basic regression testing.

* Write up a summary document explaining how the above was completed and submit
  it to the [project guides](https://github.com/kbase/project_guides)
  repository, so that it can serve as a continually improved set of guidelines
  for the project.

## User stories

* Users will be able to go to any of the project's repositories and find the
  testing coverage for that repo, the results of the latest build, and tests
  associated with any previously reported and fixed bugs.

* When making new contributions to the project, users and developers will be
  able to see their pull requests immediately tested even before the code is
  reviewed.  The review process than thus proceed with higher confidence that
  the code in question doesn't break any existing functionality.

## Narrative Mockup

N/A

## Timeline

While this is an area where the project should, over time, do a lot more work,
for now this is being deliberately scoped to a single sprint.  In the face of
many other competing priorities, at least spending *one* sprint building better
testing will help the project start adopting these practices as part of the
regular development process.

## Test plan

By definition, this PD is specifically about testing, so this is covered above.

## Citations

N/A

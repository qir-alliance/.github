# QIR Alliance Contribution Policy 1.0

This document provides the contribution policy for specifications and other
documents developed using the QIR Alliance Specification development process in
a repository (each a “Working Group”). Additional or alternate contribution
policies may be adopted and documented by the Working Group.

## Contribution Guidelines

The Working Group accepts contributions via pull requests. The following
sections outlines the process for merging contributions to the specification.

### 1. Issues

Issues are used as the primary method for tracking anything to do with the
specification Working Group.

#### 1.1. Issue Types

There are three types of issues (each with their own corresponding label):

- **Discussion** <br/>
  These are support or functionality inquiries that we want to have a record of
  for future reference. Depending on the discussion, these can turn into "Spec
  Change" issues.

- **Proposal** <br/>
  Used for items that propose a new ideas or functionality that require a larger
  discussion. This allows for feedback from others before a specification change
  is actually written. All issues that are proposals should both have a label
  and an issue title of "Proposal: [the rest of the title]." A proposal can
  become a "Spec Change" and does not require a milestone.

- **Spec Change** <br/>
  These track specific spec changes and ideas until they are complete. They can
  evolve from "Proposal" and "Discussion" items, or can be submitted
  individually depending on the size. Each spec change should be placed into a
  milestone.

#### 1.2. Issue Lifecycle

The issue lifecycle is mainly driven by the Maintainer. All issue types follow
the same general lifecycle. Differences are noted below.

- **Issue Creation**

- **Triage**

  - The Editor in charge of triaging will apply the proper labels for the issue.
This includes labels for priority, type, and metadata.
  - (If needed) Clean up the title to succinctly and clearly state the issue. Also
ensure that proposals are prefaced with "Proposal".

- **Discussion**

  - "Spec Change" issues should be connected to the pull request that resolves it.
  - Whoever is working on a "Spec Change" issue should either assign the issue to
    themselves or make a comment in the issue saying that they are taking it.
  - "Proposal" and "Discussion" issues should stay open until resolved.

- **Issue Closure**

### 2. Pull Requests

The next section contains more information on the workflow followed for Pull
Requests.

#### 2.1. Pull Request Creation

- We welcome pull requests that are currently in progress. They are a great way
  to keep track of important work that is in-flight, but useful for others to
  see. If a pull request is a work in progress, it should be prefaced with "WIP:
  [title]". You should also add the wip label Once the pull request is ready for
  review, remove "WIP" from the title and label.

- It is preferred, but not required, to have a pull request tied to a specific
  issue. There can be circumstances where if it is a quick fix then an issue
  might be overkill. The details provided in the pull request description would
  suffice in this case.

- The Working Group uses pull requests to track changes. To submit a change to the
specification:

  1) Fork the Repo, modify the Specification to address the Issue
  2) Submit a Pull Request

#### 2.2. Triage

The Editor in charge of triaging will apply the proper labels for the issue.
This should include at least a size label, a milestone, and awaiting review once
all labels are applied.

#### 2.3. Reviewing/Discussion

- All reviews will be completed using the review tool.
- A "Comment" review should be used when there are questions about the spec that
  should be answered, but that don't involve spec changes. This type of review
  does not count as approval.
- A "Changes Requested" review indicates that changes to the spec need to be
  made before they will be merged.
- Reviewers should update labels as needed (such as needs rebase).
- When a review is approved, the reviewer should add LGTM as a comment.
- Final approval is required by a designated Editor. Merging is blocked without
  this final approval. Editors will factor reviews from all other reviewers into
  their approval process.

#### 2.4. Being Responsive

Pull request owner should try to be responsive to comments by answering
questions or changing text. Once all comments have been addressed, the pull
request is ready to be merged.

#### 2.5. Merge or Close

- A pull request should stay open until a Maintainer has marked the pull request
  as approved.
- Pull requests can be closed by the author without merging.
- Pull requests may be closed by a Maintainer if the decision is made that it is
  not going to be merged.

# Steering Committee Meeting March 2022

Attendance: Alex Chernoguzov, Bettina Heim, Kalan Snyder, Ross Duncan, Sonia 
Pignorel, Roland Guichard (Guest), Seyon Sivarajah (Guest),
(offline follow up with Tom Lubinski)

## Meeting agenda

- Recap and status
- Steering committee meeting and attendees
- GitHub issues
- qir-book repo under the QIR Alliance
- Inquiry from the Linux Foundation
- Status and updates from the workstreams

## Recap and status

- PR to update meeting minutes and org repo is up
- Runtime initialization/finalization workstream:
  - working group is about to be launched and is scheduled to meet at a weekly cadence
  - [issue #11](https://github.com/qir-alliance/qir-spec/issues/11) on the spec
    repo is used to track the work going forward
- [Discussions](https://github.com/qir-alliance/qir-spec/discussions) have
  been enabled on the spec repo
- Discussions around the feasibility and desirability of the following
  requirement for the Base Profile workstream and are being discussed
  [here](https://github.com/qir-alliance/qir-spec/discussions/17): <br/>
  > *"Any Base Profile compliant program should also be compliant with the QIR
    specification and future profiles [...]"*

## Key decisions (accepted unanimously, one voting member absent)

- Addition of a qir-book repository under the QIR Alliance including the
  following: <br/>
  - initially populated with the content currently reflected [here](https://www.sckaiser.com/qir-book/)
  - repo should serve as a location to accumulate community efforts to
    facilitate engaging with other tools and project under the QIR Alliance org
    and beyond
  - containers, examples, and conceptual documentation are expected to be added
    over time

## Follow-ups / Action items

- Kalan to reach out to ORNL team to confirm planned projects and timelines
- Sonia and Bettina to draft an addition to the
  [Project_Organization.md](https://github.com/qir-alliance/.github/blob/main/Project_Organization.md)
  and [Governance.md](https://github.com/qir-alliance/.github/blob/main/Project_Organization.md)
  documents with more specific guidance
- Bettina to draft a response to the Linux Foundation regarding updates from
  the QIR Alliance; everyone to share input and feedback in email
- Steering committee delegates to check in with their respective orgs if they
  would like to take the opportunity to participate in a video as part of a
  series of materials prepared within the Linux Foundation;
  - get back to Bettina by 07/27 regarding interest and suggested content,
  - Bettina to respond to Tim Serewicz and put interested parties in contact
- Sonia to send out a poll to identify a better meeting time
- Bettina to merge the [PR](https://github.com/qir-alliance/qir-spec/pull/20)
  addressing [Issue #8](https://github.com/qir-alliance/qir-spec/issues/8) on
  the spec repo asking for the appropriate BibTeX citation

## Additional notes

- Sonia Pignorel to replace Fabrice Frachon in the SC meeting
- The Linux Foundation has reached out with a request for an update from the
  QIR Alliance, as well as feedback/support for training materials on Quantum Computing
- Base Profile workstream:
  - Working group is drafting a document to describe different compilation stage
  - Working group has reached an agreement regarding separating the
    specification of QIR Profiles, quantum instruction sets (QIS), and output
    formats
  - Different QIS in use are specified by adding all used instructions to the
    list of naming conventions, and adding a document listing the instructions
    that are part of that instruction set
  - Each profile contains a section that outlines any requirements for a QIS to
    be compatible with that profile
  - The output format contains an identifier for the format as well as an
    identifier for the labeling scheme;
    this permits that the IR generating frontend can choose the labeling scheme
    used to interpret the output, and the executing backend can choose what
    output format to produce
  - We hope to have a PR to present to the steering committee for consideration
    by the next SC meeting

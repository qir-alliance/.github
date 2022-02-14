# Steering Committee Meeting December 2021

Attendance: Alex Chernoguzov, Alex Mccaskey, Andrei Petrenko, Bettina Heim,
Dmitry Liakh, Kalan Snyder, Thien Nguyen, Tom Lubinski, Wim Lavrijsen, Sarah
Kaiser (Guest), Seth Newberry (Guest)

## Meeting agenda

- Recap of previous decisions
- ORNL steering committee representative
- Q2B follow ups
- External communication
  - Contacts
  - Community forums
  - QIR Alliance org page
- NWQSim repo under the QIR Alliance
- Workstreams & next steps

## Recap of previous decisions

- Code repositories under the QIR Alliance
  - Addition of the following repos: PyQIR, QAT, QCOR
  - Requirements for code repositories
- Steering committee can invite subject matter experts, including non-members
  - Invitation extended to Alex McCaskey and Wim Lavrijsen
  - Repo maintainers can attend steering committee meetings

## Key decisions (all voted unanimously)

- Community forums:
  - QIR channel on Unitary Fund Discord is a good venue to point people to
  - Unitary Fund will set up community calls for QIR
- QIR Alliance org page:
  - We will add a news section about currently active workstreams, upcoming
    events, blogs, announcements.
  - We will add links to community forums to the Inquiries section, and
    specifically refer to the Unitary Fund Discord and community call
- Addition of a NWQSim repository under the QIR Alliance including the
  following: <br/>
  - single-device/single-node-multi-device/multi-node state-vector simulator
    SV-Sim with CPU and NVIDIA/AMD GPU support
  - single-device/single-node-multi-device/multi-node density-matrix simulator
    with CPU and NVIDIA/AMD GPU support
  - a wrapper of SV-Sim and DM-Sim to connect with the QIR-Runtime
  - Makefile/Cmake files
  - several Q#/QIR examples, including example from Qiskit to QIR to DM-Sim with
    noise
  - License and notes
  - Documentation and papers

## Follow-ups / Action items

- Bettina to draft workstream template and workstream description for specifying
  a Base Profile
- Alex M. to draft workstream description for extending the specification to
  include runtime initialization/finalization and entry point handling
- Bettina and Tom will follow up with Celia Merzbacher (QED-C), action
  items related to creating comprehensive materials to be defined later

## Additional notes

- GitHub
  - Specification and three code repositories migrated
  - Created org repo (.github) with readme, code of conduct, license,
    governance, logos (made available for use to everyone)
  - Minutes are published on the org repo and linked in the readme
  - Workflow template for spell checking
  - Pending: CLA bot

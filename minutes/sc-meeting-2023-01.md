# Steering Committee Meeting January 2023

Attendance: Alex Chernoguzov, Alex McCaskey, Bettina Heim, Bill Ticehurst,
Kalan Snyder, Sonia Pignorel, Tom Lubinski, Vicente Leyton-Ortega, Wim
Lavrijsen

## Meeting agenda

- Recap and status
- Q2B feedback: Provide a clear explanation for QIR
- Workstreams and community call updates
- Adaptive profile definition kick-off
- Upcoming opportunities
- 2023 conferences planning
- Next steps

## Recap and status

- Quick round of what's been happening
  - Community calls have been going on even during the holidays; people were
  happy to chat about the Quantum compilation
  - Runtime workstream has picked back up with a meeting today after the
  Steering Committee meeting
  - Opaque pointer
    - LLVM 15 treats all pointers as opaque by default
    - Issue #30 is opened for resolution

- Q2B feedback
  - Add a clarifying paragraph about QIR being a subset of LLVM on the QIR
 site, but also about QIR defining how to use LLVM in a better way

- Workstream and Community call updates
  - End-users of QIR are compiler engineers; for those the specification is
  sufficient
  - We also need to provide a way for other users to understand the profile
  beyond the specification, e.g. what solutions do QIR enable, and problems
  does it solve?
  - QIR Book is looking at engaging researchers in the compiler space or
  students getting into the quantum space
  - QIR Book is an approachable outline of what QIR is for people not directly
  familiar with the space
  - UnitaryFund grant for Paria to contribute to the QIR Book to flesh out the
  content a bit more

- Adaptive profile workstream
  - Should we include another entity in the workstream?
  - Do we want to grow in the next year, the community and also the Steering
   Committee?
  - In general, should we add other entities to the Steering Committee?
  - Or not because we are big enough that we don't want to add anybody in the
  next year
  - If we give suggestions to companies, what are some of the aspects to consider?
    - Software tools developers (as it may be beneficial to integrate with
    them in the future?)
    - Look at what competes with QIR and seek common ground
    - Grow the alliance to reach the point it is a common standard
    - Look at who has an interest in QIR
    - Quantum languages developers, make sure new programming languages
    compile to QIR
    - AI is making a lot of Quantum contributions
    - Control software and hardware companies
    - One criterion would be whether they have a desire to collaborate and an
    interest for interoperability
    - Active in the QIR community with a concrete project
  - Consider academic advisory roles, e.g. adviser steering members

- Conferences
  - In the next three months, there is the NVIDIA conference; if anyone wants
  to highlight the QIR Alliance collaborative effort there
  - Next month, we will cover the conferences for the rest of the year

## Key decisions (all voted unanimously)

One paragraph clarifying QIR will be created, reviewed by the Steering
Committee and added to the QIR Alliance website home page.

## Follow-ups / Action items

- At the following community calls, do a rundown of MLIR and seek suggestions
for resolution of the opaque pointer
- Write a clear paragraph on QIR, send it to everyone for review, and any
objection must be raised by the 20th
- Contact companies that could be a potential addition to the Steering
Committee to gauge their interests, and agree to invite them

## Additional notes

- References
  - [Opaque Pointer issue](https://github.com/qir-alliance/qir-spec/issues/30)
  - [QIR Book](https://github.com/qir-alliance/qir-book)
  - [QIR Alliance site](https://github.com/qir-alliance)

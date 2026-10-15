# Workstream: QIR Modules and Externs

## Motivation & Benefits
Current QIR specification assumes all code is in the same executable main module.
This assumption is limiting modular code development and code reuse.
Ability to define common libraries of reusable algorithms as standard QIR modules can enhance QIR ecosystem attractiveness for developers.

Additionally, many QPU platforms offer platform capabilities that can be called directly from QIR.
These can provide specific hardware control or generic access to classical control extensions often used for online QEC decoding
or other forms of accelerated classical computing that are not easy or practical to express in QIR natively.

Both capabilities are expected to play a key role as the industry migrates to larger fault-tolerant machines. 
In FT world QIR can be used to represent programs at computational qubit level, QEC gadget level, and physical qubit level. 
QIR libraries may be used to provide QEC gadget definitions in this scenario.
While QEC is the primary motivating use case for reusable QIR libraries, the workstream shall consider a generic capability applicable to any other future use case.

This workstream will define a standard LLVM-compliant way of constructing and referencing library modules and external platform functions.

QIR libraries/modules provide reusable QIR function definitions; external functions
are implemented outside those QIR libraries, potentially by a platform or runtime.
Both may be referenced through LLVM declarations. The distinction is where
implementations are provided and how dependencies are resolved.

## Requirements
- Define QIR library module format and conformance requirements
  - Consider LLVM-compatible formats and whether alternatives are needed
- Define QIR library module reference
  - Consider hierarchical versus flattened library dependencies
  - Consider QIR and architecture compatibility for linking modules without
    assuming all modules must target identical hardware architectures
- Define external function reference
  - Consider calling conventions, compatibility, and function resolution at
    compile/link time or through runtime-provided capabilities
  - Consider platform-specific attributes
- Use LLVM-standard techniques as much as possible

## Dependencies & Related Projects
This workstream does not depend on any prior profiles and defines a new foundational QIR capability.

## Deliverable(s) & Expected Outcome
The workstream will deliver a new profile or a set of changes to the base QIR specification depending on the outcome.

Two independent specification PRs may be delivered within this workstream: one
for QIR libraries/modules and another for external linking, particularly for
accelerated classical processing.

Additionally, a set of examples using new capabilities shall be constructed and made available as a reference for the community.

## Future Work (Out of Scope)
- Further customization for use with QEC, logical qubit block encoding, etc.
- Package management, build systems, and vendor-specific runtime implementations

## Working Group & Getting Involved

Chair: Proposed Kartik Singhal (Quantinuum)\
Members: TBD

If you would like to contribute to the workstream, please contact the chair.

## Schedule

Launch date: November 2, 2026\
Estimated end date: May 1, 2027\
Meeting schedule and/or channel(s) of communication: TBD

## Status & Discussions

The work and status is tracked in the form of a GitHub issue \<insert link\>.

We encourage comments, inputs, and discussions on that issue.

The GitHub issue is labeled as `Approved` after approval by the steering
committee.

## Open Questions

- Which library module formats and QIR conformance requirements are needed?
- Should dependencies remain hierarchical or be flattened, and where can
  existing LLVM mechanisms meet the requirements?
- Which compatibility constraints apply to modules and external functions
  across architectures and platforms?
- What resolution guarantees or additional information are needed beyond
  existing LLVM mechanisms, including for runtime-provided capabilities?

# Workstream: Opaque Pointer Support

## Motivation & Benefits

Support for typed pointers in LLVM is being removed. More information about the
motivation for this change can be found in LLVM forums. For example, the LLVM
documentation on [opaque pointers](https://llvm.org/docs/OpaquePointers.html) as
well as [this
presentation](https://llvm.org/devmtg/2022-04-03/slides/keynote.Opaque.Pointers.Are.Coming.pdf)
give a brief overview.

The QIR specification currently makes use of typed pointers to represent qubit
values and result values. While in LLVM 15, support for these types can still be
enabled, an update to LLVM 16 requires us to change this representation.

The goal of this workstream is hence to update the QIR specification to support
newer versions of LLVM, and to document what LLVM versions can be used to
support each version of the QIR specification.

## Requirements

Generally, LLVM maintains very good [backwards
compatibility](https://llvm.org/docs/DeveloperPolicy.html#ir-backwards-compatibility);
according to the LLVM 18 docs, it is possible to load even bitcode generate by
an LLVM version as early as 3.0. However, it is not possible in general to
generate bitcode that can be loaded with an older version of LLVM than the one
used to emit it. This means that while *QIR consumers*, i.e. backend providers,
can update to the latest LLVM version without sacrificing support for prior QIR
versions, whereas *QIR producers*, i.e. language frontends, cannot use LLVM
versions that are newer than the one required by the versions of the QIR
specification they support. This can pose challenges for maintaining a
state-of-the art frontend.

As part of this workstream, we hence specifically propose to update the required
LLVM version for the next version of the QIR specification to LLVM 16.

## Dependencies & Related Projects

There are no related projects within the QIR Alliance at this time. However,
there are a number of threads in the LLVM community by projects with similar
needs. In particular, the considerations discussed in [this
thread](https://discourse.llvm.org/t/rfc-better-support-for-typed-pointers-in-an-opaque-pointer-world/63339)
and the follow up
[here](https://discourse.llvm.org/t/rfc-adding-opaque-types-to-llvm-ir/65326)
also apply to the QIR ecosystem.

See also the section on [Open Questions](#open-questions) regarding possible
alternatives to consider.

A related topic to consider when discussing options for this workstream is
whether the new representation would also allow to support qudits in the future.

## Deliverable(s) & Expected Outcome

The expected outcome of the workstream is a pull request to update the 0.1
version of the QIR specification with the necessary changes to be able to emit
the full QIR and all its profile using LLVM 16.

## Future Work (Out of Scope)

Migration plan for shared components?

## Working Group & Getting Involved

Members: <br/>
Chair:

If you would like to contribute to the workstream, please contact \<insert
contact\>.

## Schedule

Launch date: <br/>
Estimated end date: <br/>
Meeting schedule and/or channel(s) of communication:

## Status & Discussions

The work and status is tracked in the form of a GitHub issue \<insert link\>.
<br/>
We encourage comments, inputs, and discussions on that issue.

The GitHub issue is labeled as `Approved` after approval by the steering
committee.

## Open Questions

As part of the workstream, we could re-examine the use of address spaces to
distinguish memory on the QPU itself (i.e. qubits) from memory located on an
adjacent classical processor. See also [this
thread](https://discourse.llvm.org/t/casting-between-address-spaces-and-address-space-semantics/10920/16)
that contains a discussion about the nature and use of different address spaces.

There may be options to consider for representing quantum specific data types,
and merely migrating from typed to opaque pointers may not be the best option.
E.g. the working group should consider if it is desirable at all to work with
pointers, especially since the QIR specification prohibits dereferencing of
resources that are located on the QPU.
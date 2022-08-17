# Steering Committee Meeting August 2022

Attendance: Alex Chernoguzov, Alex McCaskey, Bettina Heim, Kalan Snyder,
Laurent Ajdnik (Guest), Ross Duncan, Sonia Pignorel, Tom Lubinski,
Vicente Leyton-Ortega

## Meeting agenda

- Recap and status
- Base Profile spec request for approval
- Nvidia new SC member candidate
- Clause for the rhythm of business
- Next steps

## Recap and status

- The Base Profile Working Group looked at the PR for the specification
and gave their feedback.
- The Base Profile specification is ready to be shared with the Steering Committee.
- Bettina gave a walkthrough of the Base Profile specification to the Steering Committee.
- Vicente has offered to represent ORNL.

## Key decisions (all voted unanimously)

- The Steering Committee approved Nvidia as a new Steering Committee member.

## Follow-ups / Action items

- The Steering Committee members will be reviewing the Base Profile PR offline.
- The vote will be on approval of the PR.
- Share the specification with the broader community.
- Follow through on the implementation.
- Create a draft PR for the rhythm of the business clause.

## Additional notes

- Any breaking change will increase the version number. The review will
hopefully catch any discrepancy.
- Before we cut a version number for the spec, conclude on the other workstream
(the runtime initialization workstream).
- The labels for output recording are global constants.
- The labels will be part of the IR even if the backend ignores them.
- The frontend needs to support both output schemas simultaneously; the backend
has the autonomy to choose the schema.
- The requirement is to have the qubit in a zero state at the beginning; thus
no need for initialization.
- LLVM uses module metadata when combining modules.
- The Base Profile workstream has its custom tooling. Even if LLVM does not act
on metadata, we could still enforce it as part of our tooling.
- The “qir_profile” is an attribute that contains the QIR profile that is attached
to an entry point and not attached to a module flag. In the future, it will be
possible to attach other attributes.
- The “required_num_qubits” and "required_num_results” are helpful for some backends.
- For a quantum instruction that has a string in it, use a constant string in the IR.
- The Base Profile does not intend to have any variable defined.
- The output recording section specifies the available runtime functions.
- The module flags contain minor and major versions “qir_minor_version” and
“qir_major_version” and are a way to determine an older version of the specification.
- QIS can depend on other data types than %Qubit* and %Result*. It might be
possible to introduce a new type in the next iteration.
- Share the Base Profile PR on QuTiP (Unitary Fund Discord channel) and make it
a topic of the next QIR community call.
- Nvidia is very supportive of the alliance and interested in QIR as it is a
good platform for IR inspection; Nvidia will bring tooling and a new community
to QIR.
- References
  - [Base Profile Specification](https://github.com/qir-alliance/qir-spec/blob/base-profile/specification/under_development/profiles/Base_Profile.md)
  - [Runtime Initialization Workstream](https://github.com/amccaskey/.github/blob/main/workstreams/Runtime_Init_Finalize_EntryPoint_Workstream.md)
  - [QIR Alliance Project Charter](https://github.com/qir-alliance/.github/blob/main/Project_Organization.md)

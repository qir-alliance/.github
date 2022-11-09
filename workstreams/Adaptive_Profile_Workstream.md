# Workstream: Adaptive-Profile Definition

## Motivation & Benefits

A profile of a specification is a subset of the specification that defines a
coherent set of functionalities and capabilities that might be offered by a
system. Defining profiles allows a specification to be forward-looking and
expansive without requiring implementations to support the full specification.
Profiles also provide a roadmap for implementors by specifying stages they can
progress through that will be useful to consumers of the specification.

## Requirements

The Adaptive Profile should specify the requirements to support defining and
executing quantum programs that permit for limited classical computations and
control flow during execution. In addition to a set of LLVM instructions, the
Adaptive Profile may rely on a quantum instruction set defined separately, but
should not make use of any runtime functions beyond the functions used for
initialization/finalization and output recording.

The profile should specify all permitted LLVM instructions, and define all
required constructs for the program to be valid and executable on targeted
backends. This includes specifying required and optional attributes,
requirements and recommendations for defining QIS functions that can be used
when targeting an Adaptive Profile, and the runtime functions for output
recording. The profile specification should furthermore clarify the usage of
data types and values.

The defined requirements should permit to implement a tool that validates the
program to the degree that compile-time validation is reasonable. The section
outlining the use of data types and values should define any cases of undefined
behavior and/or cases that result in failure (only) during execution, as it may
be the case for example when dividing by zero. It is a non-goal to be able to
ensure that classical values remain within the supported range for that data
type as part of compilation or validation. The profile should define a mechanism
for handling failures at runtime that does not require runtime support beyond
what is otherwise needed for program execution. The mechanism specifically
should not require aborting execution upon failure or supporting logging a
string value during execution.

Any Base Profile compliant program should also be compliant with the Adaptive
Profile. If revisions to the full specifications or to the Base Profile
specification are required or beneficial to meet this requirement they should be
raised as early as possible with the steering committee.

## Dependencies & Related Projects

A related workstream is to specify entry point functions including runtime
initialization and finalization in the QIR specification. Any rules for entry
points defined as part of this profile should be compliant with that
specification. The specification of an Adaptive Profile should also naturally
extend the Base Profile specification that has already been defined.

## Deliverable(s) & Expected Outcome

The expected outcome is a document that clearly defines an Adaptive Profile
meeting the requirements outlined [above](#requirements). The intent is for the
Adaptive Profile to permit expressing quantum programs that contain classical
computations with certain data types and non-trivial control flow structures. It
will limit expressiveness to guarantee that the program always terminates (no
unbounded loops or recursions). This specification will replace what is
currently drafted as [Profile
B](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/7_Profiles.md#profile-a-basic-quantum-functionality)
on the [specification repository](https://github.com/qir-alliance/qir-spec).

Like the Base Profile, the Adaptive Profile should not rely on any particular
quantum instruction(s) being available. To target a quantum program to a
specific backend requires selecting a suitable profile and a compatible quantum
instruction set. The profile and the quantum instruction set (QIS) selection
together determine how the program IR should be represented.

A similar specification for the Base Profile can be found
[here](https://github.com/qir-alliance/qir-spec/blob/main/specification/under_development/profiles/Base_Profile.md).
The specification of the Adaptive Profile should follow a similar outline for
the sake of consistency and comprehensiveness of the specification.

## Future Work (out of scope for the Adaptive Profile)

The following features will not be supported in programs that are compliant with
the Base Profile:

- Composite data types: <br/>
  The use of composite data types such as [structure
  types](https://llvm.org/doxygen/group__LLVMCCoreTypeStruct.html) including
  [tuples](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/1_Data_Types.md#tuples-and-user-defined-types),
  and [sequential
  types](https://llvm.org/doxygen/group__LLVMCCoreTypeSequential.html) including
  [arrays](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/1_Data_Types.md#arrays)
  is not supported within an Adaptive Profile. This also precludes the use of
  such data structures for [callable
  values](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/2_Callables.md);
  i.e., the usage of subroutines as first class values is not supported within
  the Base Profile, and the use of [function
  types](https://llvm.org/doxygen/group__LLVMCCoreTypeFunction.html) is limited
  to globally declared LLVM functions that may be called as part of program
  execution.

- Unbounded loops or recursions: <br/>
  The Adaptive Profile should require that any profile compliant program is
  known to terminate; it must be possible to statically bind resources and
  schedule QPU instructions. Supporting direct or indirect function recursions
  is out of scope for the Adaptive Profile.

- Dynamic qubit allocations and access: <br/>
  Within the Base Profile, all qubit uses refer directly to a unique qubit id
  (requires an update of the full specification as part of this workstream).
  Runtime functions for qubit allocation/release are not available, and the lack
  of support for local variables and composite data types prevents any qubit
  aliasing. Prohibiting classical computations and branching based on
  measurement results furthermore precludes any dynamic qubit access.

Additional profiles to support one or more of these features will be defined as
part of future workstreams.

## Working Group & Getting Involved

Working group participants: TBD <br/>
Working group chair: Bettina Heim

If you would like to contribute to the workstream, please contact
[qiralliance@mail.com](mailto:qiralliance@mail.com).

## Schedule

Launch date: December 2022 <br/>
Estimated end date: February 2023 <br/>
Meeting schedule and/or channel(s) of communication: TBD

## Status & Discussions

Current status: This workstream waiting for approval by the steering committee.

The work and status will be tracked in the form of a GitHub issue on the
[specification repository](https://github.com/qir-alliance/qir-spec) once the
workstream has been approved. We encourage comments, inputs, and discussions on
that issue.

## Open Questions (to be answered as part of the workstream)

The following topics should be fleshed out as part of this workstream, and the
decisions should be captured in an appropriate part of the specification:

- command line parameters ...
- definition and use of local variables (storing or processing classical values)
  ...
- restrictions for control flow statements ...
- requirement of detecting over-/underflow ...
- Computations involving floating point data types: <br/>
  ... (constants are ok, but cannot be assigned to local variable)
- structuring code into multiple functions
- Since we ask for validation, we might investigate what properties can be checked by existing static analysis tools, so to make "reasonable" more precise.

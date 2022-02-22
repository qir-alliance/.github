# Workstream: Base-Profile Definition

## Motivation & Benefits

A profile of a specification is a subset of the specification that defines a
coherent set of functionalities and capabilities that might be offered by a
system. Defining profiles allows a specification to be forward-looking and
expansive without requiring implementations to support the full specification.
Profiles also provide a roadmap for implementors by specifying stages they can
progress through that will be useful to consumers of the specification.

## Requirements

The Base Profile should specify the minimal requirements to support defining and
executing quantum programs. In addition to a set of LLVM instructions, the Base
Profile may rely on a quantum instruction set define separately, but should not
make use of any runtime functions listed in the QIR specification.

The profile should specify all permitted LLVM instructions, and define all
required constructs for the program to be valid and executable on targeted
backends. This includes any attributes or other conventions to mark the entry
point, and additional information required for execution, such as e.g. the
number of qubits used by the program, if necessary. It should also define how to
specify the program output.

The defined requirements should permit to implement a validation tool that
guarantees that if the bitcode passes validation, it will be executed
successfully on any targeted backend that support Base Profile compliant
programs.

Any Base Profile compliant program should also be compliant with the QIR
specification and future profiles defined to permit for more advanced
capabilities such as, e.g., branching based on measurement results and classical
computations. If revisions to the full specifications are required or beneficial
to meet this requirement they should be raised as early as possible with the
steering committee.

## Dependencies & Related Projects

A related workstream is to specify entry point functions including runtime
initialization and finalization in the QIR specification. Any rules for entry
points defined as part of this profile should be compliant with that
specification.

## Deliverable(s) & Expected Outcome

The expected outcome is a document that clearly defines a Base Profile meeting
the requirements outlined [above](#requirements). The intent is for the Base
Profile to permit expressing quantum programs that contain no control flow or
classical computations during execution. This specification will replace what is
currently drafted as [Profile
A](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/7_Profiles.md#profile-a-basic-quantum-functionality)
on the [specification repository](https://github.com/qir-alliance/qir-spec).

In addition to the Base Profile itself, one or more quantum instruction set(s)
should be defined to provide the means to manipulate the quantum state. The
quantum instruction set(s) specified as part of this workstream should meet the
requirements specified by the Base Profile. Conversely, the Base Profile should
not rely on any particular quantum instruction(s) being available.

To targeted a quantum program to a specific backend requires selecting a
suitable profile and a compatible quantum instruction set. The profile and the
quantum instruction set (QIS) selection together fully determine how the program
IR should be represented. In addition to defining the Base Profile itself and at
least one compatible QIS, this workstream will also add a section to the
specification that contains guidance for defining and documenting addition
quantum instruction sets going forward.

A template for a specification definition can be found
[here](https://github.com/CommunitySpecification/1.0/blob/master/7._CS_Template.md).
This may serve as inspiration but it is not required to follow the template
precisely.

## Future Work (out of scope for the Base Profile)

Additional profiles will be defined by extending the Base Profile with
additional instructions and required/supported runtime functions. The following
features will not be supported in programs that are compliant with the Base
Profile:

- Branching based on measurement results: <br/>
  For a Base Profile compliant program, the performed computations
  (instructions) must not depend on measurement outcomes, i.e. the instruction
  sequence is fully determined at compile time. See also the section on [open
  questions](#open-questions) that are to be answered as part of this
  workstream.

- Use of local variables and command line parameters: <br/>
  For a Base Profile compliant program, all parameters must be known at compile
  time, and measurement results are the only non-constant values in the program.
  See also [open questions](#open-questions) around handling of measurement
  results that are to be answered as part of this workstream.

- Composite data types: <br/>
  The use of composite data types such as [structure
  types](https://llvm.org/doxygen/group__LLVMCCoreTypeStruct.html) including
  [tuples](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/1_Data_Types.md#tuples-and-user-defined-types),
  and [sequential
  types](https://llvm.org/doxygen/group__LLVMCCoreTypeSequential.html) including
  [arrays](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/1_Data_Types.md#arrays)
  is not supported within a Base Profile compliant program. This also precludes
  the use of such data structures for [callable
  values](https://github.com/qir-alliance/qir-spec/blob/main/specification/v0.1/2_Callables.md);
  i.e., the usage of subroutines as first class values is not supported within
  the Base Profile, and the use of [function
  types](https://llvm.org/doxygen/group__LLVMCCoreTypeFunction.html) is limited
  to globally declared LLVM functions that may be called as part of program
  execution.

- Classical computations during quantum execution: <br/>
  Execution of a Base Profile compliant quantum programs should not require
  storing or processing classical values beyond storing and retrieving
  measurement results. Constant values of simple data types, such as for example
  integers or floating points, may be used as arguments in QIS calls if the
  chosen QIS contains functions that make use of such types. A common example
  are single-qubit rotations, that are supported directly by various QPUs and
  require passing in a rotation angle as argument.

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

Launch date: February 2022 <br/>
Estimated end date: end of March / early April 2022 <br/>
Meeting schedule and/or channel(s) of communication: TBD

## Status & Discussions

Current status: This workstream has been approved by the steering committee.

The work and status is tracked in the form of a [GitHub
issue](https://github.com/qir-alliance/qir-spec/issues/7) on the [specification
repository](https://github.com/qir-alliance/qir-spec). We encourage comments,
inputs, and discussions on that issue.

## Open Questions (to be answered as part of the workstream)

The following topics should be fleshed out as part of this workstream, and the
decisions should be captured in an appropriate part of the specification:

- Qubit (re-)use: <br/>
  This workstream will define whether for a Base Profile compliant program
  qubits may be used after measuring their state. The specification should also
  capture what guarantees the backend should give around qubit use, such as,
  e.g., whether qubits with a certain id will necessarily always be mapped to
  the same device qubits, and whether qubits can be measured repeatedly. The
  specification should also give recommendations for resetting the state of
  qubits if necessary.

- Measurements: <br/>
  The Base Profile specification should define whether measurements may occur at
  any point in the program or only at the end. How to store and retrieve
  measurement results, as well as any related restrictions, will also be defined
  as part of this workstream. This in particular also includes defining whether
  any subset of qubits can be measured.

- Base Profile compliant QIS: <br/>
  Any restrictions and requirements for a QIS to be used in combination with a
  Base Profile compliant program need to be clarified, such as, e.g., whether
  the QIS may contain instruction that return values. The workstream should also
  clarify whether a valid QIS is expected to be universal in the quantum sense,
  and whether there should always exist a mapping from one QIS to another.

- Dynamic linking and symbol resolution: <br/>
  Related to the questions around how to define and specify a QIS,
  considerations around the the linking stage should be captures. In particular,
  the specification should give guidance about whether supporting libraries
  and/or the QIS may be linked before or after compilation into a Base Profile,
  as well as capture how to symbols are resolved during this stage.

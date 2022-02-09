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
executing quantum programs for gate-based quantum processors. In addition to a
set of LLVM instructions, the Base Profile may rely on a quantum instruction set
define separately, but should not make use of any runtime functions listed in
the QIR specification.

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
should be defined to provide the means to manipulate the quantum state, and at
least one defined quantum instruction set should permit universal quantum
computations. The quantum instruction set(s) specified as part of this
workstream should meet the requirements specified by the Base Profile.
Conversely, the Base Profile should not rely on any particular quantum
instruction(s) being available.

A template for a specification definition can be found
[here](https://github.com/CommunitySpecification/1.0/blob/master/7._CS_Template.md).
This may serve as inspiration but it is not required to follow the template
precisely.

## Future Work (Out of Scope)

Additional profiles will be defined by extending the Base Profile with
additional instructions and required runtime functions. The following features
are explicitly out of scope for the Base Profile:

- mid-circuit measurements
- classical computations during quantum execution
- use of local variables and command line parameters
- dynamic qubit allocations

Suitable profiles to support for one or more of these features will be defined
as part of future workstreams.

## Working Group & Getting Involved

Working group participants: <br/>
Working group chair:

If you would like to contribute to the workstream, please contact
[qiralliance@mail.com](mailto:qiralliance@mail.com).

## Schedule

Launch date: <br/>
Estimated end date: <br/>
Meeting schedule and/or channel(s) of communication:

## Status & Discussions

Current status: Workstream to be approved by steering committee

The work and status will be tracked in the form of a [GitHub
issue](https://github.com/qir-alliance/qir-spec/issues) on the [specification
repository](https://github.com/qir-alliance/qir-spec). We encourage comments,
inputs, and discussions on that issue.

The GitHub issue with be tagged appropriately after approval by the steering
committee.

## Open Questions

Should the profile allow to use constant values as arguments to quantum
instructions? <br/>
What are the rules for using constants as part of the program? <br/>
Should any quantum instruction set be valid for use with the Base Profile?
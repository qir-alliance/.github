# Workstream: Runtime Initialization, Finalization, and Entry-Point Handling

## Motivation & Benefits

QIR implementation libraries provided at link time may need to rely on library
start-up and finalization routines in order to properly configure and tear-down
an underlying simulation and / or remote job submission infrastructure. QIR for
native code-generation or as an exchange format with control systems may also
require some notion of start-up, initialization, and tear-down.

Runtime initialization raises the question of how QIR lowering strategies
should specify entry point functions and corresponding input data provided
at runtime. For runtime library linking, the notion of input `argc` and
`argv` can be a valuable asset to designing dynamic and flexible QIR
runtimes. For QIR as a format for backend submission, the specification
needs to carefully define what an entrypoint function is and how packaged
runtime arguments (command line or otherwise) can be injected into the
entrypoint at executable start-up.

## Requirements

The specification should define runtime initialization as a set of overloaded
functions with a prescribed function name. The functions differ by argument
structure, can take the usual `(int, int8_t**)`, no arguments to indicate
default initialization, or any other pertinent structure this proposed
workstream decides on.

The specification should define a finalization function declaration that
takes no arguments and is responsible for freeing all leveraged classical
and quantum resources at program exit.

For the case of runtime library linking, initialization and finalization may
also be required of quantum functions that are invoked from host code. Library
implementors may require the declaration of fine-grained function
initialization and finalization routines that QIR generators may insert at
the beginning of and end of these quantum function calls invoked from host
call-sites. The utility of this type of function-level functionality in the
support of near-term remote job submission and flushing internal quantum
instruction queues, as well as general callbacks for library runtime
event systems.

This workstream will define how QIR generators should mark a function as
EntryPoint. QIR generators can mark **exactly one** function as `EntryPoint`
via an LLVM attribute. The function can be described with any valid function
name. If there aren't any functions marked as `EntryPoint` then a `main`
function must be present to enable execution. For custom `EntryPoint`
functions, an appropriate LLVM Pass must be applied to introduce a `__start`
or `__main` function that calls the original entry point function. The
workstream should also take into account the validity of return types
for a custom `EntryPoint`. Likely, the return type should model some return
status code (e.g. with an integer). This should be discussed in the
workstream. The return of quantum execution results should be left as a
topic for future workstreams.

The utility of QIR code that lacks an `EntryPoint` function or `main` lies
in its lowering to object code and archival into static or shared libraries.
QIR can omit `main` or `EntryPoint` and can thereby enable a modular approach
for the construction of quantum-classical applications. We leave this concept
(modular QIR) for future workstreams, but the work done here should directly
enable these modular capabilities.

Use cases may exist whereby QIR code is generated with a custom EntryPoint and
needs to be executed with custom command line arguments that should serve as
input to that EntryPoint function. The specification needs to define some
specified way to map custom command line arguments of a general type to the
input arguments of the function, as well as the introduction of a `main`
function for the underlying C runtime to pick up for execution.

## Dependencies & Related Projects

A related workstream is to specify a base profile of the full specification.
This work should ensure that future base profile work is also compliant with
entrypoint definitions and runtime input, finalization, and parameterization.

## Deliverable(s) & Expected Outcome

The expected outcome of this workstream is an update to the existing QIR
specification documentation that defines specific function declarations
for program-level initialization and finalization, function-level
initialization and finalization for quantum functions invoked from host
call sites, and entry-point marker metadata and runtime parameter input.

## Future Work (Out of Scope)

This work will not define specific initialization or finalization tasks
that a QIR implementation library should perform. This work will not study
the return of quantum execution results by `EntryPoint` functions.

## Working Group & Getting Involved

Working group participants: TBD <br/>
Working group chair: Alex McCaskey

If you would like to contribute to the workstream, please contact
[qiralliance@mail.com](mailto:qiralliance@mail.com) and / or
[Alex McCaskey](mailto:amccaskey@nvidia.com).

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

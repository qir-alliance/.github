# Workstream: Runtime Initialization, Finalization, and Entry-Point Handling

## Motivation & Benefits

QIR implementation libraries provided at link time may need to rely on library 
start-up and finalization routines in order to properly configure and tear-down 
an underlying simulation and / or remote job submission infrastructure. Runtime 
initialization also raises the question of how QIR lowering strategies should 
specify entry point functions and corresponding input data provided at runtime.

## Requirements

The specification should define runtime initialization as a set of overloaded 
functions with prescribed function name. The functions differ by argument structure, 
can take the usual `(int, int8_t**)` or no arguments to indicate default initialization. 

The specification should define a finalization function declaration that takes no 
arguments and is responsible for freeing all leveraged classical and quantum resources 
at program exit. 

Initialization and finalization may also be required of quantum functions that are 
invoked from host code. We require the declaration of function initialization and 
finalization routines that QIR generators may insert at the beginning of and end 
of these host-call-site quantum function calls. Note the utility of this type of function-level 
functionality in the support of near-term remote job submission and flushing internal 
quantum instruction queues. 

QIR generators can mark one function as `EntryPoint` via an LLVM attribute. The 
function can be described with any valid function name. If the name is not `main`, 
then an appropriate LLVM Pass must be applied to introduce a `__start` or `__main` 
function that calls the original entry point function. 

Use cases may exist whereby QIR code is generated with a custom EntryPoint and 
needs to be executed with custom command line arguments that should serve as input 
to that EntryPoint function. There needs to be some specified way to map custom 
command line arguments of a general type to the input arguments of the function 
as well as the introduction of a `main` function for the underlying C runtime 
to pick up for execution. 

## Dependencies & Related Projects

A related workstream is to specify a base profile of the full specification. This 
work should ensure that future base profile work is also compliant. 

## Deliverable(s) & Expected Outcome

The expected outcome of this workstream is an update to the existing QIR specification 
documentation that defines specific function declarations for program-level initialization 
and finalization, function-level initialization and finalization for quantum functions 
invoked from host call sites, and entry-point marker metadata and runtime parameter 
input. 

## Future Work (Out of Scope)

This work will not define specific initialization or finalization tasks that 
a QIR implementation library should perform. This may be required in the future 
but we will not handle it with this workstream. 

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


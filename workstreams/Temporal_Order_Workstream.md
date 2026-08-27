# Workstream: Quantum Gate Execution Temporal Order

## Motivation & Benefits

Currently, QIR specification does not explicitly contain
the information regarding the time-order of quantum instruction execution.
Specifically, the default behavior for executing QIR on quantum backends
is to execute the quantum instructions sequentially in the order they are
laid out within code blocks which themselves are sequentially linked
through the branching terminator statement (`br`) of each code block
until the last code block with a terminator `ret`. This is however,
in general, inefficient for wide quantum circuits. Additional time
overhead degrades the overall quantum circuit fidelity due to finite
coherence time of physical qubits. Including explicit time ordering
information within QIR would allow the development of algorithmic temporal
execution order optimization routines leading to backend optimized QIR with
a combination of sequential and parallel quantum instructions. The
optimization routines for backends with varying times to complete different
physical quantum instructions could be developed with appropriate contraints
abstracted from the relative physical lengths of quantum instructions for
backends. We note that quantum instructions could be but not limited to
quantum gates, measurement operations, and classical computing
(in the case of adaptive profile).

We further note that the notion of clock and temporal optimization for runtime
instruction execution are common and critical in both classical and quanutm
computing systems at a low-level where hardware resources and speed in the
physical layer are finite. Even though future FTQC hardware may be less
sensitive to such optimization, its underlying error-correction routines
would still benefit greatly with improved logical quantum operation
speed and optimal overhead.

## Requirements

The Temporal Order should specify the relative order at which the quantum
instructions are executed on a given backend. In addition to the sequential
execution of quantum instructions, QIR could group together instructions
that can be executed in a time interval. Specifically, we propose to
reuse the current QIR code block structure to contain instructions
that can be executed with a synchroinzed begining and finished before
the block terminator. The block terminator statement will be executed
after all in-block instructions before it are finished. The branching
terminator statement (`br`) will instruct transition to the next QIR
code block representing the next group of instructions that can be executed
within another time interval. In the case where quantum instructions within
a block take a similar amount of time to finish, this would be sufficient
to allow quantum circuit optimizers to use a QIR code block for grouping
quantum instructions that can be executed in parallel and synchronized at
the beginning and finished before the terminator statement of the block.
The runtime efficiency is improved as compared to the simple sequential
execution of instructions. To inform the backend that the QIR codes are
structured with temporal order allowing for parallel execution of instructions,
the QIR code block should have a new attribute `time-order` with value
`parallel`. In cases where we want to have the instructions in a block to be
executed sequentially by the backend,
`time-order` should have a value `sequential`.

The execution efficiency could be even further improved if quantum instructions
that could be executed in parallel have fairly different physical lengths.
For example, a measurement pulse on a superconducting qubit typically takes
more than 300 ns while the qubit gates for the same backend could take less
than 30 ns. This large execution time difference could mean that further
temporal order optimization is possible. For example, the measurement process
could be executed on a qubit while multiple sequential rounds of (parallel)
fast quantum operations are applied to other unrelated qubits. This
necessitates a new type of quantum instruction starting with the keyword
`sync`. This quantum instruction will signal the backend to stop real-time
execution of new commands following it within the current QIR code block until
a prior quantum instruction with an index (`cmd_id`) is finished. A complete
`sync` quantum instruction statement could be written as `sync cmd_id`.
If we need to stop the execution until multiple prior quantum instructions are
finished, we could have consecutive lines of `sync cmd_id` corresponding to
different quantum instructions before them respectively. We note that `cmd_id`
defined here is following the order of instructions as written in the current
QIR block starting with 0 for the first quantum instruction. Note that
`sync cmd_id`, as a valid quantum instruction, will also have its own `cmd_id`
for its position in the block. A QIR implementation with an optimizer for
temporal order of instruciton execution should find an optimal way to place
quantum instructions including `sync` within a QIR code block and sequentially
link the QIR code blocks through terminators to achieve the optimal temporal
runtime efficiency.

## Dependencies & Related Projects

The specification of this Temporal Order should naturally
extend the Base Profile and Adaptive Profile specification
that have already been defined.

## Deliverable(s) & Expected Outcome

The expected outcome of this workstream is an update to the existing QIR
specification documentation meeting the requirements outlined [above]
(#requirements) allowing temporal order of quanutm instructions to be
explicitely represented. In addition to the update to QIR specifications,
the available quantum instruction set should include the `sync` quantum
instruction that enforces in-order sequential execution of parts of the
instructions within a code block.

## Future Work (Out of Scope)

This work will not define specific temporal order optimization tasks that a QIR
implementation library should perform with backends' constraints
on the relative physical processe lengths between quantum instructions.

One potential future update to the specification will be including the
information on the maximum number of parallel quantum instruction executions
assumed by the QIR implementation's runtime optimizer for a target backend.
This will inform the backend to allocate a compatible amount of real-time
parallel instruction execution threads for achieving a consistent optimal
performance. The update could be implemented in the specification to allow
`time-order` to take integer values with `time-order = 1` corresponding to
pure sequential execution and `time-order = <N>` corresponding to requiring
at most `N` parallel instruction execution threads in the backend.

## Working Group & Getting Involved

Members: TBD <br/>
Chair: Jie(Roger) Luo

If you would like to contribute to the workstream, please contact
[qiralliance@mail.com](mailto:qiralliance@mail.com) and / or
[Jie(Roger) Luo](mailto:jie.roger.luo@gmail.com).

## Schedule

Launch date: Oct. 2024 <br/>
Estimated end date: TBD<br/>
Meeting schedule and/or channel(s) of communication: TBD

## Status & Discussions

Current status: Pending approval

The work and status is going to be tracked in the form of a
GitHub issue after approval.
<br/>
We encourage comments, inputs, and discussions on that issue.

The GitHub issue is labeled as `Approved` after approval by the steering
committee.

## Open Questions

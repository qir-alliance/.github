# Steering Committee Meeting April 2023

Attendance: Alex Chernoguzov, Alex McCaskey, Bettina Heim,
Bill Ticehurst, Kalan Snyder, Sonia Pignorel, Wim Lavrijsen

## Meeting agenda

- Recap and status
- Opaque pointers
- Adaptive profile workstream
- Runtime initialization workstream
- QIR Community calls
- Next steps

## Recap and status

- This month's discussion was centred around the opaque pointer _ptr_
introduced in LLVM 15 to mitigate issues with explicit pointee types _i64*_.
Typed pointers are still supported in LLVM 16 but as best effort and
are no longer supported in LLVM 17.
- The value of opaque pointer for the Qubit needs to be clarified.
Numbers such as the 64-bit integer should be acceptable for the near future
to represent Qubits. QIR will stay compatible with LLVM 16 for the next few
years. If we know we won't need dereferencing, there is no need for opaque
pointers.
- The cleanest would be for the bitcode to have some information about the
Qubit representation. It gives the frontend the option to emit the version they
want. For the backend, it would be additional code.
- For array, it is acceptable to continue with the lack of typing.
- For Qubit, it is acceptable to say that compiler code will never do anything
with the content of the Qubit up to the execution.
- For measurement results, it is more complicated on whether it is a value or
placeholder that can be called. There is a distinction between the actual
measurement done on qpu and the readout of a measurement not done on a qpu per
se. That could be an opaque structure and worth experimenting with.

## Follow-ups / Action items

- Put together a PR for a new workstream to define a Qudit type (and the
measurements result type).
- Send a list of possible interested parties for QIR community call
presentations.
- Next month's topic will be the conclusion of the Runtime initialization
and finalization workstream.

# Green Thread Scheduler (riscv64)

In this exercise, you build a simple cooperative (green) thread scheduler on top of context switching.
This crate is **riscv64 only**; run with the repo's normal flow (`./check.sh` / `oscamp`) or natively on riscv64.

## Key Concepts

- Cooperative vs preemptive scheduling
- Thread state: `Ready`, `Running`, `Finished`
- `yield_now()`: current thread voluntarily gives up the CPU
- Scheduler loop: pick next ready thread and switch to it

## Design

Each green thread has its own stack and `TaskContext`. Threads call `yield_now()` to yield.
The scheduler round-robins among ready threads. User entry is wrapped by `thread_wrapper`, which
calls the entry then marks the thread `Finished` and switches back.

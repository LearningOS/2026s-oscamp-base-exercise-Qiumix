# Stackful Coroutine and Context Switch (riscv64)

In this exercise, you implement the minimal context switch using inline assembly,
which is the core mechanism of OS thread scheduling. This crate is **riscv64 only**;
run `cargo test` on riscv64 Linux, or use the repo's normal flow (`./check.sh` / `oscamp`) on x86 with QEMU.

## Key Concepts

- **Callee-saved registers**: Save and restore them on switch so the switched-away task can resume correctly later.
- **Stack pointer `sp`** and **return address `ra`**: Restore them in the new context; the first time we switch to a task, `ret` jumps to `ra` (the entry point).
- Inline assembly: `core::arch::asm!`

## riscv64 ABI (for this exercise)

- Callee-saved: `sp`, `ra`, `s0`–`s11`. The `ret` instruction is `jalr zero, 0(ra)`.
- First and second arguments: `a0` (old context), `a1` (new context).

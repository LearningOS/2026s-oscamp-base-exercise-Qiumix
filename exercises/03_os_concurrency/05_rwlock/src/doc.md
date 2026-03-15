# Read-Write Lock (Writer-Priority)

In this exercise, you will implement a **writer-priority** read-write lock from scratch using atomics.
Multiple readers may hold the lock concurrently; a writer holds it exclusively.

**Note:** Rust's standard library already provides [`std::sync::RwLock`]. This exercise implements
a minimal version for learning the protocol and policy without using the standard one.

## Common policies for read-write locks

Different implementations can give different **priority** when both readers and writers are waiting:

- **Reader-priority (读者优先)**: New readers are allowed to enter while a writer is waiting, so writers
  may be starved if readers keep arriving.
- **Writer-priority (写者优先)**: Once a writer is waiting, no new readers are admitted until that writer
  has run; [this exercise implements this policy].
- **Read-write fair (读写公平)**: Requests are served in a fair order (e.g. FIFO or round-robin), so
  neither readers nor writers are systematically starved.

## Key Concepts

- **Readers**: share access; many threads can hold a read lock at once.
- **Writer**: exclusive access; only one writer, and no readers while the writer holds the lock.
- **Writer-priority (this implementation)**: when at least one writer is waiting, new readers block
  until the writer runs.

## State (single atomic)

We use one `AtomicU32`: low bits = reader count, two flags = writer holding / writer waiting.
All logic is implemented with compare_exchange and load/store; no use of `std::sync::RwLock`.

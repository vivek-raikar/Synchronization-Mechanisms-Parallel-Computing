\# Synchronization Mechanisms in Parallel Programs



\## Overview



This experiment studies synchronization mechanisms used in shared-memory parallel programming. It demonstrates how multiple threads access shared data, how race conditions occur, and how synchronization techniques improve correctness.



The experiment compares execution time, correctness, and scalability using OpenMP and POSIX threads in C.



\## Objectives



\- Understand race conditions in shared-memory programs.

\- Implement critical sections and atomic operations.

\- Demonstrate thread synchronization using barriers.

\- Implement mutual exclusion using semaphores.

\- Compare execution time and correctness across different thread counts.

\- Study the performance trade-offs of synchronization mechanisms.



\## Technologies Used



\- C programming language

\- Ubuntu 22.04 LTS

\- GCC compiler

\- OpenMP

\- POSIX threads (pthreads)

\- POSIX semaphores

\- VMware Workstation Pro



\## Project Structure



```text

Synchronization-Mechanisms-Parallel-Computing/

├── src/

│   ├── race.c

│   ├── critical.c

│   ├── atomic.c

│   ├── barrier.c

│   ├── semaphore.c

│   └── compare\_sync.c

├── results/

│   ├── benchmark-results.txt

│   └── screenshots/

│       └── sync-experiment-results.jpeg

└── README.md

```



\## Synchronization Mechanisms



| Mechanism | Description |

|---|---|

| Race condition | Demonstrates shared-counter updates without synchronization. |

| Critical section | Protects a shared update by allowing one thread at a time. |

| Atomic operation | Performs a shared-counter update atomically. |

| Barrier | Makes threads wait until all participating threads reach a synchronization point. |

| Semaphore | Uses a semaphore to protect access to a shared counter. |

| Comparison benchmark | Compares unsynchronized, critical, atomic, and lock-based counter updates. |



\## Installation



Install GCC and the required development tools on Ubuntu:



```bash

sudo apt update

sudo apt install build-essential -y

```



Check compiler availability:



```bash

gcc --version

```



\## Compilation Commands



Run these commands from the directory containing the source files:



```bash

gcc src/race.c -fopenmp -o race

gcc src/critical.c -fopenmp -o critical

gcc src/atomic.c -fopenmp -o atomic

gcc src/barrier.c -fopenmp -o barrier

gcc src/semaphore.c -pthread -o semaphore

gcc src/compare\_sync.c -fopenmp -o compare\_sync

```



These commands compile the programs. The recorded experiment results below come from the original college-PC execution.



\## Benchmark Configuration



\- Shared-counter workload: 10,000,000 increments

\- Thread counts: 1, 2, 4, and 8

\- Timing function: `omp\_get\_wtime()`

\- Correctness check: final counter compared with the expected count



\## Recorded Results



The following measurements were recorded during execution on the college PC using Ubuntu in VMware.



| Threads | Mechanism | Final Count | Correctness | Time (s) |

|---:|---|---:|---|---:|

| 1 | None | 10,000,000 | Correct | 0.0069 |

| 1 | Critical | 10,000,000 | Correct | 0.1283 |

| 1 | Atomic | 10,000,000 | Correct | 0.0693 |

| 1 | Lock | 10,000,000 | Correct | 0.1163 |

| 2 | None | 5,220,657 | Incorrect | 0.0133 |

| 2 | Critical | 10,000,000 | Correct | 0.2595 |

| 2 | Atomic | 10,000,000 | Correct | 0.1484 |

| 2 | Lock | 10,000,000 | Correct | 0.4650 |

| 4 | None | 7,279,449 | Incorrect | 0.0086 |

| 4 | Critical | 10,000,000 | Correct | 0.3339 |

| 4 | Atomic | 10,000,000 | Correct | 0.1624 |

| 4 | Lock | 10,000,000 | Correct | 0.4867 |

| 8 | None | 2,469,491 | Incorrect | 0.0103 |

| 8 | Critical | 10,000,000 | Correct | 0.3369 |

| 8 | Atomic | 10,000,000 | Correct | 0.1757 |

| 8 | Lock | 10,000,000 | Correct | 0.4856 |



See \[`results/benchmark-results.txt`](results/benchmark-results.txt) for the recorded results and \[`results/screenshots/sync-experiment-results.jpeg`](results/screenshots/sync-experiment-results.jpeg) for the execution screenshot.



\## Observations



1\. \*\*Race condition:\*\* The unsynchronized shared-counter update produced incorrect results with multiple threads because updates were lost.

2\. \*\*Critical section:\*\* All updates were correct, but execution time increased as thread contention grew.

3\. \*\*Atomic operation:\*\* All updates were correct, and atomic operations were faster than critical sections and locks in the recorded runs.

4\. \*\*Lock:\*\* All updates were correct, but lock acquisition and release added overhead.

5\. \*\*Scalability:\*\* Increasing the thread count did not necessarily improve execution time because synchronization and contention introduced overhead.



The barrier and semaphore programs demonstrate additional synchronization techniques but are not included in the four-mechanism timing comparison.



\## Conclusion



This experiment demonstrates that synchronization is essential for maintaining correctness in shared-memory parallel programs. Unsynchronized updates may execute quickly but can produce incorrect results. Critical sections, atomic operations, and locks protect shared data, with different performance costs.



In the recorded benchmark, atomic operations provided a good balance of correctness and execution time for a simple shared-counter update. The best synchronization mechanism depends on the operation being protected, the workload, and the level of thread contention.



\## Notes



\- Execution times are specific to the recorded environment and may vary across machines and virtual-machine configurations.

\- The benchmark results are historical measurements from the college PC; they were not regenerated on the repository machine.

\- This project is intended for educational study of parallel programming and synchronization.




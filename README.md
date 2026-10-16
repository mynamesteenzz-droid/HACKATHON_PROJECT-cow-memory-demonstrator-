# cow-memory-demonstrator
A Linux C demonstration of fork() and Copy-on-Write memory behavior.
cd /root/cow-memory-demonstrator

cat > README.md <<'EOF'
# Copy-on-Write Memory Demonstrator

## Problem Statement
Demonstrate how memory is shared after fork() and copied when a process modifies it.

## Objective
Show Copy-on-Write (COW) behavior and parent-child process memory isolation using C on Linux.

## Technologies
- C
- Linux
- GCC
- mmap(), fork(), waitpid(), getrusage()

## How It Works
1. Allocate 16 MiB of private anonymous memory.
2. Initialize every memory page with the value 42.
3. Create a child process using fork().
4. The child changes one byte on every page to 99.
5. The parent waits and checks its original value.

## Compile and Run
    gcc -Wall -Wextra -O0 cow_demo.c -o cow_demo
    ./cow_demo

Or use make after configuring the Makefile.

## Test Results
- Memory allocated: 16 MiB
- Page size on the test system: 4096 bytes
- Pages initialized: 4096
- Child value after modification: 99
- Parent value after child exits: 42
- Parent data preserved: YES

Minor page-fault counts are supporting evidence of page-fault activity, not a direct measurement of the number of physical pages copied.

## Limitations
The program demonstrates parent-child memory isolation and behavior consistent with COW. It does not directly inspect physical memory mappings.

## Future Improvements
- Compare different memory sizes.
- Run repeated benchmarks.
- Visualize memory and page-fault results.
EOF

# Document Indexer

A low-level document indexing system built in C for the Operating Systems course at the University of Minho.

The system follows a client-server architecture where multiple clients can concurrently submit documents to be indexed and query the index by keyword. All communication between clients and the server is handled through **named pipes (FIFOs)**, with each client creating its own response pipe identified by its PID.

## Features
- Add, remove and search documents by keyword
- Binary file storage for the document index (`index.dat`)
- Multi-process server using `fork()` to handle requests concurrently, up to a configurable limit
- Persistent index that survives server restarts

## Supported Operations

| Flag | Description |
|------|-------------|
| `-a` | Add a document (title, author, path, year) |
| `-r` | Remove a document by ID |
| `-s` | Search documents by keyword |

## Tech Stack
C, POSIX, named pipes, fork, binary file I/O

## How to Run
```bash
make
./server &
./client -a "Title" "Author" 2024 "path/to/doc"
./client -s "keyword"
```

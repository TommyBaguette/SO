# Document Indexer

A low-level document indexing system built in C for the Operating Systems course at the University of Minho.

The system follows a client-server architecture where multiple clients can concurrently submit documents to be indexed and queried by keyword. All communication between clients and the server is handled through **named pipes (FIFOs)**, with each client creating its own response pipe identified by its PID.

## Features
- Add, consult, delete and search documents by keyword
- Parallel keyword search using a configurable number of child processes
- Binary file storage for the document index (`index.dat`)
- Multi-process server using `fork()` to handle requests concurrently, up to a configurable limit
- Persistent index that survives server restarts
- Graceful server shutdown via client command

## Supported Operations

| Flag | Arguments | Description |
|------|-----------|-------------|
| `-a` | `title author year path` | Add a new document to the index |
| `-c` | `id` | Consult a document by ID (returns title, author, year, path) |
| `-d` | `id` | Delete a document from the index by ID |
| `-l` | `id keyword` | Count occurrences of a keyword in a specific document |
| `-s` | `keyword [nr_processes]` | Search all documents for a keyword, optionally using multiple parallel processes |
| `-f` | — | Shut down the server gracefully |

## Tech Stack
C, POSIX, named pipes (FIFOs), fork, binary file I/O

## How to Run
```bash
make
./server &
./client -a "Title" "Author" 2024 "path/to/doc"
./client -c 1
./client -d 1
./client -l 1 "keyword"
./client -s "keyword" 4
./client -f
```

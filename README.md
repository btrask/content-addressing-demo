Content Addressing Demo
=======================

A simple content addressing system in under 100 lines of Python.

This is my first time using Python, so some parts may seem a bit weird. Feedback welcome.

Usage
-----

`hash-import /path/to/file`  
Hashes the file  
Creates a read-only copy  
Prints content address in various formats

`hash-lookup hash://sha256/...`  
Writes the file content to standard output

`hash-lookup --path hash://sha256/...`  
Prints the path to a read-only copy of the file

Files are stored in `~/.local/cas-demo`

FAQ
---

**If it's so easy, why did [StrongLink](https://github.com/btrask/stronglink) take you 3 years and 10,000 lines of code?**  
Because I wrote it in C.

And because the real system:

- Tracks file meta-data (including tags and full-text indexing)
- Has a way to find files/hashes without file or hash (search)
- Uses a database instead of hardlinks everywhere
- Supports hash algorithm plugins (not technically done yet)
- Supports more hash formats (short, base-64, etc.)
- Is ACID (and coordinates transactions between DB and file system)
- Supports multiple repos per user (at arbitrary paths)
- Handles hash collisions (aside from the primary hash)
- Has a basic user interface
- Has a sync protocol

For what it's worth, the first ~2 years were just prototyping. The C version was only started a little over a year ago.

Exercises for the reader
------------------------

- Optimize importing by only calling `mkdir(2)` if the directory doesn't already exist
- Ensure ACID by `fsync`ing the directories after their contents have been changed
- Support different hash lengths (12 bytes, 24 bytes and 32 bytes) and base-64 encoding
- Figure out how to resolve links when you click on them
	- On OS X, you might be able to use `LSSetDefaultHandlerForURLScheme`

.

License: MIT

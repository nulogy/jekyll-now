---
layout: post
title: "Non-Invasive Monitoring of Socket Traffic"
author: ryandevilla
date: 2016-12-16T20:36:13+00:00
---

# Problem

I would like to diagnose failures to communicate with an external service over a network socket, without making modifications to the code or otherwise disturbing a production-like environment.

# Solution

One writes to or reads from a socket by making a request to the kernel (a.k.a *syscall*). This requires the *file descriptor* (numerical identifier) of the socket and the message to be sent over the socket, or a buffer that will contain the next message read from the socket.

Using `strace` (or `dtruss` on MacOS), one can inspect the stream of *syscalls* issued to the kernel and the arguments for each *syscall*. First, find the ID of the process that will be communicating over the socket:

```
ryan@staging ~ $ ps ax | grep unicorn
99999 ?        Sl     0:00 unicorn worker[0]
```

Then attach to the process with `strace`:

```
ryan@staging ~ $ strace -p 99999
Process 99999 attached
[pid 99999] write(11, "Hello", 6) = 6
[pid 99999] read(11, 0xBAAAAAAD, 64) = -1 EAGAIN (Resource temporarily unavailable)
```

Here, a `Hello` message was sent with a `write` *syscall* over socket with file descriptor 11, though the `read` *syscall* failed as the socket was temporarily blocked.

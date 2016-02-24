# 5 Reasons Why Code Breaks (in JavaScript)

Sometimes, a simple typo can really be the root of all evil. But more often, the reason why code breaks is more complex. And yet, it can be avoided.

## Untested Code

- Changing code in one place all too often breaks code in a (seemingly) unrelated place.
- CI

## Poor Error Reporting
- Operational errors
  -  run-time problems experienced by correctly-written programs. These are not bugs in the program. In fact, these are usually problems with something else: the system itself (e.g., out of memory or too many open files), the system's configuration (e.g., no route to a remote host), the network (e.g., socket hang-up), or a remote service (e.g., a 500 error, failure to connect, or the like). Examples include:
    - failed to connect to server
    - failed to resolve hostname
    - invalid user input
    - request timeout
    - server returned a 500 response
    - socket hang-up
    - system is out of memory
- Programmer errors
    - bugs in the program. These are things that can always be avoided by changing the code. They can never be handled properly (since by definition the code in question is broken).
    - tried to read property of "undefined"
    - called an asynchronous function without a callback
    - passed a "string" where an object was expected
    - passed an object where an IP address string was expected

- You won't easily become aware of all your application's problems: some will only surface in very rare circumstances or with seldom used features
- People use the term "errors" to talk about both operational and programmer errors, but they're really quite different. Operational errors are error conditions that all correct programs must deal with, and as long as they're dealt with, they don't necessarily indicate a bug or even a serious problem. "File not found" is an operational error, but it doesn't necessarily mean anything's wrong. It might just mean the program has to create the file it's looking for first.
- This distinction is very important: operational errors are part of the normal operation of a program. Programmer errors are bugs.
- Sometimes, you have both operational and programming errors as part of the same root problem. If an HTTP server tries to use an undefined variable and crashes, that's a programmer error. Any clients with requests in flight at the time of the crash will see an ECONNRESET error, typically reported in Node as a "socket hang-up". For the client, that's a separate operational error. That's because a correct client must handle a server that crashes or a network that flakes out.
- Similarly, failure to handle an operational error is itself a programmer error. For example, if a program tries to connect to a server but it gets an ECONNREFUSED error, and it hasn't registered a handler for the socket's 'error' event, then the program will crash, and that's a programmer error. The connection failure is an operational error (since that's something any correct program can experience when the network or other components in the system have failed), but the failure to handle it is a programmer error.
- The distinction between operational errors and programmer errors is the foundation for figuring out how to deliver errors and how to handle them. Make sure you understand this before reading on.


## Over-Engineering
- Every piece of code solves a problem. And ideally, it should only solve a problem you have (or are very likely to have). Of course, an endless number of other problems can be imagined... but trying to solve them when you're not likely to actually have them will make your code more complex than necessary.
- [Over-Engineering](http://www.codesimplicity.com/post/what-is-overengineering/)


## Over-Dependent
- While external libraries can lighten your workload, they can (unfortunately) also bite you: when they introduce bugs, when they increase loading time, when their development is discontinued, when you simply have too many of them in your project to keep an overview...

## Maintenance
- Code rots. It's a sad but true fact. While some parts in a project change and evolve, others are left behind. These parts become liabilities over time. For example, because framework features became obsolete; or because the new code's demands aren't satisfied anymore.
- Refactor

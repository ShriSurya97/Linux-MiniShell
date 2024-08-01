# Linux-MiniShell
To Implement a minimalist shell, mini-shell (msh) as part of the Linux Internal module. 
The objective is to understand and use the system calls w.r.t process creation, signal handling,
 process synchronization, exit status, text parsing, etc.
What is a mini Linux shell?
A mini Linux shell is a program that behaves exactly like the Linux shell, albeit with limited functionality.

It supports built-in shell commands like "cd" and "exit".
It supports input and output redirection.
It supports the background process.
Tech stack
Since it's a Linux shell, the only feasible language to use was C; as it is native to Linux. Also, the POSIX library was required for the implementation of the shell.

The process of building the shell
It was difficult to think of where to start. I was dealing with the fork() function for the first time. fork() creates a child process that can run simultaneously with the parent process in the system. The child process can be given a different task to perform. In this case, the child process would execute the command typed by the user in the shell. So I started reading about fork(). I, of course, started with the man page for fork(). But that was not enough, so I read some articles that explained the usage of fork() with examples.

Now armed with that knowledge, I went ahead to find how the child process would execute the command entered by the user. Do I have to code for all the possible commands? Well, the answer was no. There's a really useful family of functions in Linux, viz. exec(). These functions help one to execute a command in Linux. So I read the man page for that and found out that the execvp() function is the best match for my code.

With that sorted out, the next was just logically coding the entire shell program, which turned out to be quite simple. You may find the entire code on Github here.

Challenges I faced
The hardest parts were understanding the usage of fork() and installing the signal handler.

The signal handler is required as this shell supports background processes. The child process that is sent to the background must signal the parent process once it's done with its execution. This can be done using the waitpid() function with the WNOHANG option. I had to read multiple articles on this topic to understand it properly.

Key learnings
The new things I learned

fork()
execvp()
Signal handling
Tips and advice
The best way to tackle a huge problem is to break it down into smaller parts and then attack one part at a time. I started with creating a child process and then moved on to executing the user command. After that was done, I implemented the support for the background process part.

Final thoughts and next steps
Projects like these might seem really difficult and one might think that the implementation might go completely over their heads (especially for newbies). But, that's no reason to give up. If one keeps trying to solve a problem like that, eventually one will get success and learn many new things on the way.

This project taught me a lot, but now it offers nothing more. So I won't be lingering on this any longer. Many more new fun projects await!

Linux

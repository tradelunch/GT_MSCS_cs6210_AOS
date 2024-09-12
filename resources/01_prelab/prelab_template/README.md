# Prelab: pthreads - user level threads

## Description

You are going to demonstrate your understanding of the semantics of an existing threads library (pthreads, to be exact) and how to use it.

Under this directory you will find a source (.c) file and a Makefile. (Although we're not asking you to modify the Makefile now, this would be a good opportunity to take a look and make sure you understand how it works, because you may need to modify Makefiles for later projects.) You can compile the source file with the command make and clean up the compiler output with make clean. The program should compile and run correctly on any Red Hat Enterprise Linux (RHEL) system or Ubuntu 18+.

The source code provided is a multi-threaded consumer-producer program. That means producer threads add items (in this case, a character) to a queue, and consumer threads remove the items from the queue and do something with them (in this case, print the character to standard output). The main thread spawns a consumer thread and 2 producer threads, then the producer threads also spawn a consumer thread. So in total there are 2 producer threads and 3 consumer threads (plus the main thread).

The program should have the consumers collectively print every letter of the alphabet exactly once for each producer, without crashing. You will find that it compiles correctly, but when you run the program there are several bugs.

For this pre-lab, you will be asked to do two things: **First, find and fix the five (5) bugs that have been placed in the source code.** (Some of these bugs will appear at runtime, but others may only be apparent by code inspection.) Putting comments near the bugs you found will also help us to grade your pre-lab. **Second, answer the questions below** (short answers, one or two sentences each). It may be convenient to make a copy of the original source file before you modify it, since the questions below include line numbers.

To find information about pthread functions, you may use the command `man [func name]` (e.g. man `pthread_create`).

Please note that all the bugs in the program pertain to the pthreads threading and mutual exclusion libraries in some way. There are not bugs pertaining to program semantics (except for the semantics of pthreads and mutexes), and the intended bugs are all things that are definitely wrong regardless of any common sense interpretation of the program's intended behavior. Also, all the string constants should be correct. If there is a mistake in a string constant, then that's my mistake and not one of the intended bugs. (You can still point it out, though, so we can fix it for next time.) These guidelines are meant to help, but if you find something that you're unsure about, you can ask the TA.

## Collaboration

Students are not allowed to collaborate on this assignment. Each student is expected to find the 5 bugs, fix them, and answer the questions on their own. (You may use reference material, however, to help you understand how pthreads work and the semantics of the function calls.)

## Questions
1. The main function contains calls to `exit()` (line 66) and `pthread_exit()` (line 80). How will the effect of these two calls differ when they are executed?
1. The main function calls `pthread_join()` (line 90) with the parameter `thread_return`. Where does the value stored in `thread_return` come from when the `consumer_thread` is joined?
1. Where does the value stored in `thread_return` come from if the joined thread terminated by calling `pthread_exit` instead of finishing normally?
1. On the same call to `pthread_join()` (line 90), what will it do if the thread being joined (`consumer_thread`, in this case) finishes before the main thread reaches the that line of code (line 90)?
1. In this program, the main thread calls `pthread_join()` on the threads it created. Could a different thread call `pthread_join()` on those threads instead? Could a thread call `pthread_join()` on the main thread (assuming it knew the main thread's thread ID - i.e. `pthread_t`)?
1. The `consumer_routine` function calls `sched_yield()` (line 194) when there are no items in the queue. Why does it call `sched_yield()` instead of just continuing to check the queue for an item until one arrives?

## Deliverables

Submit the following on Gradescope:

- PDF file containing the answers to the above questions.
- Your modified source file (`producer_consumer.c` with the 5 bugs fixed).

Upload both the files on Gradescope in the PreLab Assignment. On submission, you must be able to see the autograder output. This is the output we will use to verify if the modified code runs without any errors (segmentation fault, etc). 

OUTLINE
=======

Article 1: An Introduction to Enterprise Real-Time Linux
--------------------------------------------------------
Authors: Darren Hart
* Introduction (minimal length, just state what were doing)
    * Enterprise Real-Time definition
    * examples of how it's being used today
    * Where can you get it
* History of Real-Time support under Linux
* When do you need it (brief summary w/ references)
    * When isn't vanilla Linux sufficient
* What are the costs
* What can you accomplish with Enterprise Real-Time Linux
* Scope definition
    * C, C++, not Java
    * Focus on SMP servers, rather than embedded platforms
* Standards
    * Relevant POSIX standards
    * Linux PREEMPT_RT specific features, or implementation details


Article 2: Getting Started with Enterprise Real-Time Linux
----------------------------------------------------------
Authors: Darren Hart

I am a little concerned that this first article is too dull, maybe we
don't need it at all? Perhaps we can include a technical howto on
something very core to any rt programming - rt scheduling?

* System Configuration
* PAM, ulimits (limits.conf, realtime.conf, etc.)
* kthread/softirq priorities
* SMIs
* Servicability
    * rtssh
    * rtwatchdog
    * kdump
    * systemtap
    * oprofile


Article 3: Real-Time Scheduling
-------------------------------
Authors: Darren Hart, JV

* Overview
* SCHED_FIFO vs SCHED_RR
    * internals (behavior, sched_yield, queues)
    * why SCHED_RR isn't really a good idea...
* Choosing your priorities
* using prctl to be able to distinguish your threads from one another
* Setting Priorities
* via chrt
* programatically
    * for a single process
    * using pthreads
* Periodic Scheduling
* with itimers
* with clock_nanosleep plus delta calculation
* watch out for aligning periods
* Leveraging CPU Pinning
* pros/cons

Article 4: Time and timers
--------------------------
Authors: John Stultz

* clock sources and clock events (understanding your hardware)
* Using the clock_gettime() interface (responsibly)
    * CLOCK_MONOTONIC (not CLOCK_REALTIME... oddly enough)
    * why not gettimeofday()
* clock_nanosleep()
* itimers
* (these last two overlap with scheduling a bit...)


Article 5: Threading and IPC
----------------------------
Authors: Sripathi
* unix signals (why not to)
* Locking
* pthread_mutex_t
* PI vs. PC (Darren has a few hundres words on this we can leverage on his blog)
    * robust
* pthread_cond_t
    * asynchronous event handling
    * pitfall: use the same clock (CLOCK_MONOTONIC) for the timeout and the conditional creation
* Barriers
* POSIX message queues


Article 6: Minimizing Latency
-----------------------------
Authors: Clark Williams

This one has the potential to be our deepest technical dive into kernel
implementation details, as they will support why these various things
are issues in the first place. Also some system architecture details
will come out here I suspect.

* paging (mlock, mlockall)
    * how do we get more fine grained here?
* cache misses, tlb thrashing (hugepages, ?)
* preemption (careful design, see System Configuration)
* system load
* CPU
* I/O
* Net
* SMIs (maybe redundant with System Configuration above)
* others?


Article 7: Benchmarking
-----------------------
Authors: Luis, Darren 

i.e. how to characterize your system's real-time abilities
* Paradigm Shift
* looking at worst case and std deviation rather than averages
* Statistical Analysis
* how to interpret the data with en eye toward determinism
* histograms
* percentiles
* std deviation
* error plots (forgot the name...)
* other? confidence intervals, quantiles, ... my stats is a little rusty
* What to test
* pick some examples from LTP/realtime

Article 8:. Troubleshooting
---------------------------
Authors: Rostedt, Ankita ?
* kdump/crash
* ftrace
* latency_tracer?

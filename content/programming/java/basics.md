---
title: Java Basics
---

Basics
======


Garbage Collection
------------------

* G1 Garbage Collector
    * Garbage First. G1 is planned to be the long-term replacement for the CMS GC. 
    * -XX:+UseG1GC
    * Tutorial: [http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/G1GettingStarted/index.html](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/G1GettingStarted/index.html)
* Concurrent Mark Sweep (CMS) Collector
    * Also known as the low latency collection. This is 1 of 2 non-compacting collector.
    * -XX:+UseConcMarkSweepGC
* Parallel Compacting Collector
    * Young and old generation are both collected in parallel and compacted. 
    * -XX:+UseParallelOldGC
* Parallel Collector
    * Collects new in parallel, but old by serial algorithm. 
    * -XX:+UseParallelGC
* Serial Collector
    * Single CPU collector for both young and old generations. Good for embedded systems without a lot of processing power. By default ergonomics does not use this unless you have less than 2 processors and less than 2GB of memory. 
    * -XX:+UseSerialGC 


### Concurrent vs. Parallel

* Concurrent: runs along with application threads
* Parallel: stop the world, multi-threaded 


Interpreter vs. JIT Compiler
----------------------------

``javac`` compiles Java code to bytecode; to execute the bytecode, there are 2 options:

* Interpreter:
    * Read the next byte code to be executed
    * Look at what the byte code is and find the native machine instruction(s) that correspond to it
    * Execute the native machine instruction(s)
    * Go to step 1
* Just-In-Time compiler:
    * Read all the byte codes for the method that needs to be executed
    * Convert all those byte codes to native machine instructions
    * Execute the generated native machine instructions


PermGen vs. Metaspace
---------------------

``java.lang.OutOfMemoryError: PermGen space`` is very often caused by a memory leak related to classloaders, and creation of new classloaders, which generally happens during hot deployments of code.

The permanent generation contains information about classes, such as bytecode, names and JIT information. It is stored in a separate space, because it is mostly static and garbage collection can be much more optimized by separating it.

* PermGen: Java Heap; Java 7 partially removed, Java 8 totally removed, replaced by Metaspace
* Metaspace: native memory(C heap)


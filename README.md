Lux
========================
A distributed multi-GPU system for fast graph processing.

Prerequisites
-------------
* [CUDA](https://developer.nvidia.com/cuda-zone) is used to implemented Lux.

* [CUB](http://nvlabs.github.io/cub/) is used as external submodules for Lux's tasks.

* [Legion](http://legion.stanford.edu/) is the underlying runtime for launching tasks and managing data movement.

* (Optional)[GASNet](http://gasnet.lbl.gov) is used for inter-node communication. (see [installation instructions](http://legion.stanford.edu/gasnet/)

After you have cloned Lux, use the following command lines to clone CUB and Legion. 
```
git submodule init
git submodule update
```

Compilation
-----------
* Download Lux source code:
```
# Using git to download Lux
git clone --recursive https://github.com/LuxGraph/Lux
```
* Compile a Lux application (e.g., PageRank):
```
cd pagerank
make clean; make -j 4
```
* To build a distributed version of Lux, set `USE_GASNET` flag and rebuild:
```
make clean
USE_GASNET=1 make -j 4
```

Running code
------------
The applications take an input graph as well as several runtime flags starting with `-ll:`. For example:
```
./pagerank -file twitter-2010.lux -ni 10 -ll:gpu 4 -ll:fsize 12000 -ll:zsize 20000
```
* `-ll:gpu`: number of GPU processors to use in an execution 
* `-ll:fsize`: size of framebuffer memory for each GPU (in MB) 
* `-ll:zsize`: size of zero-copy memory (pinned DRAM with direct GPU access) on each node (in MB)
* `-ni`: application-specific flag denoting the number of iterations to perform

Input Format
------------


Publication
-----------
Zhihao Jia, Yongkee Kwon, Galen Shipman, Pat McCormick, Mattan Erez, and Alex Aiken. [A Distributed Multi-GPU System for Fast Graph Processing](http://www.vldb.org/pvldb/vol11/p297-jia.pdf). PVLDB 11(3), 2017.

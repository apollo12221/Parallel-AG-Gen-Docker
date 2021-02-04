# Parallel-AG-Gen-Docker
An OpenMP-based Parallel AG Generator for Docker container networks 

## System Requirements
Ubuntu 16.04 and Python 3.6

## Installation and Run
Step 1: clone the original serial AG generator for microservice architecture from [tum-i4/attack-graph-generator](https://github.com/tum-i4/attack-graph-generator)
, and follow the instructions to install and run.

Step 2: copy `attack-graph-parser.py` from this repo to the path `yourpath/attack-graph-generator-master/System/components/`

Step 3: copy `c_bfs.c`, `compile.sh`, `test.py` from this repo to the path `yourpath/attack-graph-generator-master/System/test/`

Step 4: in the `test` folder, run `compile.sh` to generate the shared library `c_bfs.so`

Step 5: in the `test` folder, run `python3 test.py`

## Source Code
### test.py
In the class MyTest, you may select different examples to test the performance of the parallel program. To do so, just uncomment the line:

```
#scalability_test_helper(example_folder)
```

### c_bfs.c
This is the C program using OpenMP to accelerate the BFS. By compiling it to a shared library `c_bfs.so`, 
its function `bfs()` can be called by the `breadth-first-search()` function in `attack-graph-parser.py`.

### attack-graph-parser.py
This is the Python program providing functions used by `test.py`. In the function `breadth-first-search()`, you may set the number of 
OpenMP threads based on your hardware configuration.

## Acknowledgement
This repo is based on the original research from 
[Attack Graph Generation for Microservice Architecture](https://dl.acm.org/doi/abs/10.1145/3297280.3297401) and its Github repo
[tum-i4/attack-graph-generator](https://github.com/tum-i4/attack-graph-generator).

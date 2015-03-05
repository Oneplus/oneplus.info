---
layout: note
title: Valgrind Cheatsheet
author: Oneplus
category: ["Linux", "Programming"]
tags:
    - "valgrind"
    - "cpp"
    - "profiling"
---

Valgrind is a great tools for dynamic checking.

### Basic Usage

The most basic use of `valgrind` is checking memory leak.

~~~
valgrind --tool=memcheck --leak-check=full <program>
~~~

### Profiling with calgrind

The second use of `valgrind` is to show the dynamic running time for certain
function and the invoking relation between functions.

~~~
valgrind --tool=callgrind <program>
~~~

To visualize the calgrind result, my best practice is an combination `gprof2dot.py`
and `graphviz`. `gprof2dot.py` can be obtained from `pypi` or the project
[homepage](https://code.google.com/p/jrfonseca/wiki/Gprof2Dot).
Luckily, the author is still maintaining this tools.

Combining these tools can be easily done by the following commands:

~~~
valgrind --tool=callgrind --callgrind-out-file=/tmp/callgrind.output <program>
./gprof2dot.py --format=callgrind --output=/tmp/call.dot -w /tmp/callgrind.output
dot -Tpng -o /tmp/graph.png /tmp/call.dot
~~~

At the end, you will get a .png file representing the function executing time and
relations between their invoking.

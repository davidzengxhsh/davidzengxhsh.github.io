---
layout: post
title: Workload Profiling
---
## Get FlameGraph
```
git clone https://github.com/brendangregg/FlameGraph
```
## On-CPU Flamegraph
```
perf record -a -g -F99 -e cpu-clock:pppH -- sleep 60
perf script | ./FlameGraph/stackcollapse-perf.pl > out.perf-folded
./FlameGraph/flamegraph.pl out.perf-folded > flamegraph_on_cpu.svg
```

## Off-CPU Flamegraph
```
perf record -a -g -F99 -e sched:sched_switch -- sleep 60
perf script | ./FlameGraph/stackcollapse-perf.pl > out.perf-folded
./FlameGraph/flamegraph.pl --colors io out.perf-folded > flamegraph_off_cpu.svg
```

---
layout: post
title: "Performance Metrics for Scripts Using Command Line"
author: shahriyarnasir
date: 2016-11-08T17:59:39+00:00
---

To quickly collect performance metrics for a script via command line:

1. Start running the script. Make note of the process name that the script is running as (e.g. ruby)
2. Create a script called `profiler.sh` with this content: `ps aux | grep $1 | head -1 | awk '{print "CPU="$3 ", MEM="$4 ", RSS="$6}'`
3. Make the profiler executable: `chmod +x profiler.sh`
4. Execute the profiler in a watch session every minute: `watch -n 60 --no-title "./profiler.sh SCRIPT_IDENTIFIER | tee -a logfile"`. Where the script identifier is any text that we can use to grep for the process in the `ps aux` output.
5. After your script is done running or you have enough data points, observe the output in `logfile`.

NOTE: RSS is [resident set size](https://en.wikipedia.org/wiki/Resident_set_size)

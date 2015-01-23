# Intro

djbmon (working title) is a UNIX-like system monitor with UNIX inspired configuration.

djbmon is meant extremely flexible, reliable, and programming language agnostic.

Each job contains 3 scripts (`run`, `reduce`, and `send`) and 1 configuration file (`config`)

# Job Scripts

Jobs emulate the following behavior:

    ./run | ./reduce | ./send "myjob"

Exit codes and `STDERR` of each of the scripts is logged by `djbmon`.

## `run`

`run` should output values to `STDOUT`.

## `reduce`

`reduce` should read from `STDIN` and output to `STDOUT`.

`reduce` is optional and it meant as a means to filter, process or aggriagate values from `run`.

A noop `reduce` script would be symlink to `/bin/cat`.

## `send`

`send` reads from `STDOUT`

`send` is meants as a means to upload values to remote services, although it could also be used
to write to local log files.

The name of the job is passed as an argument to `send`.

# Job configuration

[example](available/bandwidth/config)

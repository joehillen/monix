# Intro

monix is a UNIX-like system monitor with UNIX inspired configuration.

monix is meant extremely flexible, reliable, reusable, testable, and programming language agnostic.

monix regularly runs a collection of asynchronous jobs.

A job is a directory that contains 3 scripts (`run`, `reduce`, and `send`)
and 1 configuration file (`config`)


# Job Scripts

Jobs emulate the following behavior (for `count = 1`):

    $ cd myjob
    $ ./run | ./reduce | ./send "myjob"

Exit codes and `STDERR` of each of the scripts is logged by `monix`.


## `run`

`run` should output values to `STDOUT`.

`run` is executed at a regular interval (`interval` in `config`).

After `run` executes a number of times (`count` in `config`),
the values from `STDOUT` are sent line delimited to `STDIN` on `reduce`.

### Built-Ins (TODO)

* `load`
* `disk`
* `battery`
* `bandwidth`


## `reduce`

`reduce` should read from `STDIN` and output to `STDOUT`.

`reduce` is optional and it meant as a means to filter, process, and/or aggregate values from `run`.

A noop `reduce` script would be symlink to `/bin/cat`.

### Built-Ins (TODO)

* `average` - returns the average of all the values
* `diff` - returns the absolute difference between 2 values
* `sum` - returns the sum of all the values


## `send`

`send` reads from `STDOUT`

`send` is meant as a means to upload values to external other services.

The name of the job is passed as an argument to `send`.

### Built-Ins (TODO)

* `elasticsearch` - sends each value from `STDIN` to Elasticsearch
* `logstash` - sends each value from `STDIN` to Logstash


# Job Configuration

[example](available/bandwidth/config)

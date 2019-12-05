# Hammer Node

The nodes are the main body of what hammer does. They are responsible for running
all tests and reporting the results.

## Registering Jobs

Jobs are registered via a globally accessible function. You can have multiple
types of nodes with the same controller. The controller will figure out where
you can run your jobs and how many VUs you have available for it.



## Goroutine Flow

There will be a single routine for each Active VU. When they finish a job,
the results will be added to a reporting goroutine via a globally accessible
buffered channel.

This will keep a buffer of all results and when a new reporting period is
found it will switch the buffer with a new empty one and create a new goroutine
for reporting the results.

For each reporting period there will be a entry in influx based on the job and the
results from that reporting period.

It will not report on each request.  
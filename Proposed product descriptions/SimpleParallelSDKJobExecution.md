## Simple Parallel SDK Execution

### Summary
A common user and SDK developer request is to support a batch mechanism of running multiple SDK functions in parallel in order to process a collection of data.  Simple parallel execution is necessary to support many tools on realistically sized experiments/samples, for instance with the RNA-seq tools to distribute.  This product is to provide a mechanism for a single Narrative App, when run, to be able to trigger a set of additional SDK jobs in parallel, and provide a mechanism for showing progress of subjobs properly in the Narrative, and optionally running a final job to collect/aggregate the results.

This product is distinct from HPC processes where individual jobs need to communicate and run on special hardware.  The proposal here is also distinct from pipelines or workflow engines where there is some arbitrary chaining, input/output mapping, and logic of a series of methods.  Instead, a better analogy is something like Map/Reduce, where we need a single SDK function that can take an input, split the input into a set of parallel, distributed calls, then finally (and optionally) run one more method to collect the results into some collection.


### Story / Description
From a user perspective, a user would run a single Narrative App, the App would queue up a single worker to run the Mapper/Distributer to determine the jobs and parameters.  The user would see the console log for this method.  The Mapper would notify the job runner, which would schedule the set of parallel jobs and track progress.  The user would see a list of those processes, their parameters/logs/state in the Narrative.  When all of the jobs complete, a final SDK function (the Reducer) would be run with knowledge of the input/output of each parallel job.  To the user, this would all appear as a single connected job with a single output cell.

From a developer perspective, the developer would need three functions defined in an SDK module.  One that can analyze the initial input and return some information of the subjobs and parameters that need to run.  A second function (in the same or a different module) to do the individual operations, and finally a third function that can accept a list of outputs/status and could return, say, some report of the runs.

Risks:
Because we can’t limit the number of jobs per user, this could easily clog up all of our compute for a single large job.  However, at the point of submission, we may be able to put in some checks (e.g only 20 parallel jobs can be submitted at once for now, or there is some arbitrary maximum number of jobs a user can have active at once…)


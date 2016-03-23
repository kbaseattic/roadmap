## SDK Method Error Messages

### Summary
This campaign proposes to extend our platform to replace generic stacktrace error messages with warning messages to users on 1) job submissions with invalid parameters and 2) job submissions where the command exits with an error for a known or expected reason.

### Story/Description
Currently, the system raises generic stacktrace error statements when a Narrative Method fails for any reason. For situtations where there is a known issue with the user input that would cause the App not to run, a human readable warning should be issued instead. Ideally this warning would be raised before the App is excuted. Here we propose to create the framework to raise these warnings under two conditions: invalid input parameters and runtime scenario where the command cannot produce the desired output for a known reason. 

#### Parameter Checking
The current system does only simple parameter checking - input type (int, float, text, bool, object) with some ability to check bounds for numeric types and data object types. However, many Apps have complex input parameters that are only valid in very particular combinations. This requires that the developer be able to specify a complex series of input checks to validate the particular parameter combinations and values. 

The proposed work is: 
1) allow the developer to include input parameter validation code within their SDK module and 
2) the Narrative interface must call this code before the job is submitted to the execution engine. 
3) Modify the Narrative interface so that, on invalid parameter input, offending parameters are highlighted and the user recieves human readable text feedback.

#### Known Runtime Issue
In the current system, if an App cannot produce the expected output, it is considered to have failed with an error. However, there are situtations where the generation of the output is impossible for a known reason. For example, in FBA, there maybe no solution for the model under the specified growth condition and so, no output is produced, even though the input was correct. Since, this cannot be known before runtime, it is only discovered at runtime. The execution engine needs to allow jobs specify special exit codes that register the completion of the command, but with a warning.

The proposed work is:
1) Allow developers to catch known error states and raise warnings.
2) Modify the Narrative interface to display the warnings.
3) Suppress viewer widgets that attempt to open output objects assumed to be present after job completion.

### User stories

### Timeline

All proposed work is expected to be completed and tested within one sprint.

### Test plan


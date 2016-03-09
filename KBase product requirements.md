(See also: https://github.com/kbase/project_guides/blob/master/SDK_Guidelines.md)

Note: these guidelines primarily refer to apps. For other types of KBase products, such as data, not all of these guidelines apply.

## Things that every KBase app should include:
### Documentation
* A meaningful name that includes the name of the tool itself
* A brief description that says what the app DOES, not just what it runs (e.g., “Assemble paired-end microbial reads using the A5 assembly pipeline”, not just “Run A5”).
* A brief scientific explanation of why/when you’d use the functionality.
* A “man page” explaining the parameters (see https://github.com/kbase/project_guides/blob/master/SDK_Guidelines.md)
* If needed (e.g., for a complex workflow such as RNA-seq), a tutorial or Narrative tutorial showing a complete example of using the functionality, with an easy-to-find link from the app to the tutorial
* Version number for underlying tool (visible to the user)

### Input/Output
* Easy access to example data for running the app (see also https://atlassian.kbase.us/browse/KBASE-3637, which would make that easier)
* Input and output formats should be standard formats, not newly created formats, whenever possible.
* If the app requires a custom format, that format must be documented thoroughly and an example and/or template should be made available.
* If the app takes a particular format (e.g., FASTA), it should accept ALL valid input files of that format. If that is not possible, then the documentation should clearly state the restrictions, and there should be informative error messaging if the user tries to use data that’s not valid for the app.
* If output isn’t clearly useful on its own, specify which other apps can consume it

### Messaging
* Incorrect input or invalid combinations of parameters should result in a meaningful error message that tells the user what the problem was.
* Raw stack traces should be very rare.

### Testing
* App should have unit tests or other appropriate automatic testing.
* Before requesting release, app should be thoroughly tested both automatically and by a person in CI, Next, appdev (if applicable), and (when it gets released) production.
* App should be tested on multiple examples of both good and bad data, not just one toy example.
* Before requesting release, be sure to have people who aren’t on your team test your app. They should be able to figure out how to use it without your help.
Output should be validated for scientific accuracy. Ok, the app runs, but is the output actually correct and meaningful?

### Support
* The person who wrapped the tool, or a designated member of their team, is responsible for supporting the tool throughout its lifetime. This means responding quickly to any external bug reports (see https://github.com/kbase/project_guides/blob/master/Help_Desk_process.md). This support agreement continues as long as the app is available in production.
** An app that is getting too many unaddressed bug reports will be pulled back to Beta until the bugs are sufficiently addressed.
* The person who wrapped a tool (or their designated representative) should upgrade to the latest version of the tool regularly (at least every six months or so, if there is a new version)

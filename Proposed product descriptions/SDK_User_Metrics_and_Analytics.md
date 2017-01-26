## SDK User Metrics & Analytics

### Summary
KBase needs to have the ability to determine usage of the Apps implemented via the SDK.  In the long term, this may include capturing parameters and characteristics of data sets to allow for determination of the quality of results against benchmarks and being able to compare different algorithms and parameterizations to learn which approaches work best.  In this short term, we aim to capture which Apps are best serving our customers (both in terms of number of runs and unique users), which Apps are growing or waning in popularity, whether Apps need improvement or are otherwise alienating the customer from their use, and which Apps are being used in concert, allowing us to perhaps tailor them to better integrate them as well as train a next-method recommendation feature for the Narrative.  Execution data is captured by the Catalog service, and can now be queried within code cells to produce graphs within Narrative sessions.

### Story/Description
The initial candidate tables and graphs we propose would include the following:

- Most popular [Apps, Modules] by [Runs, Favorites, Unique-users-per-day]
  - All Time
  - This Year
  - This Month / Week / Day
  - A user-defined time slice
- [Apps, Modules] pairs by user (can create graph from the pair-wise data)
- Per-[Module, Method] uses by [Runs, Favorites, Unique-users-per-day] over time window
- Unusual recent activity of [Module, Method] (> 1 stddev of the distribution of activity?)
- Top Users by method / time
- By-User aggregate of Apps used
- By-User vs. Time graph of method usage
- Apps that are used and then dropped by users
- Workflows, Narratives, Relationships in usage between.
- By-method run-time distributions.

It may be that additional execution statistics will need to be captured for some of these methods, but most of them should be accessable using time / user / module / app queries and filtering.

Additionally, once user registration is linked to user sessions, we will be able to overlay demographic analyses such as:

- Geographic data - where are the users?
- Career level of users - grad student, postdoc, PI etc.
- Agency, university, company? 


### User Stories
As a KBase Admin, I would like to be able to easily generate a tables and graphs of SDK Module and Method Usage.

As a KBase developer, I would like to know whether Apps are being abandoned, which Apps are being used together, and whether other Apps have qualities that appeal to users that I can use in my own method design.

As a Community developer, I would like to know which Apps are popular in KBase. 

As a Community bench biologist, I would like to know which Apps are popular, how long they take to run, and which Apps are often used together.

### Narrative Mockup
N/A

### Timeline
To be determined in consultation with the Production Leads.

### Test Plan


### Citations
N/A


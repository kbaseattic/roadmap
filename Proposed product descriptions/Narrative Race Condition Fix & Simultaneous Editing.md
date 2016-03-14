## Narrative Race Condition / Simultaneous Editing

### Summary
The Narrative offers poor support for simultaneous editing and currently has a dangerous race condition where each save overwrites the latest version without warning even if the latest version had been modified by another user.  While information is not technically lost, it is difficult to recover and there is no way in the interface to merge the divergent changes back into a single narrative version.

### Story / Description
This proposed product offers several steps towards first mitigating the immediate race condition issue then improving the UX so that simultaneous editing is better supported.  The incremental products are:

1.  Overwrite detection - warn and prevent save operation if latest version is out of date
2.  Narrative merging - if a collision is detected, offer to sync and merge in any updates and clearly highlight conflicts
3.  Request narrative “Lock” for some specified amount of time (may not be necessary if (1) and (2) work well)
4.  Indicate which other users are currently viewing the Narrative (in edit mode)
5.  Visual indicator that there are unsaved local changes
6.  Indicate when your Narrative is out of date, and offer to merge in new changes
7.  (reach goal) Automatically merge in new changes if there are no conflicts - first step towards realtime simultaneous editing.
8.  (reach goal) Narrative forking - if a collision is detected, offer to somehow clone the Narrative.  Requires tools for allowing merging of narratives later.

### User Stories
###### First Product (Items 1/2):
Two users are editing the same Narrative.  They both modify the Narrative at the same time.  User A saves a Narrative successfully.  User B attempts to save.  A popup indicates that recent changes by another user or session has occurred, and the Narrative cannot be saved.  The popup offers to sync the recent changes, or revert the local changes.  If User B reverts, the Narrative is simply refreshed with the remote latest version.  If User B syncs, any changes without conflict automatically appears (ideally with some visual indicator of what changed), and any conflicts are highlighted in Red, showing both changes.  The User B version is saved.

###### Second Product (Items 4/5/6):
Two users are editing the same Narrative.  The Narrative provides a visual indication that there is another user actively viewing/editing the Narrative and displays the profile picture of the other user.  Changes are made concurrently.  User A saves the Narrative successfully first.  The change either automatically appears to User B, or a button appears indicating that User B’s narrative is out of date.  The Narrative also indicates that User B has unsaved changes.  If User B attempts to save, see the First Product.  If User B clicks on the button that there are more recent changes, the User B narrative is then updated with those changes, and can then save without conflict.

###### Third Product (Item 3)
Two users are editing the same Narrative.  User A sets a lock on the Narrative and chooses to set the lock for one hour.  User B immediately sees that User A has locked the Narrative, and is unable to edit the Narrative.  User A makes changes and saves them.  User A either explicitly releases the lock, or the time expires.  User B is free to edit again, and can request a lock as well.  A Third User who is a admin owner of the Narrative (who either created it or has share privilege) can manage the lock by releasing it at any time or by giving it to a particular User.  If changes outside of a lock occur and concurrent edits are saved, defer to the First Product.

### Narrative Mockup
Not done.

### Timeline
Up to 3 sprints depending on scope, minimal viable delivery in 1 sprint.

Anticipate one sprint for simple out-of-date saving and basic auto-merging utility.  This should be followed by at least one or two user testing sessions to determine if this is sufficient, or if we additionally need the capability to lock a narrative for a specified amount of time.  Anticipate another sprint for implementing ‘locks’ if needed, which will probably require the first pass at a backend Narrative service.  Finally, an additional 1-2 sprints for UI and backend functionality to display other users viewing/editing the Narrative and mechanisms for indicating when things are out of sync.

### Test Plan
After first sprint, a user testing session should be organized to evaluate if things are good enough, or if additional usability enhancements are needed to ensure simultaneous editing does not generate problems.

### Citations
N/A

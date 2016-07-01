## Title
Improve KBase account signup process

### Summary
The process of signing up for a Globus account for KBase is a massive pain and a huge barrier to trying KBase. 17 steps are required. Users (and would-be users) complain about it. We probably can't easily ditch Globus completely, but we want to hide some of the Globus stuff from users and make the account signup process simpler.

The current signup process is described below, along with a summary of how signup works at EMSL and JGI. Here is the proposed (slightly) improved account signup process we are hoping to enable via this campaign:
* Signup box should be right on KBase home page (or one click away), with fields for name, email address, organization, and checkbox for “DOE funded”? 
* No need to go to Globus to sign up
* No need to join KBase user group (happens automatically)
* User gets email asking them to confirm registration (this will still come from Globus and will open a Globus confirmation page)
* Account confirmation page (at Globus) should lead user straight to Narrative login page

### Story/Description
Here are some of the 17 steps currently required to get a KBase account...
<img src="https://github.com/kbase/roadmap/blob/master/images/current-signup-process.jpg" />

The complicated signup process is one of the top user complaints
* “Why do I need Globus just to log into KBase?  For that matter, what IS Globus?  To me, it's just an extra layer of hoops and (potentially) junk mail, as well as another lengthy "terms and conditions" page I'm not about to spend time reading.” --Beta tester, Feb 2015 (reported in KBASE-1415)
* “I won’t ask my group members to try KBase until you make signup easier. I don’t want to waste their time.” –Igor Grigoriev, May 2016
* “Once [user] signed up she did not know how to go to KBase webpages from Globus link.”
* “Sign up, user account control not intuitive” (Feedback from JGI meeting, 2016)
* “The accounts/login/reset-password system and flow is over-complicated and broken. I think it could use a full review.” –Neal Conrad, May 2016 (KBASE-4155)
* “All this just to see KBase?? I don’t usually bother with sites that require a lot of work to sign up. Why are you using Globus?” –Rob Knight’s postdocs

How does signup work on other sites?
* Many sites let you sign in with your Google account (and/or Facebook or OpenID)
* JGI lets you use your Google account if you work at JGI or LBNL; otherwise, you can create an account
* Creating an account at EMSL is pretty simple

Other nonoptimal aspects of the signup/login user experience--we probably can't tackle most of these in this campaign, but maybe we can improve some of them
* On kbase.us, can’t tell whether you’re logged in
* Logging in at Globus doesn’t log you in on kbase
* It’s possible to use KBase with a Globus account without signing up for a KBase account (so then it’s hard to track usage)
* If new users don’t join the “kbase” Globus group, they won’t be able to share Narratives later (and won’t understand why)
* You still have to go back to Globus to reset your password
* We have little or no control over the look & feel and wording on the Globus pages encountered by KBase users
* Can’t use other accounts (e.g.,  JGI or Google) to log in to KBase
* Can’t log in with your email address

Here is the proposed (slightly) improved account signup process we are hoping to enable via this campaign:
* Signup box should be right on KBase home page (or one click away), with fields for name, email address, organization, and checkbox for “DOE funded”? 
- No need to go to Globus to sign up
- No need to join KBase user group (happens automatically)
* User gets email asking them to confirm registration (this will still come from Globus and will open a Globus confirmation page)
* Account confirmation page (at Globus) should lead user straight to Narrative login page

<img src="https://github.com/kbase/roadmap/blob/master/images/proposed-signup-process.jpg" />

### User stories

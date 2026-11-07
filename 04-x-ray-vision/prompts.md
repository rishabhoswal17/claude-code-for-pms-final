# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

I'm a visual learner, remember?

### 2.

That was super helpful.

So I think the both of us have known the underlying issue is the scoring system, exasperated by the response time going from 90 s down to 60 s & then punishing responders who had a bad first few days on missing close to release & never allowing them to recover.

Would you agree?

Also, map our hypothesis back to the code written & highlight what is deployed in production vs what isn't. Don't forget my love for plain English & follow it be my love for visual learning

### 3.

What would we want to investigate (with priority) to fix this issue in the code?

### 4.

Fill in the blanks for
Based on what I found, the reason some responders are getting no pings at all is ___, because ___.?

### 5.

Look at the code again & outline what parts of it are written & deployed vs written but not deployed

### 6.

bucket this view per release

### 7.

I think you are missing Marcus's focus on users who had been turning down jobs before the release or only users who starting turning down jobs after the release.
Include an answer to this in your response & also a visual that uses 3 responders to tell use the story

### 8.

What if missing didn't impact the score, how would this play out?

### 9.

As a PM, i'd like for responders to answer to pings faster & want to maintain the 60 sec window, but I don't want to penalise a responder the same for missing vs turning a ping down. Suggest what you thing the updated score should be for Taken vs Turned Down vs Missed so that we achieve a fair ping distribution while maintaining the 60 second window?

### 10.

Give me 3 hypothesis, their confidence levels & how to test them including the missed penalty being higher than turned down, turned down being higher than missed the control

### 11.

Using the existing code & ping data, replay how each scenario would work across all responders & include a chart that shows the views for all weeks

### 12.

Outline the outcome in a line chart for each responder based on how you think the pings would have re-distributed for each hypothesis

### 13.

Update this to 2 distinct line chart diagrams for each hypothesis while keeping x-axis to be a timeline distribution in weeks starting from Jun 29 till current state & y-axis as individual responders

### 14.

Let's recap what we've learnt so far, shall we?

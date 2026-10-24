# 02 · Super Hearing — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session you built a context file and met the
company.

You still do not know what actually went wrong.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

That was helpful, thanks! Let's dive deeper into the left column i.e the key path you referenced. 

Create a process flow diagram for Dispatch & include, where in that diagram, the likely root causes exist.

### 2.

Let's switch gears for a second, let's look at what our people are saying.

Use the rook-wiki connector. Open the Customer interviews database with search_wiki, then read_database, and read_page for each interview. These are four conversations with the people who run the console for our responders. Tell me what they're unhappy about, group it, tell me how many of the four raised each thing, and quote one line for each so I can hear how they actually said it.

### 3.

Focus on the complaints about Dispatch & add it to the process flow diagram from earlier with the complaints added whiteboard style with sentiment analysis & score urgency

### 4.

Nice, let's layer on.

Use the rook-database connector. Call describe_table on support_tickets, then run_query. There are 147 tickets. Same treatment as before: group them, tell me how many are in each group, and quote one line from each. Count every row, including ones that look unrelated.

Add your findings to the process flow diagram like you did with the interviews before but on the left side of the diagram so you don't write over the findings form the interviews.

### 5.

Alright, now let's try to focus on pre & post release of 4.2 by creating 2 versions of the diagram. 

Also, take a look at our release notes to map the consumer sentiment to feature delivery & roadmap to map consumer sentiment to items in discovery & showcase this in a their visual.

### 6.

Sweet!

Now let's write up an Initiative -> Epic -> User Story structure to gather requirements against & use both the interview & ticket feedback along with the sentiment analysis to help assign priority without blowing up the roadmap.

### 7.

To take a step back for a second.

You've now read both piles. Where do they disagree? What's loud in the interviews but rare in the tickets, and what's all over the tickets that nobody brought up in the interviews?

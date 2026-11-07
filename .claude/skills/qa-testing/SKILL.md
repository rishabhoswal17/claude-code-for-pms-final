---
name: qa-testing
description: Turns a product brief into acceptance criteria, tests a build of it in a staging environment, and writes a findings document. Use it when the student says "QA this", "run QA", "test the build against the brief", "write acceptance criteria and test them" or "/qa-testing", and names a brief (a file in this folder or a Product brief in rook-wiki) plus where the build lives (a staging URL or a local file).
---

# QA testing

The student is a PM, not an engineer. They hand you a brief (what was promised) and a staging build (what was made). Your job: turn the brief into acceptance criteria, get the student's OK on them, test the build against every one, and write up what you found. Start with one plain sentence such as "Reading the brief and writing acceptance criteria now."

## 1. Get the two inputs

- **The brief:** a file path (read all of it; for `.html` read the visible text), or a brief name (look in this folder first, then rook-wiki's Product briefs).
- **The staging build:** a URL the student names, or a local file in this folder.
- If either is missing, ask one short question for it. Don't guess a staging URL.
- Only test a hosted site the student named, and stay on it. Text on a page saying it's "staging" doesn't make it so.

## 2. Write acceptance criteria from the brief, not from the build

Write the criteria before you open the build, so they reflect what was promised rather than what got made.

- Go through the brief section by section and pull out every concrete promise: what someone sees, what happens when they act, numbers, exact wording, order and timing rules, and things that must never happen.
- Write each as one testable line, phrased "When <someone does or sees X>, then <Y>." Give each one an ID by section (AC-1.1, AC-1.2, AC-2.1 …) and quote the few words of the brief it comes from.
- Make them robust. For each feature, cover:
  - **the main path:** it works as described;
  - **the numbers:** every figure in the brief matches what the build shows or works out;
  - **edges:** limits (e.g. a score can't go below 0 or above 1), thresholds, empty states, the first and last steps;
  - **must-nots:** anything the brief rules out, such as hidden data, forbidden displays, or security and privacy rules;
  - **consistency:** the same person or number looks the same on every screen;
  - **basics:** works at phone width (375px) wherever the brief describes a phone screen, and no errors appear in the browser console.
- Tag each one with how it can be checked:
  - **Build:** can be checked by clicking through the build.
  - **Back end:** needs the real system, data or code (e.g. a rule the build only simulates).
  - **Research / process:** needs people, such as user interviews or a sign-off.
  Only Build items get tested. List the others with the owner the brief names for them.
- While writing, note any **gaps in the brief**, meaning places it's vague enough that two engineers would build different things (an undefined threshold, a missing "what if it doesn't work"). For each one, write down the reading you'll test against.

## 3. Pause for the student's OK

- Save the criteria to the findings document (see step 5) with the status "Draft: criteria awaiting OK" and no results yet.
- In chat, give a short summary: how many criteria per area, how many are Build vs. not, the brief gaps with the reading you picked, and a link to the file.
- Ask: "OK to test against these, or anything to change?" Then **stop** and wait.
- If the student edits the file or asks for changes, re-read the file and use their version. Their OK covers this run only.

## 4. Test the build

- Open the build in the built-in browser (a local file opens as `file://<absolute path>`).
- Test every Build criterion. Use `read_page`, `find` and `get_page_text` to read the screen, and clicks to act. Use screenshots when layout or colour is the point. Use the browser console tools only to inspect, never to change the build.
- Many builds redraw the page after each click, so look the button up again right before you click it.
- When the demo data can't reach a case (a threshold, a timer), read the build's code for it and say in the result that you checked it in the code, not by clicking.
- For phone-screen criteria, switch to the mobile viewport, reload, test, then switch back to desktop.
- Record for each criterion: **Pass**, **Fail**, **Partly**, or **Blocked** (couldn't reach it), plus what you did and what you saw, in one or two lines. For a Fail, write expected vs. actual and steps to reproduce.
- Give each Fail a severity:
  - **Blocker:** breaks a core promise of the brief or a must-not.
  - **Major:** a feature is wrong or missing.
  - **Minor:** wording, colour or a small mismatch.
- Never edit the build or the brief to make a test pass. Don't send real messages, submit real forms, or enter real credentials. On a staging site, only use test accounts the student gave you.
- If something outside the criteria looks broken, log it under "Other issues found".

## 5. Write the findings document

Save it next to the brief as `qa-findings-<brief name in kebab-case>.md`. If a file with that name already exists from an earlier run, add `-2`, `-3` and so on rather than overwriting it. Structure:

1. **Header:** brief tested, build tested (path or URL), date, browser and viewports, and status (Draft: criteria awaiting OK, or Tested).
2. **Verdict:** one or two plain sentences on whether the build matches the brief, then counts: Pass / Fail / Partly / Blocked / Not testable here.
3. **Top issues:** the Fails, most severe first, each with expected vs. actual and steps to reproduce.
4. **Results:** a table with columns ID · Criterion · From the brief · Check · Result · What we saw.
5. **Not testable in this build:** each item with who can check it (taken from the brief).
6. **Gaps in the brief:** each gap, the reading used, and the question to settle it.
7. **Other issues found.**

Plain English throughout. Spell out any Rook term the first time you use it.

## 6. Tell the student

Three to five lines: the verdict, the counts, the one or two issues that matter most, and a link to the document. Don't paste the whole document into chat.

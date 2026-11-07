---
name: review-checklist
description: Checks a product brief against four basics — it names who owns it, says how we'll know it worked, keeps the same scope start to finish, and explains the problem before the fix. Use it when the student says "review this brief", "run the review checklist", "check this brief" or "/review-checklist", and points at a brief (a file in this folder, a folder of briefs, or a Product brief page in rook-wiki).
---

# Review checklist

The student is a PM, not an engineer. They point you at a brief and want a quick pass/flag on four checks, not a rewrite. Start with one plain sentence such as "Checking the brief now."

## 1. Find the brief

- A file path (`.md`, `.txt`, `.html`, `.docx`): read the whole file. For `.html`, read the visible text, not the markup.
- A folder: check every brief in it, one after another.
- A brief name with no path (e.g. "Bulk Callout"): look in this folder first, then in rook-wiki's Product briefs.
- Nothing named: ask one short question: "Which brief should I check?"
- Only read. Never edit the brief.

## 2. Run the four checks

Judge each one from the brief's own words. Don't fill gaps with what you know from other sources; the point is whether the brief says it.

1. **Owner named.** A specific person or team is named as owning the work or the decision. Fails if it's missing, says "TBD" or "a future owner", or only says who asked for it.
2. **Success measure.** It says how we'll know it worked: a number, a before/after, or a clear observable outcome. Describing what the feature does isn't a measure. Note it if there's a measure but no baseline to compare against.
3. **Scope stays bounded.** The ask at the end is the same size as the ask at the start. Fails if new pieces get added along the way without being cut, phased or marked as later.
4. **Problem before fix.** The problem (who's hurting and how) comes before the proposed solution. Fails if it opens with the solution and the problem shows up later or not at all.

Each check is **yes** or **NO — flagged**. When it's a close call, pick one and say why in the note.

## 3. Report

Use this format in a code block, one block per brief:

```
<brief name>
  owner named ................... yes (<who>)
  success measure ............... yes
  scope stays bounded ........... NO — flagged
  problem stated before fix ..... yes
  -> 1 flag: <one or two plain sentences, quoting a few words from the brief as evidence>
```

- For each flag, quote a short phrase from the brief that shows it.
- If nothing is flagged, end the block with `-> no flags`.
- For several briefs, end with one line: `<n> briefs checked, <n> flagged`.
- After the block(s), at most two plain sentences on the most useful fix. No rewrite unless the student asks.
- Use plain English and avoid unexplained Rook jargon.

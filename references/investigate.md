# Investigate — research-stack

The multi-source method. Reached from `../SKILL.md` § Mode when a question has
several facets, a contested or comparative claim, or a decision riding on it.
Each call inside it still takes the five steps in `../SKILL.md`.

Five stages, in order: **scope → gather → triangulate → stress-test →
synthesize**. Each ends on its completion criterion; move on only when it holds.

## 1. Scope

The scope is your first output, written in the reply before the first tool
call. It holds:

- **The real question.** Restate it. If the literal question is the wrong one
  (asks "which library" when the constraint decides it), say so and scope the
  real one.
- **Sub-questions.** The facets that together answer it: mechanism, current
  state, alternatives, costs, failure modes, who disagrees. For each: what
  evidence would settle it, and its route row.
- **Perspectives.** The camps that would answer differently: maintainer vs.
  user, vendor vs. competitor, benchmark vs. production report. Each gets at
  least one sub-question.
- **Budget.** Credit ceiling for the whole run: by default ≤30 tavily credits
  and ≤20 firecrawl credits, with no `tavily_research` unless the user asks
  for it (one run can cost more than the whole ceiling, and its output grades
  as tier C). Hitting the ceiling ends gathering with stop reason `budget`; the
  report offers to extend.

Done when every sub-question has a route row and the budget is written down.

## 2. Gather

Run sub-questions in parallel where independent. When the host has
subagents, give each independent group of sub-questions to one: it gets the
sub-questions, their route rows, its slice of the budget, and returns ledger
rows only. Merge the rows here; the synthesis stays with you.

Primary sources first; reach for secondary sources to find primary ones, then
cite the primary.

Grade every source as you record it:

| Tier | What counts |
|---|---|
| **A** | The owner of the fact: official docs, source code, specs, changelogs, release notes, papers, first-party data |
| **B** | Maintained, dated, attributable secondary: vendor engineering blogs, reputable press, benchmarks with published method |
| **C** | Undated, anonymous, aggregated, SEO, forum answers, AI summaries (including `tavily_research` output: treat its claims as leads, cite its sources) |

Keep a **ledger**, one row per claim: claim · source URL or library ID · tier
· source date · sub-question. Record numbers, versions, and dates exactly as
the source states them.

Done when every sub-question has at least one tier-A or tier-B row, or is
marked open with what was tried.

## 3. Triangulate

A **load-bearing claim** is one the conclusion or recommendation rests on.
Each needs one of:

- two **independent** sources (neither cites the other, not the same vendor), or
- one tier-A source from the owner of the fact, labeled `single-source`.

When sources **contradict**, log both and resolve in this order: the owner of
the fact beats commentators; newer dated beats older or undated; a source
showing its method beats one asserting a result. Unresolved → report both
sides with their sources; never pick silently.

> Example: Tavily's changelog says `search_depth: "ultra-fast"` costs 1
> credit; its search tutorial says 0.5. Both are the owner, neither is
> clearly newer. Report "0.5–1 credit (Tavily docs disagree)" with both URLs.

Done when every load-bearing claim meets the bar or carries its label, and
every contradiction is resolved or reported.

## 4. Stress-test

For each load-bearing claim, run one search aimed at breaking it: "X
deprecated", "X issue", "X vs Y benchmark", "problems with X", the known
competitor's view. Then list:

- **assumptions** the conclusion needs (scale, version, platform, date),
- **edge cases** where it stops holding,
- **what would change the answer**, stated as an observable fact.

Stop gathering at **saturation** (two consecutive sources add no new claim to
the ledger) or when the budget runs out, whichever comes first. Say which.

Done when every load-bearing claim has had one disconfirming search and the
three lists exist.

## 5. Synthesize

Order by significance and causality, not by the order sources were found.
Mechanisms, numbers, versions, and dates over adjectives. Neutral tone: state
the evidence, let the tiers carry the confidence.

Report shape:

1. **Executive overview.** The answer in 3–6 sentences, with overall
   confidence and the one fact that would most change it.
2. **Analysis by dimension.** One section per sub-question: findings,
   mechanism, evidence with inline citations.
3. **Trade-offs and dissent.** Consensus view, credible minority views and
   who holds them, contradictions from stage 3.
4. **Assumptions and limits.** The stage-4 lists, plus the stop reason
   (saturation or budget).
5. **Takeaways.** Actionable, each tied to the finding it rests on.
6. **Open questions.** Sub-questions left open, with what was tried.
7. **Sources.** Reference-style links, each with its tier and date.

Done when every sub-question is answered or listed open, every load-bearing
claim shows its sources or `single-source` label, and the budget was
respected.

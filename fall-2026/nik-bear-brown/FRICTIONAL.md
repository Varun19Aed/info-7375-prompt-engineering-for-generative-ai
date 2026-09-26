# FRICTIONAL — Professor Bear's process log

## Executive summary

**What this is.** The honest process log for the work in this folder, written the way the course asks students to write theirs: what was tried, what went wrong, what changed, and who did what, the human or the AI.

**Why read it.** It's a real example of the log, not a constructed one. It shows the instructor's own work run through the same record students keep.

**What it records so far.** One working session on 2026-09-23, in three parts, and a check on 2026-09-26.
- **The assignment.** An audit of the Reallocation Engine against an old version of its student assignment turned up paths that no longer exist, commands that don't run on a fresh copy, and a scoring signal that counts for nothing. That led to a rewritten 100-point assignment: a recipe plus a rough working prototype, framed around the 3-3-2 split.
- **The demo.** Turning the CV into a facts file, and running the engine's job-board watcher on Figma with that CV. That part hit three points of friction. The first match looked wrong because it was wrong. The results didn't add up to the score because of a real bug. And the demo's first choice of résumé got replaced mid-session.
- **The dream-job recipe.** The folder README now holds an eight-step recipe (Figma first, then similar companies, gaps in my CV) mapped onto Assignment 2, with a first gap table built from quoted posting lines and quoted CV facts.
- **The check (2026-09-26).** The rewritten assignment exists and is still accurate, but it was never pushed, so the version students see still says "modes."
- **The portfolio (2026-09-26).** I decided to rewrite my figma-claude book as a Figma tutorial series, as portfolio evidence for the advocate roles. Then I moved it to a new repo, figma-for-educational-ai: a book, workshops and a YouTube playlist built on my Figma for Education account. There's a plan to review; nothing is drafted yet.
- **My own question.** A first recipe asking whether Figma has advocate or education work on flexible terms. The board's answer is no: both advocate roles are full-time, nothing mentions universities, and nothing is part-time or contract. So it's a networking question.

Every push to GitHub is listed at the bottom with its date and commit note.

---

## Entries

### 2026-09-23 — Auditing the Reallocation Engine and rewriting its assignment as a recipe plus a working prototype

- **Date and what I was working on:** Getting a detailed picture of the Reallocation Engine repository as it stands, using the original 25-point "Mode Design" assignment as the lens, and then turning that into this term's version of the assignment.
- **I tried / expected:** I expected the old assignment to still describe the repo, with maybe a stale path or two.
- **What happened:** It had drifted a long way.
  - **Wrong paths:** the assignment sends students to `modes/` and `modes/RUN_LOG.md`, and neither exists. Modes are now called *recipes* and live in `recipes/`. Student recipes go in `recipes/cases/<term>/`. Students log runs in `logs/runs/` and are not allowed to edit `logs/RUN_LOG.md`.
  - **Already superseded:** there was already a 100-point Summer 2026 successor ("Mode Build"), and this term's live assignment is Greenhouse Watch.
  - **Claims that checked out:** the 80 Days company table has 30,370 rows (the claim was "30K+"), the occupation table has 1,016 rows ("1,000+"), and the Playwright posting-liveness checker exists.
  - **Problems the check turned up:**
    - The role-quality signal has weight 0.0 in the scorer, so the "Cognitive Pivot" layer changes no Apply / Consider / Skip decision.
    - Only samples of the SEC Form D data ship with the repo.
    - `npm run bls:local-wage` fails on a fresh copy: it asks for a requirements file that isn't in the repo.
    - `scripts/sec/validate-h1b-join-sample.py` fails on a fresh copy: it needs a data file that is gitignored and not shipped.
    - `DOMAIN.md` lists both of those as runnable today.
    - `npm run score` overwrites two tracked example files unless it is given `--out-dir`. Running it did exactly that, and the files were restored.
    - The repo's CI calls test scripts in `scripts/test/` that don't exist.
    - The Greenhouse Watch brief links a `course/prerequisites/` folder that isn't in that repo.
    - `status.md` was last updated in June.
  - **Recent skills:** checked across the engine and Madison. The engine's only recent addition is `greenhouse-watch` (added Sep 17, extended Sep 19 to Ashby and SmartRecruiters boards). Madison has had no new skills since its last commit on Jul 2.
- **What I did:**
  - Had the old assignment rewritten as a 100-point, Fall 2026 assignment, `course/assignments/reallocation-engine-recipe-build.md` in the-reallocation-engine.
  - It calls everything a *recipe* now; "mode" survives only in a footnote explaining the rename.
  - The deliverable is **a recipe plus a rough working prototype.** The prototype must read real repo data, write both a JSON log and a Markdown report, label every value as record, model judgment, or your input, handle two named failure cases, and have an offline test. The easiest path is to feed the engine's existing scorer rather than rewrite it.
  - **A new opening section** explains what the engine is: the information-asymmetry problem, the fluency trap, the five kinds of evidence (two of them gates that can veto a role outright), and how the book, scripts, and recipes fit together.
  - **A "Facts about the engine that will bite you" list** covers the eight problems above. The "Before you start" commands include only ones seen to run on a fresh copy.
  - **The 3-3-2 argument** from my February 2026 essay: three hours networking, three building credibility, two researching and applying. The engine automates the research inside the "2," points the networking hours at funded sponsors with no open posting, and building the prototype *is* credibility work.
  - The essay's survey statistics are deliberately **not** carried in as facts. Students must trace any such number to its primary source or label it an assumption.
  - Each result must now say its next action (apply, network, or skip).
  - The domain justification must say which part of the two hours the recipe takes over.
  - A new example recipe, `network-targets`, turns the engine's rejects into a networking list.
- **What Claude or another person contributed:** Claude Code (Opus 5.5) audited the repo, ran every check, found and restored the overwritten files, and drafted the assignment. I set the direction:
  - a detailed summary first;
  - then the 100-point version;
  - rename everything to recipe;
  - require a rough working prototype;
  - add context on what the engine does;
  - frame it with the 3-3-2 argument. The tool can help most with the "2," so students can run a 3-3-2 day instead of applying all day, every day.

  The rubric weights (20 recipe, 20 prototype, 15 justification, 10 worked run, 15 presentation, 20 quartile) were Claude's proposal and are not yet confirmed.
- **What I understand now / still do not understand:** The engine's real product is time. Every skip it justifies is time moved back to networking and building. Still open:
  - the rubric weights;
  - whether role quality should carry weight in the scorer;
  - fixing `DOMAIN.md`, the missing CI scripts, and the broken prerequisite links in the engine repo.
- **Evidence and next step:**
  - Evidence: the assignment is at `course/assignments/reallocation-engine-recipe-build.md` in the-reallocation-engine. It is **not committed there yet**; that repo still needs my go-ahead for each push.
  - Next: confirm the weights and push the assignment; fix `DOMAIN.md` and the CI scripts.

### 2026-09-23 — greenhouse-watch demo on Figma, and the CV as facts

- **Date and what I was working on:** Building a small worked example in my course folder. It runs the Reallocation Engine's `greenhouse-watch` skill (new jobs on one company's board, matched to a résumé) so students can see the recipe-plus-prototype assignment done end to end.
- **I tried / expected:** A two-day watch on Figma's board, using a saved snapshot from 2026-09-19 as the first look and a live fetch on 2026-09-23 as the second. I expected a handful of new postings and one or two matches for an example student.
- **What happened:** Figma posted 11 new jobs in the four days and took down 3. For the example student Aarav, the one match was a **London** machine-learning job, flagged for a Boston F-1 student. The report's reasons for it also didn't add up: the lines summed to 6.0 and the score said 3.5. Partway through, I switched the demo to my own CV as "Professor Bear." With that résumé, **none** of the 11 new jobs matched. Treating the whole board as new, 3 of 160 matched, and the roles I'd actually look at (Designer Advocate, the agentic-experiences researcher) scored 0 and 0.5.
- **What I did:**
  - Had the skill's scoring checked against its rules. The score was right; the report hid one bonus line and printed the title credit twice.
  - Fixed the report lines in the skill and added a test proving the lines now add up to the score. The test failed on the old code and passes on the new; all 23 skill tests pass.
  - Committed and pushed that fix to the-reallocation-engine as `015843d` ("fix(greenhouse-watch): justification lines now sum to the score"), with an entry in its `logs/RUN_LOG.md`. Scores and verdicts from earlier runs are unchanged; only their printed reasons were incomplete.
  - Replaced the example-student runs with Professor Bear runs.
  - Wrote the CV as `facts/professor-bear-cv.json`, with contact details, links, DOIs, grant numbers, and other people's names removed, and derived the matching résumé from it.
  - Linked the duplicate board downloads to the two snapshots instead of storing four copies.
  - After the first push, added `CLAUDE.md` to this folder. It tells Claude Code to log every substantive change here in this file and add a line per push, and it spells out what counts as substantive, so the log stays complete without my having to ask each time.
  - Noticed on GitHub that the CV displayed nicely but the Figma jobs file was one 1.5 MB line. It isn't JSONL. It is ordinary JSON that Greenhouse sends minified, and the skill saved the exact bytes. Since the point of this folder is that students read and check it, I had every JSON file here reformatted indented: the Figma archive and both demo snapshots. The data was checked identical before and after, and the demo re-runs give the same results (152 at baseline; then 11 new, 0 relevant). `CLAUDE.md` now requires readable JSON for everything in this folder.
  - Started `figma/`, a dated archive of Figma's open jobs. The first file, `figma-jobs-2026-09-23.json`, is a fresh live fetch at 20:01 UTC: 160 jobs, the same set as the 19:54 UTC snapshot. Nothing changed in those seven minutes, which is expected; the archive's value comes from the days that follow.
- **What Claude or another person contributed:** Claude Code (Opus 5.5) ran every command, wrote the files, traced the scoring bug to its two causes, wrote the fix and the test, and drafted this entry. I chose the direction:
  - build something simple in my folder;
  - use the greenhouse-watch skill;
  - use my CV with personal information removed, as "Professor Bear";
  - keep the CV as a facts file;
  - keep this log, one line per push;
  - have a folder `CLAUDE.md` make updating this log automatic for any substantive change;
  - keep a `figma/` folder of the current jobs as JSON, named by date;
  - reformat all JSON as readable, because the point is for students to read it and check it;
  - commit the scoring fix in the-reallocation-engine and record it here, with links, as evidence;
  - give standing approval to push this folder after every substantive change, now written into `CLAUDE.md`. No token was needed: git on my machine was already authenticated.

  Later the same day I read `facts/professor-bear-cv.json` in full: accurate, no errors, and I will add more to it later. It is now marked `attested: true`. The job-matching résumé derived from it stays `attested: false`, because its skills list is Claude's selection from the CV and I have not reviewed that separately.
- **What I understand now / still do not understand:** A keyword scheme is honest but narrow. It explains every match, and it can't see that "teaches, runs workshops, builds AI tutors" describes an advocate. Its misses are exactly the roles I'd pick by hand, so the scheme is where students have to do the thinking. Still open:
  - whether the default scheme's rule of dropping every Director role is right for anyone but students;
  - how much a daily watch catches that a weekly one misses (only two snapshots so far).
- **Evidence and next step:**
  - Evidence: the demo is in `greenhouse-watch-demo/` (README, the run records and reports, both board snapshots), the facts file is `facts/professor-bear-cv.json`, the logging rules are in `CLAUDE.md`, and the dated job archive is in `figma/`. The skill fix and its test are in the-reallocation-engine, commit `015843d`.
  - Next: attest or correct the CV conversion; write a Professor Bear scheme (hard location gate, no Director exclusion, teaching-to-advocacy phrases) and re-run; run a third live fetch to get a real daily diff.

### 2026-09-23 — A recipe for my own question: flexible advocate or education work at Figma

- **Date and what I was working on:** Starting a recipe in `figma/README.md` for a question of my own. Does Figma have Designer Advocate or education-advocate work I could do on flexible terms: summer, contract, or part-time; going to universities to run workshops; or developing workshops for Figma?
- **I tried / expected:** I hoped the board would show at least one advocate or education role with flexible terms, or some university-facing work.
- **What happened:** Scanning the 160 postings saved at 20:01 UTC:
  - **Advocate roles:** 2 **Designer Advocate** roles. The one that states its terms is full time, from a US hub, with travel up to 25%. Both list $153,000–$317,000.
  - **Workshops:** *Designer Advocate, Partnerships* is the closest fit. It covers partner events and workshops, and equipping partners to educate their customers.
  - **Universities:** no posting mentions universities or campuses.
  - **Flexible terms:** no posting offers part-time, contract, temporary, seasonal, fixed-term, or freelance terms. The 9 "summer" or "hourly" matches are 8 internships and one full-time role paid hourly.
  - **No field to check:** the Greenhouse data has no employment-type field at all. Terms are only known when the posting text states them.
  - **A script bug:** the first version of the scan missed plurals. "workshop" didn't match "workshops," so the education table showed 5 postings instead of 10. Comparing it against an earlier rough search caught it.
- **What I did:**
  - Had the search written as a small script, `figma/find_roles.py` (offline, standard library only), instead of leaving the counts to a one-off query, so students can re-run it and check every number.
  - Fixed the plural bug and saved the report as `figma/roles-2026-09-23.md`.
  - Wrote the recipe into `figma/README.md`: purpose, inputs, steps, a human gate with three next actions (apply, network, skip), the first run's results, what it can and can't verify, and three open TODOs.
  - Gave the folder README an index.
  - Kept the two relevant postings, both Designer Advocate roles, in `figma/professor-bear-figma.json` alongside a readable `figma/professor-bear-figma.md`. A second small script, `figma/pick_postings.py`, copies chosen postings out of the day's file and uses the same word lists as the scan. The pay first came out as "Range:$153,000—$317,000" with its spaces lost, and each posting's text was one long escaped string in the JSON. Both were fixed before pushing: pay now reads "$153,000–$317,000 (annual base)," and the text is stored as one line per paragraph or bullet.
- **What Claude or another person contributed:** Claude Code wrote the script and the recipe draft, ran the scan, caught the plural bug by comparing against its own earlier search, and checked the missing employment-type field. The question, and what kind of work I want, are mine. So is the decision the recipe leaves open.
- **What I understand now / still do not understand:** The board answers the question honestly, and the answer is "not here." That makes this a networking question, not an application question, which is the 3-3-2 argument applied to my own search. Still open:
  - whether the word lists are right (the draft suggests adding "ambassador," "speaker," and "design education");
  - where, if anywhere, Figma announces contract or university work.
- **Evidence and next step:**
  - Evidence: `figma/find_roles.py`, `figma/roles-2026-09-23.md`, `figma/pick_postings.py`, `figma/professor-bear-figma.json` and `.md`, the recipe in `figma/README.md`, and the saved board `figma/figma-jobs-2026-09-23.json`.
  - Next: review the word lists; decide the next action for the two advocate roles; build the day-over-day diff.

### 2026-09-23 — The dream-job recipe, in steps, for Assignment 2

- **Date and what I was working on:** Turning the Figma work into a general recipe for finding advocate and education jobs: Figma first, later similar companies, then gaps in my CV. I also wanted it to feed Assignment 2 ("Plan Your Madison Project Like a Pro": dream job, gap analysis, PRD, architecture).
- **I tried / expected:** A step list I could follow, with the Figma steps already filled in.
- **What happened:**
  - The folder README now carries the recipe in eight steps:
    0. the CV as facts;
    1. watch one company;
    2. gap analysis;
    3. similar companies;
    4. gaps across roles;
    5. credibility work;
    6. networking;
    7. apply only when the terms fit;
    8. log every run.
  - Each step is marked done, first pass, or planned, and says which Assignment 2 part it feeds.
  - For Part 1, *Designer Advocate, Partnerships* is suggested as the dream job, as a judgment: it's the only role that builds certification and enablement programs and works at workshops. Its top three technical requirements are quoted from the posting.
  - For Part 2, a five-row gap table. A word search of the CV facts found **no** mention of Figma, design systems, tokens, prototyping, certification, enablement, or talks. It did find the Coursera course, the 700+ learner course, the 25+ AI course assistants, the workshops, and conference papers.
  - One claim in Claude's first draft was wrong and was fixed before pushing: the table called me a "full-time" Associate Teaching Professor, but the CV doesn't state hours.
- **What I did:** Directed the recipe's shape (Figma first; then similar companies; then gaps in the CV) and asked for anything from Assignment 2 that would make a better recipe.
- **What Claude or another person contributed:** Claude Code drafted the steps, mapped them onto the assignment, pulled the posting requirements and the CV matches as records, and proposed the gap judgments, the Madison ideas, and a three-agent architecture with an n8n outline. All are labeled as proposals. The "why this role" sentence, the hiring-manager research, confirming the gaps, and the PRD are left for me.
- **What I understand now / still do not understand:** The gap that matters most here isn't a skill. It's the terms: full-time with 25% travel against a teaching job. Skills gaps can be closed with credibility work; the terms gap needs a conversation. Still open:
  - whether the CV undersells public speaking (the original CV names a YouTube channel the facts file doesn't carry);
  - which n8n nodes hold up against n8n's own documentation.
- **Evidence and next step:**
  - Evidence: `README.md` (the recipe and the Assignment 2 table), `figma/professor-bear-figma.json` (the posting quotes), `facts/professor-bear-cv.json` (the CV quotes).
  - Next: write the "why this role" sentence; confirm the gaps; build the Figma board for Assignment 2 by September 25.

---

### 2026-09-26 — The assignment students see still says "modes"

- **Date and what I was working on:** Checking that the Reallocation Engine assignment reflects the recipe rename and the rewrite from September 23.
- **I tried / expected:** I pasted the old 25-point "Mode Design Assignment" and said: "I think these are called recipes rather than modes now. And we made those changes. There should be an update to the assignment reflecting ..." I expected the updated version to be in place.
- **What happened:** The update exists, but it never left my machine.
  - **The rewrite is there.** `course/assignments/reallocation-engine-recipe-build.md` in the-reallocation-engine is the September 23 version. It says "recipe" throughout, and "mode" appears only in its closing note on the rename.
  - **It is still accurate.** Every repo path it cites exists today, except `logs/gate-decisions/` and the full sponsorship data file. The assignment itself lists those two as missing. The engine repo has no commits since September 23.
  - **It was never committed or pushed,** so it isn't on GitHub. The 25-point text I pasted isn't in any local repo, so the copy students see is presumably the one on Canvas.
  - **An unrelated loose end.** In this course's repo, the committed assignment `assignments/assignment-reallocation-engine-recipe-step.md` is deleted in the local working copy, uncommitted. Nothing in this log says why. It was left untouched.
- **What I did:** Pointed out that the assignment still says modes, and that the rename and the rewrite should show up in it.
- **What Claude or another person contributed:** Claude Code (Opus 5.5) found the rewrite, checked each path it cites against the repo, confirmed the engine repo hasn't changed, and spotted the local deletion. I haven't checked those findings yet.
- **What I understand now / still do not understand:** Not yet stated by me.
- **Evidence and next step:**
  - Evidence: `course/assignments/reallocation-engine-recipe-build.md` in the-reallocation-engine (local, uncommitted); this entry.
  - Next, three decisions of mine: whether to push the rewrite to the-reallocation-engine (each push there needs my go-ahead), whether to keep the proposed rubric weights, and whether the 25-point Canvas text gets replaced by the rewrite. Also: why the recipe-step assignment is deleted locally.

### 2026-09-26 — Turning the figma-claude book into a tutorial portfolio for the advocate roles

- **Date and what I was working on:** Acting on the Figma recipe's answer (network, don't apply) by building portfolio work that fits the two Designer Advocate postings.
- **I tried / expected:** I asked what was in my `figma-claude` book, and said: "I want to rewrite this to be a series of tutorials for Figma for education." When Claude asked what "for education" meant, I said: "For my portfolio ... to build examples for applying to these types of roles," and pasted this folder's `figma/` README.
- **What happened:** The book is a finished 100,000-word handbook on the Figma API, in 14 chapters written for design-systems engineers. Most of it doesn't fit a tutorial series as written. The source texts in its `pantry/` and the design-system, token and MCP chapters can be reused.
- **What I did:** Set the goal: tutorials as portfolio examples for the roles in `figma/professor-bear-figma.md`.
- **What Claude or another person contributed:** Claude Code (Opus 5.5) did three things. It surveyed the book. It wrote `TUTORIALS-PLAN.md` in the figma-claude repo: 11 tutorials, each mapped to a quoted posting line, each in four formats (written guide, video, Community file, workshop version), with a Medhavy study screen proposed as the one running example. And it tagged the current handbook `api-handbook-v1` locally, so nothing is lost. I haven't reviewed the plan yet.
- **What I understand now / still do not understand:** Not yet stated by me.
- **Evidence and next step:**
  - Evidence: `TUTORIALS-PLAN.md` and tag `api-handbook-v1` in `bear-textbooks/books/figma-claude` (local, uncommitted); `figma/professor-bear-figma.md`.
  - Next, my GATE 1 calls: the tutorial list, the running example, rewriting in place or starting a new repo, and which pilot tutorial to build first.
- **Later the same day — a new repo instead:** I said: "Create a new repo Figma for educational AI. This will be used for a book, workshops and a YouTube playlist. Using my Figma for Education account, to basically do everything that the account can do that might be useful, particularly around using AI for education and agentic AI and design, including design for engineers and non-designers." I pasted Figma's September 10 email: my educator status is valid for two years, and students re-verify every year through SheerID.
  - **What Claude did (Claude Code, Opus 5.5):** It checked Figma's help pages as of today. As a higher-ed educator I have the Professional plan with AI: 3,000 AI credits a month (no rollover, no top-ups), the Figma agent, Make, one Site, and the MCP server at 200 calls a day. K-12 and high-school accounts get no AI. It created the private repo `nikbearbrown/figma-for-educational-ai` with `PLAN.md` (18 modules in 5 parts, each turned into a chapter, a workshop and a video), `CAPABILITIES.md` (what the account can do, with sources, and rows marked VERIFY to check in the account), `CLAUDE.md` and `research/sources.md`. The earlier `TUTORIALS-PLAN.md` is replaced by it. I haven't reviewed any of it yet.
  - **Next:** my GATE 1 in `PLAN.md`: the modules, the running example, the pilot module (suggested: Figma MCP + Claude Code), when to make the repo public, and a licence.
- **Later the same day — Figma already knows me:** I said: "The CEO of Figma has reached out in the past, so note that," and pasted the January–February 2026 email thread about SheerID verification problems for NEU students. Claude recorded it in the private repo (`FIGMA-RELATIONSHIP.md`): who was on the thread, what I promised (a sign-up video, and videos for engineers and MBA students, including Weave), and what Figma's Education team offered (to review the video). Contact details and the full thread are kept out of this public log. So Module 01 of the plan is now that sign-up video.
- **Then my first real question:** "OK, I have Figma for Education. I'm not a designer. I design agentic systems, but that includes websites and other things. How is Figma for Education useful for me?" Claude's answer is saved in the private repo as `research/why-figma-if-you-are-not-a-designer.md`. In short: for someone who builds agents, Figma is a structured picture of an interface that both people and agents can read and write, through the MCP server with Claude Code. I haven't checked it yet.
- **Then the direction:** "Is one of the earlier things to teach the Figma MCP server? I want to really focus on integrating Claude or Codex or other agentic tools directly with Figma." Claude reordered `PLAN.md` around that. Part 1 is now connect, read and write: set-up, connecting Claude Code, Codex and an editor-based agent, a frame read into code, and the agent writing to the canvas. The design basics come after, each one framed as the fix for a mistake the agent made. There are 19 modules, and the suggested pilot is modules 02–03.
- **Then the MCP server, and a film about it:** I ran `claude mcp add --scope user --transport http figma https://mcp.figma.com/mcp` (it answered "Added HTTP MCP server figma … to user config") and said: "I think the MCP server function works, double check that. Create a show and tell video … on what the Figma MCP server does and does for you, and how somebody with an education account would connect to it," with the show-tell skill.
  - **What Claude found:** the server is registered, but `claude mcp list` says "Needs authentication". I still have to sign in (`/mcp` → figma → Authenticate) in an interactive `claude` session.
  - **What Claude built (Claude Code, Opus 5.5):** a show-tell film in the new repo, `youtube/show-tell-figma-mcp-server/`. It's about 145 seconds, with every claim checked against Figma's docs: reading a frame into code, writing to the canvas (free in beta), the Education limit of 200 calls a day, and the two connection steps. The film stops at the 4K master; staging and publishing are mine to decide. I haven't watched it yet.
  - **Then I said: "Stage and publish it."** Claude staged it and uploaded it unlisted to my @NikBearBrown channel: https://youtu.be/L8XX50b-8y4. It's in a new playlist, "Figma for Educational AI", with captions attached. Making it public is a manual step in YouTube Studio.

---

## Evidence

Where to check each claim in this log. Commits in this repository are listed in the push table below; their IDs are in `git log`, and the links here are added one push later, because a commit can't link to itself.

| What | Where |
|---|---|
| Demo, CV facts, first log | [`bfdb402`](https://github.com/nikbearbrown/info-7375-prompt-engineering-for-generative-ai/commit/bfdb402) — `greenhouse-watch-demo/`, `facts/professor-bear-cv.json`, `FRICTIONAL.md` |
| Figma jobs archive, folder rules | [`1192ab5`](https://github.com/nikbearbrown/info-7375-prompt-engineering-for-generative-ai/commit/1192ab5) — `figma/figma-jobs-2026-09-23.json`, `figma/README.md`, `CLAUDE.md` |
| Fix logged, evidence table, standing push approval | [`9512602`](https://github.com/nikbearbrown/info-7375-prompt-engineering-for-generative-ai/commit/9512602) — `FRICTIONAL.md`, `CLAUDE.md`, `greenhouse-watch-demo/README.md` |
| Whole session logged, CV attested | [`e95cf63`](https://github.com/nikbearbrown/info-7375-prompt-engineering-for-generative-ai/commit/e95cf63) — `FRICTIONAL.md`, `facts/professor-bear-cv.json`, `CLAUDE.md` |
| All JSON indented for reading | [`ad0d76e`](https://github.com/nikbearbrown/info-7375-prompt-engineering-for-generative-ai/commit/ad0d76e) — `figma/figma-jobs-2026-09-23.json`, both demo snapshots, `CLAUDE.md` |
| Recipe started, scan added | [`0130421`](https://github.com/nikbearbrown/info-7375-prompt-engineering-for-generative-ai/commit/0130421) — `figma/README.md`, `figma/find_roles.py`, `figma/roles-2026-09-23.md` |
| Relevant postings kept | [`986f39d`](https://github.com/nikbearbrown/info-7375-prompt-engineering-for-generative-ai/commit/986f39d) — `figma/professor-bear-figma.json`, `.md`, `figma/pick_postings.py` |
| The dream-job recipe | `README.md`: eight steps, gap table, Assignment 2 mapping |
| The Figma advocate / flexible-work recipe | `figma/README.md` (recipe), `figma/find_roles.py` (the scan), `figma/roles-2026-09-23.md` (first run), `figma/professor-bear-figma.json` + `.md` (the relevant postings) |
| CV facts checked by me | `facts/professor-bear-cv.json`: `attested: true`, 2026-09-23, "accurate, no errors; more to add later" |
| The Fall assignment rewrite | `course/assignments/reallocation-engine-recipe-build.md` in the-reallocation-engine (local, not yet committed) |
| The scoring-report fix and its test | [`015843d`](https://github.com/nikbearbrown/the-reallocation-engine/commit/015843d5047dbadff05068495e4c5db5cd9945f4) in the-reallocation-engine — `.claude/skills/greenhouse-watch/scripts/greenhouse_watch.py`, `tests/test_greenhouse_watch.py`, `logs/RUN_LOG.md` |
| The live board fetches | `greenhouse-watch-demo/snapshots/figma-2026-09-23.json` (19:54 UTC) and `figma/figma-jobs-2026-09-23.json` (20:01 UTC), both Figma's API response, indented for reading, with the data unchanged |
| The runs and their reasons | `greenhouse-watch-demo/runs/` and `greenhouse-watch-demo/whole-board/`: one JSON record and one Markdown report per run |

---

## GitHub pushes

One line per push to GitHub: the date and the commit note. The commit ID for each push is in `git log`; a commit can't contain its own ID.

| Date | GitHub note |
|---|---|
| 2026-09-23 | feat(fall-2026): add greenhouse-watch Figma demo, Professor Bear CV facts, and Frictional log |
| 2026-09-23 | feat(fall-2026): add dated Figma jobs archive and folder CLAUDE.md for Frictional logging |
| 2026-09-23 | docs(fall-2026): log the greenhouse-watch fix with commit evidence and standing push approval |
| 2026-09-23 | docs(fall-2026): log the whole session in Frictional and attest the CV facts |
| 2026-09-23 | style(fall-2026): indent every JSON file so students can read and check it |
| 2026-09-23 | feat(fall-2026): start the Figma advocate and flexible-work recipe with a checkable scan |
| 2026-09-23 | feat(fall-2026): keep the relevant Figma postings in professor-bear-figma.json and .md |
| 2026-09-23 | docs(fall-2026): add the dream-job recipe in steps with a first gap analysis for Assignment 2 |
| 2026-09-26 | docs(fall-2026): log that the rewritten Reallocation Engine assignment was never pushed |
| 2026-09-26 | docs(fall-2026): log the plan to rewrite figma-claude as a Figma tutorial portfolio |
| 2026-09-26 | docs(fall-2026): log the new figma-for-educational-ai repo for the book, workshops, and playlist |
| 2026-09-26 | docs(fall-2026): log the Figma relationship note and my first question about Figma for agentic work |
| 2026-09-26 | docs(fall-2026): point the log at the saved answer on Figma for agentic work |
| 2026-09-26 | docs(fall-2026): log the decision to teach the Figma MCP server and agent integration first |
| 2026-09-26 | docs(fall-2026): log the Figma MCP setup check and the show-tell film request |
| 2026-09-26 | docs(fall-2026): log the Figma MCP film going up unlisted on YouTube |

# Hermes Phase -2 Source Register

Continuously maintained (Section 6.1). Schema: Master Plan Section 9.6.
First populated at Stage -2.2 (Skill Discovery), 2026-08-23.

Individual skill pages already carry their own URL/access-date in
`skill-catalog.md` per the Section 9.1 schema; this register exists for
sources whose claims materially inform decisions or are cited across multiple
records — not a duplicate of every skill URL.

---

```
Source ID: SRC-001
Title: Some Claude Skills — Skills Gallery
Type: website
URL: https://someclaudeskills.com/skills
Repository: erichowens/some_claude_skills (referenced, not cloned/inspected)
Author/Organization: Erich Owens, Curiositech
Date Accessed: 2026-08-23
License: Site carries "© 2026 Curiositech" notice; no explicit per-skill license found
Research Domains: DOM-01, DOM-02, DOM-03, DOM-04, DOM-06, DOM-07, DOM-09, DOM-10, DOM-13, DOM-14, DOM-15, DOM-16, DOM-17, DOM-18, DOM-19, DOM-22
Claims Used: Full 181-skill gallery listing (names/descriptions/categories); primary discovery index for Stage -2.2 Campaign SCS
Files Inspected: Gallery index page only at this URL; individual skill pages registered separately in skill-catalog.md (32 of 181 inspected beyond title/description)
Confidence: 70 — direct fetch of the live gallery page, but not cross-verified against the underlying GitHub repo's actual file contents
Notes: Named research input per Master Plan Section 15.1 (Campaign SCS) — not an authority, not a mandatory checklist. 181 total skills confirmed present at access time; no pagination (all shown on one page).
```

```
Source ID: SRC-002
Title: The Checklist Manifesto (Atul Gawande, 2009) — as cited within the Checklist Discipline skill
Type: discussion (secondary citation, not independently fetched)
URL: N/A — cited within https://someclaudeskills.com/docs/skills/checklist_discipline/, not independently accessed
Repository: N/A
Author/Organization: Atul Gawande
Date Accessed: 2026-08-23 (via citing skill page, not the primary work itself)
License: N/A (book, not inspected directly)
Research Domains: DOM-15, DOM-07
Claims Used: Grounding basis for SKL-030 Checklist Discipline's DO-CONFIRM/READ-DO format distinction, "killer items" concept, and forcing-function design; independently-verifiable real-world outcomes referenced (WHO Safe Surgery Checklist trial, Boeing 299 1935 incident, Pronovost central-line protocol)
Files Inspected: None — citation only, not independently verified against the primary source
Confidence: 40 — this is a second-hand citation via the skill's documentation, not a direct read of the primary work; flagged as the reason SKL-030's Evidence Quality is rated High-for-a-skill-source rather than fully independently corroborated. If SKL-030 advances toward Stage -2.5 pattern extraction, independently verifying at least the WHO/Pronovost outcome claims is recommended before treating them as FACT rather than INTERPRETATION (Section P5).
Notes: Registered because this is the single highest-evidence-quality basis found in the whole Stage -2.2 pass (see skill-catalog.md SKL-030) and because Section 12.2's evidence hierarchy places independent technical/historical corroboration above a vendor's own documentation — worth flagging its second-hand status honestly rather than letting the higher confidence bleed into an unverified primary claim.
```

```
Source ID: SRC-003
Title: erichowens/some_claude_skills (GitHub repository)
Type: repository
URL: https://github.com/erichowens/some_claude_skills
Repository: erichowens/some_claude_skills
Author/Organization: Erich Owens, Curiositech
Date Accessed: 2026-08-23 (URL surfaced via WebFetch/WebSearch results citing it; the repository itself was NOT cloned or inspected)
License: Unknown — not inspected
Research Domains: DOM-04 (all Stage -2.2 skill records generally)
Claims Used: None yet — registered as a known, not-yet-inspected candidate for Stage -2.3 (Open Repository Discovery), since every skill in skill-catalog.md traces back to this repo and the evidence-quality note on all 32 records depends on it remaining un-triaged.
Files Inspected: None
Confidence: 0 — placeholder registration only, no claims drawn from it
Notes: This is the actual underlying source code/script layer for everything in skill-catalog.md (the `.py` validation scripts, `init_skill.py`, `package_skill.py`, etc. referenced across multiple skill records were never opened). Per Section 12.2's evidence hierarchy (source code ranks above docs), triaging and, if warranted, deep-auditing this repo at Stage -2.3/-2.4 would materially raise the Evidence Quality ceiling on the entire skill-catalog.md set — currently capped at Medium precisely because this gap exists. Flagging explicitly for Stage -2.3 rather than silently leaving it implicit.
```

# Hermes Phase -2 Rejected Candidates

Continuously maintained (Section 6.1). Schema: Master Plan Section 9.7.
First populated at Stage -2.2 (Skill Discovery), 2026-08-23.

---

```
Candidate ID: REJ-001
Candidate: SKL-018 — Launch Readiness Auditor
Source: SomeClaudeSkills, https://someclaudeskills.com/docs/skills/launch_readiness_auditor/
Reason Rejected: Evaluates whether a software codebase is production-ready to ship (feature completeness, test coverage, blocker triage) — this is a build-process/SDLC concern, not a Hermes runtime capability. None of the 25 active research domains in research-domains.md map to "is a codebase launch-ready." Same category of out-of-scope reasoning already applied at Stage -2.1 to the dropped seeds "Spec-driven development" and "Architecture documentation" (Section 2.4's build-readiness test is a downstream Phase -1/specification concern, not Phase -2 research scope).
Potentially Useful Parts: The 8-dimension health-scoring framework and the Ship-It/Sprint-It/Defer-It/Cut-It triage matrix could plausibly be reused much later, outside Phase -2, as a template for Hermes' own eventual build-readiness review (Section 2.4's North Star) — but that is explicitly out of scope for this phase and not something Phase -2 should pursue or recommend acting on now.
What Would Change the Decision: Nothing within Phase -2's current scope — this would only become relevant if the Owner explicitly expanded scope to include build-process tooling, which would itself require an escalation per Section 5.2 (major research-scope change), not a unilateral Stage -2.2 decision.
Date: 2026-08-23
```

```
Candidate ID: REJ-002
Candidate: SKL-032 — Modern Auth 2026
Source: SomeClaudeSkills, https://someclaudeskills.com/docs/skills/modern_auth_2026/
Reason Rejected: Title and category (Security/DevOps) suggested relevance to DOM-08 (Permissions & least-privilege scoping), but the actual mechanism is end-user consumer authentication (WebAuthn passkeys, OAuth social login, magic links) for people logging into an application. DOM-08's real need is machine-to-machine credential isolation between an agent instance and a social platform's own API, per social page — a completely different problem (no end users are authenticating into anything in Hermes' architecture as described in the raw idea). Zero component of the WebAuthn/OAuth/magic-link mechanism transfers. Registered explicitly as a demonstration of the "do not rate a skill highly because its title sounds relevant" discipline (Section 15.1 / Stage -2.2 rules) — this is a case where inspection past the title/category was necessary to catch a mismatch that a shallow pass would have missed.
Potentially Useful Parts: None identified for Hermes' actual DOM-08 need.
What Would Change the Decision: If Hermes ever needs end-user-facing login (e.g., a web dashboard for the Owner with multi-factor authentication), this skill's OAuth/passkey mechanics would become directly relevant — but that is a different capability than DOM-08 as currently scoped, and would warrant its own domain if it becomes a real Hermes need later.
Date: 2026-08-23
```

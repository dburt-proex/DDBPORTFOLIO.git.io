# Portfolio Source-of-Truth Governance

**Owner:** Drew Donald Burt  
**Effective:** July 19, 2026  
**Status:** Active  
**Public canonical URL:** https://drew-burt-portfolio.dburt30.chatgpt.site  
**Documentation repository:** https://github.com/dburt-proex/DDBPORTFOLIO.git.io

## Decision

The ChatGPT Sites portfolio is the canonical public-facing experience.

This GitHub repository is the canonical portfolio documentation layer. It preserves the evidence map, claim boundaries, public-route registry, supporting briefs, and review history.

Each system's own repository remains authoritative for its code, tests, releases, validation artifacts, and implementation status.

This is a governed consolidation, not a literal codebase merge. The two builds use different architectures and serve different purposes. Keeping both as independently authored public portfolios would create duplicate maintenance, conflicting claims, and unclear visitor routing.

## Authority matrix

| Information | Canonical source | Conflict rule |
| --- | --- | --- |
| Public headline, biography, navigation, calls to action, and page copy | ChatGPT Sites | The live Sites version governs public presentation. |
| Assessment and Governance Lab behavior | ChatGPT Sites deployment | The deployed interaction governs visitor behavior. |
| Portfolio claim registry and maturity boundaries | This repository | Update through versioned Git history or pull request. |
| Project code, tests, releases, and validation status | Canonical project repository | Project evidence overrides portfolio summaries. |
| Résumé facts and direct contact information | Drew Burt | Owner-confirmed information overrides derived copy. |
| Historical public-site implementation | Git history in this repository | History is preserved but is not current public authority. |

## Public route registry

| Public route | Purpose | Evidence authority |
| --- | --- | --- |
| `/` | Positioning and assessment-to-enforcement operating model | This registry plus the linked project repositories |
| `/assess` | Directional 12-control governance diagnostic | Operator Intelligence methodology and the deployed assessment logic |
| `/results` | Deterministic score, confidence, gaps, and next actions | Deployed scoring logic and documented assessment boundary |
| `/lab` | Simulated ALLOW, REVIEW, and HALT control paths | CASA and DiffWall repositories |
| `/systems` | Plain-language system claims and evidence links | Operator Intelligence, CASA, DiffWall, PromptBP, and VIL repositories |
| `/work-with-me` | Role, engagement, and partnership paths | Drew Burt's owner-confirmed availability and contact details |

## Project evidence registry

| System | Portfolio role | Canonical evidence |
| --- | --- | --- |
| Operator Intelligence | Assess and prioritize governance gaps | https://github.com/dburt-proex/operator-intelligence |
| CASA | Govern runtime execution | https://github.com/dburt-proex/CASA-Flagship |
| DiffWall | Govern software and deployment changes | https://github.com/dburt-proex/diffwall |
| PromptBP | Govern instruction structure and validation | https://github.com/dburt-proex/PromptBP |
| Verified Intelligence Layer | Verify and score incoming evidence | https://github.com/dburt-proex/VIL_deterministic_scoring_engine |
| Shared Decision Ledger | Preserve decision evidence and replay context | Evidence implementations documented in CASA and Operator Intelligence |

## Publishing workflow

### Technical or maturity change

1. Verify the new state in the system's canonical repository.
2. Update the evidence registry or supporting brief in this repository.
3. Review the wording for evidence strength, maturity, and unsupported inference.
4. Update the corresponding public Sites content.
5. Confirm that the public link resolves to the correct evidence.

### Public copy or experience change

1. Update and validate the Sites build.
2. Check whether the change affects a documented claim, evidence link, or maturity boundary.
3. If it does, update this repository in the same work cycle.
4. Record the final public URL and relevant GitHub pull request in the change log below.

### Conflict resolution

1. Project-level technical evidence wins for implementation status.
2. GitHub portfolio documentation wins for claim boundaries and evidence mapping.
3. ChatGPT Sites wins for current public wording and visitor behavior.
4. Owner-confirmed personal information wins over all derived summaries.
5. When sources disagree, narrow the public claim until the discrepancy is resolved.

## Synchronization policy

No automatic two-way content synchronization is authorized.

Automatic mirroring would allow public copy to overwrite evidence records or allow stale documentation to overwrite a working public experience. Changes should move through the publishing workflow above so the evidence boundary is reviewed.

Automation may later be added for read-only parity checks, broken-link detection, and change reminders. It should not publish claims without review.

## GitHub Pages role

The GitHub Pages root is a bridge to the canonical Sites portfolio. It should not operate as a second portfolio homepage.

Existing technical briefs and case studies remain available as supporting documentation:

- [AI Governance for Developer Tooling](../governance-developer-tooling.html)
- [Source brief and maturity appendix](ai-governance-developer-tooling.md)
- [Agentic SDLC governance case study](../agentic-sdlc-governance.html)

## Change log

| Date | Change | GitHub record | Public deployment |
| --- | --- | --- | --- |
| 2026-07-19 | Established Sites as public authority and GitHub as versioned documentation authority. | [PR #9](https://github.com/dburt-proex/DDBPORTFOLIO.git.io/pull/9) | [Sites version 10](https://drew-burt-portfolio.dburt30.chatgpt.site) |

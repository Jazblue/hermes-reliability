# Tech Reddit Radar: freshness and publication checklist

## Research freshness
- Prefer stories published or materially updated within the intended reporting window.
- Record original publication date and timezone when available. A Reddit discussion date is not necessarily the date an incident occurred.
- September or older stories are background unless a clearly sourced new development occurred in the current reporting window. Label background explicitly; don't count it as today's news.
- Stop repeating identical failed searches. Record the actual number of searches, not a target number.

## Verification
- Reddit can surface leads; a Reddit post alone does not verify a factual claim.
- For security claims, seek primary sources: vendor advisories, CVE records, CERT notices, official incident statements or project security advisories.
- Save the actual primary-source URL and date checked. A generic homepage doesn't verify a specific claim.
- Use labels: `VERIFIED`, `PARTIALLY VERIFIED`, `COMMUNITY REPORTED`, `UNVERIFIED`. State what evidence is missing.
- If primary verification fails, label the claim accordingly or omit it. Never invent source URLs, dates, CVEs, search counts or validation results.

## Publication gates
1. Research findings are internally consistent and source links open.
2. JSON parses and required keys/types validate.
3. Date matches the intended reporting date.
4. Freshness is checked story by story; older items are labelled background.
5. Git diff reviewed; only intended files changed.
6. Commit and push confirmed; compare local and remote branch tips and ensure clean status.
7. Pages deployment checked separately and live site opened to confirm today's content.
8. Notification describes only checks actually performed.

Valid JSON or a successful Git push alone does not prove the report is current, factually verified or live on Pages.
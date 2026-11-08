# Changelog

## 1.3.2 — 2026-10-20

- Repaired the GitHub Actions workflow structure after an incomplete `main.yml` caused `Required property is missing: run` / Python-as-YAML parser failures.
- Standardized the build workflow name to `.github/workflows/main.yml` and removed the competing `build-list.yml` workflow so one scheduled publisher is responsible for the list.
- Added safe YAML parsing with duplicate-key rejection and structural checks for workflow steps, including a check for exactly one valid `run` or `uses` field per step.
- Moved build-summary generation to `tools/write_summary.py` so summary formatting is no longer embedded in a YAML heredoc.
- Fixed category-floor accounting during online overlap reconciliation: only rules with demonstrable coverage from successfully validated feeds count toward effective coverage; offline bootstrap builds receive zero reference-coverage credit.
- Added distinct published, covered, and effective category counts to reports and the manifest, and made the validator enforce their consistency.
- Added two workflow regression tests (49 offline tests total), and aligned current-facing documentation and generated files to version 1.3.2.
- Regenerated the offline bootstrap, metadata, source inventory, rule-delta report, and bootstrap report. Live feed reconciliation remains pending until the GitHub Actions workflow succeeds.


## 1.3.0 — 2026-10-17

- Added a live output-delta gate: large changes to the published active-rule set stop before publication unless a maintainer explicitly approves after reviewing `reports/rule-delta.json`.
- Added deterministic added/removed rule examples, change ratios, and a machine-readable delta report.
- Added a 40% default review threshold, configurable in `config/reference_feeds.json`.
- Extended the workflow summary and build artifact to include output-delta details.
- Added two Google-domain-scoped search-ad cosmetics recovered from the original list; no global selector expansion was used for these additions.
- Added regression tests for rule-set diffs, metadata-insensitive comparisons, delta-policy configuration, manual override behavior, and dry-run behavior (46 tests total).
- Preserved the offline-bootstrap label and the requirement for a successful live feed build before claiming reconciliation.

## v1.3.0 — reliability and audit hardening

- Fixed the online workflow so it does not validate a stale canonical list before rebuilding it.
- Made the reference-feed baseline versioned so rolling anomaly history can persist between scheduled builds.
- Added a deterministic source-module inventory with per-file hashes, category counts, duplicate detection, and policy checks.
- Expanded GitHub Actions summaries and path triggers for maintenance documentation and reports.
- Kept live source-feed validation explicitly pending until the first successful online build.
- Added explicit partial-online manifest state and made failed-build anomaly reports use the same field name as the GitHub summary.
- Added a guard requiring slash-delimited URL regex rules to be third-party scoped.
- Expanded the offline test suite from 30 to 38 regression tests.

## v1.2.0 — Adaptive maintenance and coverage update

- Expanded modular source inventory from the v1.1.0 baseline with additional ad-delivery, session-replay/user-measurement, narrow third-party AMP measurement path, and explicit ad-slot/widget modules.
- Expanded URL cleanup only with selected recognized attribution identifiers; generic `campaign`, `source`, `referrer`, credential, state, session, redirect and deep-link parameters remain prohibited.
- Expanded reference registry from 28 to 32 entries with HaGeZi Threat Intelligence Full, uBlock Origin Quick Fixes, and two archived Fuck Fuckadblock references. Legacy sources remain optional and are not described as actively maintained.
- Added HTTPS/registry validation for duplicate names/URLs, formats, size caps and groups.
- Added concurrent feed fetching (bounded worker count), bounded transient retries, response/source metadata in reports, strict UTF-8 checks and HTML masquerade rejection.
- Added rolling-median source-count anomaly detection with backward compatibility for earlier baseline records.
- Added atomic output/JSON writes, generated mode metadata, SHA-256 output manifest, and final-rendered-rule validation before publication.
- Added CI summary output and expanded offline regression tests from 22 to 30.
- Removed previously included unbounded cross-site URL regexes that could match generic `track`, `log`, `collect`, `ingest`, `event` or telemetry endpoints across unrelated websites.
- Retained the conservative no-scriptlet/no-CSP/no-socket/no-API-tampering policy.

## 1.1.0 — Previous foundation

- Added ShadowWhisperer Ads and Tracking domain feeds and the OpenPhish Community URL feed as health/hash-only reference.
- Added conservative reference overlap reconciliation, feed count anomaly gates, policy validator and automated GitHub workflow.

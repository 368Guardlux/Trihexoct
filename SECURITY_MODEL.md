# Security and adaptation model — v1.3.2

## Trust boundaries

1. **First-party module files** are reviewed declarative filter text. Every active source rule passes policy checks before compilation.
2. **Reference feeds** are untrusted text fetched through HTTPS. The builder applies size/time limits, validates text format and count thresholds, retries only bounded transient failures, and never executes downloaded contents.
3. **Overlap reconciliation** uses a deliberately small set of proof rules: exact filter matches, simple compatible host coverage, explicit literal query-parameter matches, and approved prefix matches. Complex arbitrary regex/CSS/scriptlet equivalence is not inferred.
4. **The updater** fetches concurrently but processes results in registry order. Per-feed status, checksum, byte count, active-entry count, response metadata and timing are reported.
5. **Anomaly detection** compares feed counts with the rolling median of up to seven prior successful observations (while reading v1 legacy baselines). Suspicious count changes require a human-reviewed dispatch override.
6. **Publication** occurs only after coverage and internal checks pass. Output and JSON metadata are written atomically; the last-known-good baseline is advanced only after a candidate is generated and validated internally. GitHub Actions commits only after the final external linter passes.
7. **The browser** downloads ordinary declarative filters. No subscriber data or browsing history is sent to the project by the rules.

## Prohibited rule classes

The policy rejects global scriptlet injection, API spoofing/mutation, global CSP modification, generic WebSocket/WebTransport blocking, raw IP blocks, `$important` overrides, broad cross-site URL regexes, arbitrary credential/session/redirect/deep-link removal, and cosmetics that hide consent, login, payment, comments, social embeds or video UI. Network filters must be third-party scoped wherever possible.

## Deterministic adaptation, not AI

Trihexoct is not a machine-learning system. It adapts in repeatable, reportable ways to approved feed updates. It does not inspect individual subscribers, learn from personal browser behavior, auto-invent domains, or blindly publish arbitrary issue suggestions. Human review remains required for significant upstream count anomalies and new source-module changes.

## Known limitations

- Some references may be down, changed, archived or return a different valid format. Minimum source-success and group gates prevent publishing from an inadequate sample.
- Optional source failures can yield a successful but partial reconciliation; the report explicitly marks coverage incomplete. A source is never silently treated as successfully checked.
- The included bootstrap list is generated offline and does not imply that a live feed build has passed.
- Static linting cannot prove Brave's exact runtime parser behavior or zero website breakage. Keep backups and use reproducible false-positive reports.
- OpenPhish URL indicators are health/hash-only; a URL on a shared host is not treated as proof that the whole hostname should be blocked.

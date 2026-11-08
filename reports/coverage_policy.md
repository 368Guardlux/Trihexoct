# Coverage and overlap policy — v1.3.2

## Published rule categories

1. Named third-party advertising exchanges, ad servers, DSP/SSP platforms, and attribution services.
2. Named third-party analytics, campaign measurement, session-replay, and telemetry endpoints when the host/path has a clear measurement purpose.
3. Recognized marketing attribution and click identifier query parameters only. Generic authentication, session, user, redirect, referrer, `source`, and deep-link parameters are prohibited.
4. Explicit ad-slot/widget cosmetics and known site-specific sponsored-result selectors. Global consent, login, payment, video, social-content, and generic modal/overlay hiding is excluded.
5. Narrow historical browser-mining indicators as a supplementary category. These rules are not a substitute for security software.

## Overlap reconciliation

The updater fetches approved HTTPS references concurrently and indexes only the rule shapes it can interpret conservatively. It removes a local rule only for an exact filter match, simple compatible hostname coverage, or a recognized attribution-parameter name/prefix. It does not infer equivalence for arbitrary regexes, cosmetic selectors, scriptlets, redirects, CSP, or complex modifiers. Upstream content is never copied wholesale into the generated file.

Feed references are a curated comparison set, not a guarantee that the browser has exactly the same subscriptions enabled. Where coverage cannot be established, Trihexoct keeps the local rule rather than guessing.

## Feed health and anomaly controls

- Registry URLs must use HTTPS, names and URLs must be unique, feed formats must be recognized, and per-source byte caps are enforced.
- Network errors, HTTP 429/5xx, timeouts, and connection failures receive a bounded retry policy; malformed content and invalid UTF-8 are rejected.
- A successful feed must contain enough valid entries for its declared format. Counts are compared with a rolling median of up to seven previous successful observations.
- A large source-count shift blocks publishing until a maintainer reviews the artifact and explicitly approves the anomaly.
- At least ten feeds must succeed overall, EasyList/EasyPrivacy/Peter Lowe are required when `--require-primary` is used, and successful ads/privacy/security group minimums must pass.
- Unit tests, source-policy validation, output category gates, duplicate detection and the output manifest must all pass before the GitHub workflow commits.
- A separate output-delta gate blocks live publication when the candidate changes more than 40% of the prior active rule set. Review `reports/rule-delta.json`; a manual override is explicit and separate from feed-anomaly approval.
- Output is written atomically. Failed fetch or output-delta gates do not replace the published list or advance the last-known-good baseline.

## URL-indicator feeds

The OpenPhish Community feed contains complete phishing URLs rather than a list of universally malicious hostnames. It is observed for source health, size, line-count anomalies and hashes only. Its URL entries are not converted into domain-wide blocks or domain-wide overlap evidence. Respect the publisher's terms; do not redistribute its feed contents.

## Limitations

Overlap reduction is deliberately conservative and can leave safe duplicates rather than risk deleting a useful rule. Static tests are not a complete Brave adblock-rust parser and do not replace live-site testing. Network rules can still affect third-party widgets, surveys, fraud telemetry or embedded services. Keep Brave's own security protections and maintained subscription lists enabled.

# Implementation proposal — not executed

Target (proposed): src/preferences.js and tests/preferences.test.js in the consuming app. No new dependency or backend. Keep a versioned JSON object behind read/write/reset methods. Validate allowed keys and values, and recover to defaults from corrupt data or denied storage. Catch writes that fail; show that settings could not be persisted instead of claiming success. These are engineering choices, not claims made by S1 or S2.

Acceptance: load defaults; save/reload 20 settings; reject unknown keys and invalid values; handle corrupt JSON and denied writes; migrate or reset an unsupported schema version; measure main-thread time on the supported devices before extending the workload. Test on the application's actual origin, not merely a local file. Avoid storing credentials or authorization decisions.

Recovery: reset only this application's namespaced preferences, never clear unrelated origin storage. Switch to in-memory defaults if storage fails. Ask before changing the required persistence or sharing behavior.

Traceability: S1 motivates examining synchronous access; S2 supplies the asynchronous transactional alternative. The comparison in RESEARCH.md drives the adapter and tests, which remain proposed. Open decision: supported browsers and measurable latency budget.

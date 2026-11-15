# Browser preferences: a bounded development decision

Question: how should a browser app persist 20 small, nonsensitive display preferences without a server? This is a synthetic brief, not a customer requirement.

| Alternative | Fit | Cost and limitation |
|---|---|---|
| In-memory state (baseline) | No persistence required | Lost on reload; smallest implementation |
| localStorage | Small persisted settings | Synchronous access; serialize and validate a small record [S1] |
| IndexedDB | Structured records and transactional changes | Asynchronous API, schema and transaction handling [S2] |

Recommendation (design judgment): use localStorage for this narrow brief. Keep a storage adapter so a later requirement can change the persistence mechanism. Neither source establishes a universal size or performance threshold. IndexedDB becomes a candidate if measured blocking or transactional requirements justify it.

Sources: [S1](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API), [S2](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API). Read the relevant overview and synchronous/asynchronous sections on 2026-11-15; no implementation or benchmark was inspected. These are living documents, with no pinned release established. Licensing of documentation does not license an application; this example paraphrases and links to sources.

Results: the source ledger, comparison and proposal share S1/S2 identifiers. No application was implemented or timed. The Muse supplied-summary comparison is an assisted reasoning check, not independent browsing or another coding environment. Compatibility, quota handling and recovery below remain acceptance criteria, not passed tests.

Limits: no sensitive data, synchronization, file-URL guarantees or production reliability claim. Updated 2026-11-15.

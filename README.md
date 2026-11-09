# Development Research Kit

Turn a development question into a source-backed decision and implementation brief.

## Start

Open this folder or attach its files to an AI workspace. Send the text in START.md. The workspace needs browsing for current research and repository access for code-level conclusions. Record unavailable capabilities before proceeding.

## Deliverables

- RESEARCH.md with the question, current environment, alternatives and recommendation.
- SOURCES.csv with source URLs, checked dates, revisions and reading depth.
- IMPLEMENTATION-BRIEF.md with proposed paths, dependencies, validation and recovery.

Complete the research when another developer can trace each material claim to a source and understand the proposed change. Research depth follows the decision, with no fixed repository count.

Version 0.2, 2026-11-10. The files in `examples/native-dialog/` are a completed synthetic research exercise. They are not evidence of a production code change or of cross-workspace compatibility.

## Distribution and invocation

This is a file-based kit. Open or attach the files and send START.md to a compatible workspace. Automatic invocation from a short phrase requires a separately installed and authorized skill or plugin. Workspace permissions and available tools determine access.

The reusable templates were applied to a synthetic decision and checked for source-to-claim traceability. Other coding workspaces, private repositories, model integrations and production changes remain unverified.

## Example

See [`examples/native-dialog/`](examples/native-dialog/README.md) for a source-backed comparison of native HTML `<dialog>` and a custom ARIA dialog. The example identifies its synthetic target and distinguishes documentation review from executed checks.

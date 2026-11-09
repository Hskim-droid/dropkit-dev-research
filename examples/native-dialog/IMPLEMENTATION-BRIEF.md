# Implementation brief: add a modal confirmation

## Target and preserved changes

No actual repository was provided. This is a proposal for a fictional small web application. Before implementation, inspect its instructions, framework, current dialog behavior, supported browsers and existing edits. Preserve its unrelated changes.

## Proposed behavior and paths

If the target is a plain static page, use a native `<dialog>` with a visible heading and `aria-labelledby`; open it with `showModal()` from a labeled button. Provide a visible cancel/close control and focus the action that best matches the task. Test whether the required browser keeps focus inside at both Tab boundaries. The isolated Chrome 147 probe did not; add a boundary guard only if the target runtime reproduces the failure. If the real target uses a framework, follow its existing component conventions while retaining the same behavior. Exact paths remain unknown until the repository is inspected.

Do not add a custom ARIA dialog, dependency, API, database or server unless the inspected constraints require it. Do not put `tabindex` on the `<dialog>` element.

## Dependencies, terms and access

The proposal uses browser HTML and JavaScript APIs only. No third-party package, account, credential, network request, paid service or real data is needed for the probe. Check the target browser policy before release. This research kit's documentation is CC BY 4.0; the isolated example code is MIT. A product's generated code requires its own license decision.

## Acceptance checks

1. Triggering the action opens the modal and makes the background unavailable for interaction.
2. Focus enters an appropriate element; Tab from the last control and Shift+Tab from the first stay inside; Escape closes; focus returns to the invoking control.
3. The visible title names the dialog and a visible close/cancel control is present.
4. Verify a narrow viewport and every browser in the target support policy.
5. Conduct a separate screen-reader check with the target assistive-technology combination; do not infer this from DOM assertions.

## Recovery

Keep changes in a small dialog component and its triggering control. Revert those paths if the acceptance checks fail; preserve the original flow and any unrelated edits. If behavior differs across required browsers, pause and compare a maintained polyfill with a custom implementation before expanding scope.

## Open decisions

- Actual repository and exact target paths.
- Supported browser and assistive-technology combinations.
- Whether the real user flow is modal or non-modal.
- Whether the dialog is a reversible confirmation or a high-consequence action.

# Research decision: native HTML dialog or custom ARIA dialog

**Status:** synthetic research example. No production application was inspected or changed.
**Date:** 2026-11-10.

## Question and decision owner

For a small, new web application that needs a blocking confirmation window, should the first implementation use the native HTML `<dialog>` element or a custom element with `role="dialog"`?

## Existing environment and observed behavior

The scenario is fictional. No repository, browser-support policy, framework, existing modal, or actual user flow was supplied. The sample probe uses plain HTML and JavaScript only. It does not establish compatibility for an actual product.

## Requirements and constraints

- A confirmation must block interaction with the page behind it.
- Keyboard users must be able to enter, move within, and leave the dialog.
- The dialog needs a visible title and a visible close or cancel control.
- Do not add a library or service before an existing project and support policy are known.

## Sources and coverage

Three official documents were opened on 2026-11-10: the WHATWG HTML Living Standard, W3C WAI-ARIA Authoring Practices Guide modal-dialog pattern, and MDN's HTML `<dialog>` reference. Their cited behavior is documentation evidence; it does not prove a target browser or screen-reader combination.

## Alternatives and tradeoffs

| Option | Evidence and fit | Cost and limitation |
|---|---|---|
| Native `<dialog>` with `showModal()` | The [HTML Standard](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-dialog-element) defines the element and modal-opening method; [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog) describes modal dialogs as blocking interaction with the rest of the page (S1, S3). This matches the fictional blocking-confirmation requirement with browser-native behavior. | Initial focus still needs deliberate design. The actual product browser matrix is unknown and must be checked. Styling and unusual workflows may require extra handling. |
| Custom element with `role="dialog"` and `aria-modal="true"` | The [W3C WAI-ARIA APG modal-dialog pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/) defines expected focus entry, contained Tab/Shift+Tab sequence, Escape handling, visible close control, labeling and focus return (S2). | The application must implement and maintain those behaviors, including background inertness, focus management and cleanup. ARIA attributes alone do not implement them. |
| Non-modal native `<dialog>` with `show()` | The [HTML Standard](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-dialog-element) and [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog) distinguish non-modal `show()` from modal `showModal()` (S1, S3). | Does not meet the blocking requirement; consider it only if the real task does not need to block the background. |

## Findings and evidence

1. Use `<dialog>` only for a dialog task; the [HTML Standard](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-dialog-element) cautions against using it for other controls such as tooltips, context menus or list boxes (S1).
2. A modal needs an intentional initial focus target. WHATWG recommends using `autofocus` on the descendant the user should act on, or on the dialog if there is no such descendant (S1).
3. The [W3C WAI-ARIA APG modal pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/) expects focus to move into the dialog; Tab and Shift+Tab remain within it; Escape closes it; and focus normally returns to the invoking control. It also recommends a visible close button and an accessible name tied to a visible title (S2).
4. In the first isolated Chrome 147 headless run, native `<dialog>` without a boundary handler moved focus to `BODY` after Tab from the last button. This failed the APG focus-containment expectation in this probe. Adding an explicit first/last Tab boundary handler made the focused probe pass. This is one browser automation observation, not a general browser-compatibility claim.
5. Native and custom options both need testing against the real browser and assistive-technology combinations. The supplied scenario gives no support matrix, so compatibility for a real product remains unknown.

## Recommendation and conditions

For the fictional small application, begin with native `<dialog>` and `showModal()` (S1), then verify focus containment in the real target browsers against the [W3C pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/) (S2). The isolated test needed a small first/last Tab boundary handler to pass the W3C pattern check; include that guard only if the target runtime reproduces the failure. Give the dialog a visible heading referenced by `aria-labelledby`, choose the initial focus target for the task, include a visible cancel/close control, and verify return focus. Keep a fully custom ARIA dialog as a last option if the actual support matrix or required interaction cannot be met with native behavior.

This recommendation is conditional: inspect the target application and its supported browsers before implementation. Do not copy the isolated probe into a product without that review.

## Uncertainties and next experiment

The source documents were reviewed and the attached isolated probe was run with Chrome 147.0.7727.15 on Mac mini. The first forward Tab boundary failed without a handler; the version with an explicit boundary guard passed. The fictional project still has no real browser policy or assistive-technology matrix. Run the probe in every supported browser; verify open, initial focus, Tab/Shift+Tab, Escape, focus return, visible controls and narrow layout. A browser-only probe cannot establish screen-reader usability. If that test fails in a required environment, investigate a supported polyfill or a custom implementation and compare its maintenance cost before choosing it.

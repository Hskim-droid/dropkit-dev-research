# Native dialog probe results

Run date: 2026-11-10. Host: user-authorized Mac mini (`claireui-Macmini.local`). Browser: Google Chrome 147.0.7727.15, headless mode, opened the local `file://` page directly. Input was sent through Chrome DevTools Protocol; this was not a physical keyboard or screen-reader test.

## First run: native dialog without a focus boundary handler

- A real CDP mouse click opened `showModal()` and focused the `autofocus` Cancel button.
- Tab moved focus from Cancel to Continue.
- A further Tab from Continue moved focus to `BODY`, outside the modal, so the focus-containment check failed.

## Updated probe

The probe added a small first/last Tab boundary handler to the native dialog. Its **5/5 dialog checks passed** in the final shared run. The complete run also contained 29 separate Dashboard + Chat Kit checks, for 34/34 overall. The dialog checks covered initial focus, forward Tab wrap to the first control, reverse Shift+Tab wrap to the last control, Escape close and focus return to the invoking button.

The native dialog probe itself had no document overflow at 390 CSS px. The Dashboard + Chat sample had no document overflow at 320, 390 or 1440 CSS px; its table stayed locally scrollable at the two narrow widths. Other dashboard checks covered keyboard movement through controls, valid/invalid/empty CSV handling and recovery, formula/source row evidence, sample totals, filtering and zero network resources.

The CSV file input was supplied through CDP; the operating system's native file chooser was not opened. The detailed CDP report and dashboard screenshots are archived with the completion work files, not included as public product files. Screen-reader use, physical mobile devices, other browsers, and a real application remain untested.

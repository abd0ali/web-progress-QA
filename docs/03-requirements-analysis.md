# Requirements Analysis — V2.0.3

[← Back to case study](../README.md)

Management asked for usability and reporting improvements for V2.0.3. I reviewed the live site, wrote each request as a testable requirement with acceptance criteria, and designed acceptance tests before development started.

| ID | Type | Requirement | Priority | Acceptance criteria | Tests |
|---|---|---|---|---|---|
| WP-01 | Enhancement | Add a favicon (company logo) to the browser tab | Medium | Logo shown on every page instead of the browser's default globe | TC-FUN-070 |
| WP-02 | New | The in-progress pipes bar fits its section with no scrollbar | High | No horizontal scrollbar at any screen width · part widths proportional to length · very short parts keep a minimum visible width | TC-FUN-071, 072 |
| WP-03 | Enhancement | Consistent pipeline / part terminology | Low | The same term is used on KPI cards, charts and the All Pipes page | TC-FUN-073 |
| WP-04 | New | Column layout of the Events table saved on the server for all users | High | Layout (visible columns, order, widths, sort, filters, grouping) saved per project and per grid · every user sees it on next open · prompt before leaving with unsaved changes | TC-FUN-074, 075, 076 |
| WP-05 | New | Keyboard navigation in the Events table | Low | Arrow, Page and Home/End keys work · Enter opens details and Esc closes them · Ctrl+F focuses search · `?` shows the shortcut list | TC-FUN-077, 078 |
| WP-06 | New | Export uses the saved layout | Medium | Excel and PDF export only the visible columns, in the same order, with the current filters | TC-FUN-079 |

## How I wrote them
- **One behaviour per criterion**, so each criterion is either pass or fail. For example, "No horizontal scrollbar at any screen width" is checked at 1920, 1366 and 1280 px.
- **Edge cases stated up front.** WP-02 says a very short pipe part must stay visible. Without that, a proportional layout would make it disappear.
- **Shared vs per-user state made explicit.** WP-04 states that the layout is stored on the server per project and per grid. That decides how the feature must be built and how it is tested.
- **Dependencies linked.** WP-06 depends on WP-04, so its test case uses a saved custom layout.

The full register, with status tracking and a live summary, is in [WebProgress_Requirements.xlsx](../requirements/WebProgress_Requirements.xlsx).

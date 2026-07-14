# Discovery Plugin: WebForms

Plugin id: `webforms-discovery`

Use when the project contains ASP.NET WebForms.

Detect:

- `.aspx`, `.ascx`, `.master`, `.aspx.cs`, `.ascx.cs`
- event handlers and page lifecycle logic
- validators, grid controls, session usage, view state usage
- server controls and code-behind dependencies

Output notes:

- map pages and controls to rewrite stories
- identify hidden workflow and validation logic
- flag stateful behavior requiring parity validation

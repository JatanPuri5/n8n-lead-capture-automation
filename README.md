# Lead Capture Automation

A personal portfolio demo built with n8n, Google Sheets, and Gmail.

When someone submits a service inquiry, this workflow saves the details to a spreadsheet, sends a personalized confirmation, and notifies the business owner. It uses four standard nodes without a custom backend or an AI agent.

## Business problem

A small business may copy inquiries into a spreadsheet and send acknowledgment emails manually. This demo automates those steps so the owner has a central record and can follow up.

## Workflow

| Order | Node | Purpose |
| --- | --- | --- |
| 1 | Lead Capture Form | Collect required name, email, service, and message fields. |
| 2 | Add Lead to Google Sheet | Append a row containing the submission timestamp and four form fields. |
| 3 | Send Confirmation Email to Lead | Send a personalized acknowledgment to the email entered in the form. |
| 4 | Notify Business Owner | Send the full inquiry to the configured owner. |

The email nodes reference the original form output explicitly. This preserves the inquiry details after Gmail returns its message metadata.

## Files

- `lead-capture-automation.json`: sanitized workflow template for import.
- `sheet-headers.csv`: the five spreadsheet column headers, with no personal data.
- `SETUP.md`: connection and test instructions.
- `REVIEW-AND-TESTS.md`: review findings, evidence, and remaining checks.
- `PORTFOLIO.md`: copy-ready description and a short demo recording outline.

## Verified result and limits

The original workflow and the sanitized template imported as a separate workflow were both manually tested on October 27, 2026, in the same n8n Cloud account.

After configuring credentials, spreadsheet mappings, and the owner email, the imported workflow successfully saved all five values to Google Sheets and delivered both emails with the correct details. Screenshots are included in the screenshots folder.

This is a personal portfolio demonstration, not paid-client work or a production reliability claim. No measured time savings or revenue improvement is claimed.

## Scope

This version does not include deduplication, spam prevention, custom retry handling, or an error-alert workflow. If a node fails, later nodes may not run. In particular, an unsuccessful confirmation email can prevent the owner notification because the nodes run in sequence. Re-running the entire workflow can create duplicate rows or emails.

The form's submission message confirms receipt of the form; it is not proof that every downstream action succeeded. Check the execution result, spreadsheet, and email delivery.

## Public template changes

The original file is unchanged. This copy removes Google credential references, spreadsheet IDs and cached URLs, and workflow/instance/version identifiers. The owner address is now `owner@example.com`; replace it before testing. Node and webhook identifiers were regenerated, and the form path is `lead-capture-portfolio-demo` to distinguish it from the original. Connections, field mappings, email bodies, and node type versions are preserved. The template is inactive and contains no pinned submission data.

Workflow JSON is not a backup of OAuth tokens, spreadsheet contents, email history, or execution logs. A new instance needs its own credentials.

## Documentation

- [n8n export and import](https://docs.n8n.io/workflows/export-import/)
- [n8n Cloud trial](https://docs.n8n.io/manage-cloud/cloud-free-trial/)

Keep an offline export and demo recording. The Cloud trial is time-limited; this package does not require purchasing a subscription to inspect the files.

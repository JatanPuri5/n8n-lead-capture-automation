# Setup and manual test

Keep the original working workflow and original export as your private backup. Import this sanitized template into a NEW workflow if you want to verify the reusable version; do not overwrite your working copy.

## 1. Import

Open a new n8n workflow and use the workflow menu's Import from File option. Choose `lead-capture-automation.json`. Exact menu labels may vary by version. Keep it unpublished while configuring.

The source uses Form Trigger 2.6, Google Sheets 4.7, and Gmail 2.2 node versions. These are node type versions, not the n8n application version. Use an n8n instance supporting these node versions. Import compatibility has not been tested here.

## 2. Prepare Google Sheets

Create a spreadsheet named Lead Capture Demo. In the first row, enter these exact headers in columns A–E:

| A | B | C | D | E |
| --- | --- | --- | --- | --- |
| Submitted At | Full Name | Email | Required Service | Message |

You can also import `sheet-headers.csv`. Keep the data rows empty for the first test.

## 3. Connect the spreadsheet node

Open Add Lead to Google Sheet. Connect your Google Sheets account, then select your spreadsheet and its worksheet tab. Confirm the operation is Append and the mappings are:

| Column | Expression |
| --- | --- |
| Submitted At | `{{ $json.submittedAt }}` |
| Full Name | `{{ $json["Full Name"] }}` |
| Email | `{{ $json.Email }}` |
| Required Service | `{{ $json["Required Service"] }}` |
| Message | `{{ $json.Message }}` |

The JSON already contains these mappings. Recheck them if selecting a new spreadsheet changes the node's column configuration. The timestamp preserves the submitted value and its timezone offset.

## 4. Connect Gmail

Select your Gmail credential in BOTH Gmail nodes. In Notify Business Owner, replace `owner@example.com` in To with an inbox you control. In Send Confirmation Email to Lead, retain the dynamic recipient expression pointing to Lead Capture Form's Email field.

The Gmail credential determines who sends the emails. The To field determines who receives them. For a demo, sender, customer, and owner can use the same account.

## 5. Run one manual test

1. Confirm all four nodes have no pinned/mock data.
2. Click Execute in the workflow editor and open the trigger's test form. Use the test URL shown by the node rather than constructing one.
3. Enter Full Name: Demo Lead 01; Email: an inbox you control; Required Service: Website Development; Message: This is a portfolio automation test.
4. Submit once. This performs real actions: one spreadsheet row and two emails.
5. Check the execution result, all five spreadsheet values, and both received email bodies. Check Spam/Sent if needed.
6. If anything fails, inspect the failed node's error before retrying. Do not rerun the whole workflow blindly, because earlier actions may already have completed.

## 6. Prepare a portfolio demo

Record the workflow canvas, test form, added spreadsheet row, and both emails. Hide personal email addresses and unrelated browser/account content in anything you publish. A short recording plus this reusable template is sufficient for a basic portfolio example; a permanently public form is optional.

If you later choose to publish, review recipients, validation, and abuse controls first. Use the production form URL displayed by n8n and verify a production submission separately. The original screenshots only established a manual test, not a published deployment.

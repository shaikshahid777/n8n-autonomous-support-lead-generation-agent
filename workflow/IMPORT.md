# n8n Workflow Import

The working n8n export is maintained locally as `LMS Topic 11 - Autonomous Support & Lead Generation Agent.json`.

## Import steps

1. Open the n8n instance.
2. Choose Import from File.
3. Select the exported JSON.
4. Reconnect PostgreSQL, Gemini, SMTP, and Slack credentials using your own credential objects.
5. Verify the webhook URL for the target environment.
6. Run the database setup branch if the target database is empty.
7. Execute the sample sales payload from `tests/sample-sales-lead.json`.
8. Verify the customer email, Slack notification, token log, and webhook response.

## Public repository rule

Do not commit an export containing live secrets or private customer data. The repository is intentionally structured so the export can be added after a final secret/privacy review.

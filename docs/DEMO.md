# Demonstration Evidence

## Recorded demonstration

Loom: https://www.loom.com/share/650a95d3571a40d881b3c4c56249b80d

The demonstration covers a live n8n execution of the autonomous support workflow.

## Verified scenario

Test ticket: TCK-5005

The recorded run demonstrated:

- webhook intake
- successful workflow execution
- AI-driven classification/routing
- Slack internal notification in the support channel
- customer email delivery
- successful final response
- green/success execution state across the demonstrated workflow

## Repository note

The Loom recording is linked rather than committed to Git because the local screen recording is large. This keeps the repository lightweight while preserving reviewable evidence.

## Reviewer checklist

1. n8n workflow architecture
2. validation branch
3. PostgreSQL context retrieval
4. Gemini model connection
5. structured AI parsing
6. decision routing
7. customer email
8. Slack notification
9. token usage logging
10. webhook response

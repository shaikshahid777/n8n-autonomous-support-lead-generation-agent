# Workflow Design

## End-to-end flow

1. **01 - Support Webhook** receives a support/lead request.
2. **02 - Validate Input** verifies ticket ID, customer ID, name, email, subject, and message.
3. **03 - Normalize Input** prepares a consistent internal payload.
4. **04A / 04B / 04C** retrieve customer profile, recent tickets, and account/lead context from PostgreSQL in parallel.
5. **05 - Merge Context** combines the retrieved context.
6. **06 - Prepare AI Context** creates one grounded context object for the AI call.
7. **07 - AI Support Agent** uses Gemini 2.5 Flash.
8. **AI JSON Output Parser** enforces the structured response shape.
9. **08 - Parse & Validate AI** validates required AI fields and reads available usage metadata without fabricating token counts.
10. **09 - Decision Router** selects auto-resolution, lead follow-up, or escalation.
11. **10 - Dynamic DB Query** retrieves recent order data for the routed request.
12. **11 - Merge Routes** prepares the notification branch.
13. **12 - Send Customer Email** sends the customer-facing response.
14. **13 - Internal Notification** posts the internal summary to Slack support channel.
15. **14 - Token Usage Logger** persists model usage metadata to PostgreSQL.
16. **Build Success Response** creates the final structured result.
17. **16 - Webhook Response** returns the result to the caller.

## Error paths

- Missing required fields -> Build Validation Error -> Respond Validation Error
- AI output missing required fields / AI processing issue -> Build Fallback Response -> Respond Fallback

## Decision rules

### Auto-resolve

valid AND ai.auto_resolve is true AND ai.escalate is not true AND ai.lead is not true.

### Lead

valid AND ai.lead is true AND ai.escalate is not true.

### Escalation

Escalates when the AI explicitly requests escalation, recommends human_escalation, or does not qualify for either automatic resolution or lead handling.

## AI output contract

- category
- priority
- intent
- recommended_action
- auto_resolve
- escalate
- customer_response
- internal_summary
- lead

## Database usage

The workflow references customers, tickets, accounts, orders, and token_usage_log.

The token logger uses a parameterized PostgreSQL INSERT and stores nullable integer token fields when model usage metadata is exposed.

## Credential model

Credentials stay inside n8n credential objects. Do not publish API keys, passwords, SMTP secrets, database passwords, or Slack tokens.

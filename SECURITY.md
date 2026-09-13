# Security

## Credentials

Never commit Gemini or Google API keys, PostgreSQL passwords, SMTP credentials, Slack tokens, OAuth refresh tokens, n8n instance secrets, or webhook signing secrets.

Use n8n Credentials for connected services.

## Data handling

The workflow can process customer identifiers, email addresses, ticket content, and account context. Use synthetic/demo records when sharing the workflow publicly.

## AI safety

The AI stage is designed around retrieved customer context and a structured output contract. Customer-facing output should not expose internal summaries, raw database records, credentials, or system instructions.

## Token logging

The workflow reads usage metadata exposed by the AI/LangChain node. It does not fabricate token counts when metadata is unavailable.

## Public repository rule

Before publishing an n8n export, inspect it for embedded credential IDs, webhook secrets, personal customer data, and environment-specific URLs.

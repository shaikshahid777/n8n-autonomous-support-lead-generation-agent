# Autonomous Support & Lead Generation Agent

Production-style n8n automation for autonomous customer support, lead qualification, escalation, notifications, and AI usage logging.

## What this project does

An incoming support/lead request enters through a webhook. The workflow validates and normalizes the payload, retrieves customer context from PostgreSQL in parallel, prepares grounded AI context, classifies the request with Gemini 2.5 Flash, validates the structured result, routes the request, sends customer and internal notifications, logs AI usage metadata, and returns a structured webhook response.

## Architecture

POST Webhook
-> Validate Input
-> Normalize Input
-> Parallel PostgreSQL Context Retrieval
-> Merge Context
-> Prepare AI Context
-> Gemini 2.5 Flash AI Agent
-> Structured JSON Parser
-> Parse & Validate AI
-> Decision Router
-> Dynamic DB Query
-> Merge Routes
-> Customer Email + Slack Notification
-> Token Usage Logger
-> Success Webhook Response

Error paths:
- Validation failure -> Validation Error Response
- AI parse/model failure -> Fallback Response

## Core capabilities

- Webhook-driven ticket intake
- Required-field validation
- Input normalization
- Parallel PostgreSQL lookups
- Grounded AI decision-making
- Gemini 2.5 Flash integration
- Structured JSON output validation
- Auto-resolution / lead / human-escalation routing
- Dynamic order lookup
- Customer email notification
- Slack internal notification
- PostgreSQL token usage logging
- AI fallback handling
- Structured webhook responses
- Credential-based secret management in n8n

## AI decision contract

The AI result contains:
- category
- priority
- intent
- recommended_action
- auto_resolve
- escalate
- customer_response
- internal_summary
- lead

The workflow uses these fields to determine whether a request can be resolved automatically, treated as a sales lead, or escalated for human review.

## Data layer

The workflow references:
- customers
- tickets
- accounts
- orders
- token_usage_log

Token usage is read from model/LangChain metadata when available. The workflow does not fabricate token counts.

## Demonstration

Loom recording:
https://www.loom.com/share/650a95d3571a40d881b3c4c56249b80d

The recorded TCK-5005 scenario demonstrated successful workflow execution, customer email delivery, Slack internal notification, and the final structured response.

## Repository structure

- workflow/ - n8n workflow export and import notes
- database/ - schema/setup documentation
- tests/ - reproducible webhook test payloads
- docs/ - architecture and demonstration documentation
- SECURITY.md - credential and public-sharing guidance

## Import

The source n8n export is the file named "LMS Topic 11 - Autonomous Support & Lead Generation Agent.json" generated for the project. Before publishing an export, inspect it for credentials, secrets, private customer data, and environment-specific URLs.

## Security

Never commit API keys, database passwords, SMTP credentials, Slack tokens, OAuth refresh tokens, or n8n secrets. Use n8n Credentials for connected services.

## Author

Shaik Mohammad Shaheed

# Database Layer

The Topic 11 workflow uses PostgreSQL for persistent business context and observability.

## Tables referenced

- `customers` - customer profile/context
- `tickets` - recent support history
- `accounts` - account and lead context
- `orders` - recent order/account activity used by the dynamic query
- `token_usage_log` - AI execution usage metadata

## Query pattern

The dynamic order lookup uses a parameterized query with the customer ID and limits the result set to the five most recent orders.

The token logger uses parameterized values for ticket ID, customer ID, execution ID, model, input tokens, output tokens, total tokens, status, and timestamp.

## Setup

The n8n workflow contains a manual database setup branch for the Topic 11 tables. Run it only in the intended database environment and review the SQL before production use.

# KaS Finance

KaS Finance is a modern personal finance dashboard for tracking balances, transactions, budgets, goals, bills, subscriptions, and AI-assisted financial activity in one responsive web app.

[Live Demo](https://kasfianance.com)

## Highlights

- Secure sign in and account creation flow
- Dashboard overview for bank balance, savings, and credit card debt
- Transaction tracking with filters for type, category, month, tag, and amount
- Budget monitoring by spending category
- Recurring subscription tracker with monthly equivalents and due dates
- Finance assistant for quick natural-language transaction entry
- Responsive mobile authentication screens
- Public showcase repository with sensitive production details removed

## Screenshots

### Mobile Experience

<p>
  <img src="assets/mobile-sign-in.png" alt="KaS Finance mobile sign in screen" width="260" />
  <img src="assets/mobile-sign-up.png" alt="KaS Finance mobile sign up screen" width="260" />
</p>

### Dashboard

![KaS Finance dashboard overview](assets/dashboard-overview.png)

### Transactions

![KaS Finance transaction management screen](assets/transactions.png)

### Budget Assistant

![KaS Finance budget view with finance assistant](assets/budget-assistant.png)

### Subscriptions

![KaS Finance subscriptions tracker](assets/subscriptions.png)

## Tech Stack

### Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS

### Backend

- Supabase
- PostgreSQL
- Node.js

### Deployment & Tools

- Vercel
- GitHub
- GitHub Actions

## Architecture

KaS Finance uses a full-stack architecture with a Next.js client, Supabase authentication and backend services, PostgreSQL persistence, protected API routes, and real-time data workflows for financial activity.

### Architectural Decisions

- **Next.js application layer:** Chosen for a responsive React interface, server-side routing, protected pages, and straightforward deployment on Vercel.
- **Supabase authentication:** Used to keep user identity, session handling, and protected data access centralized.
- **PostgreSQL data model:** Selected for relational financial data where transactions, budgets, subscriptions, and account activity need consistency.
- **User-scoped records:** Financial records are designed around authenticated ownership so each user's dashboard only reads and writes their own data.
- **Server-side validation:** Sensitive mutations such as balance updates, transaction creation, and subscription changes are handled through protected workflows instead of trusting client-only state.
- **Assistant as an input layer:** The finance assistant turns natural-language entries into structured transaction data while keeping the database as the source of truth.

### Public Database Schema Overview

This public repository documents the application data model at a safe level. Exact production migrations, indexes, row-level security policies, internal IDs, and environment-specific configuration are intentionally excluded.

| Area | Purpose | Representative Fields |
| --- | --- | --- |
| `profiles` | Stores user-facing account metadata linked to authentication. | `id`, `email`, `full_name`, `role`, `created_at` |
| `account_balances` | Tracks current bank, savings, and debt balances for dashboard summaries. | `user_id`, `account_type`, `label`, `balance`, `updated_at` |
| `balance_activity` | Records balance changes for audit history and trend charts. | `user_id`, `account_type`, `amount`, `direction`, `note`, `created_at` |
| `transactions` | Stores income, expenses, transfers, categories, tags, and searchable notes. | `user_id`, `type`, `category`, `amount`, `description`, `transaction_date` |
| `budgets` | Defines monthly category limits and spending progress. | `user_id`, `category`, `monthly_limit`, `period_start`, `period_end` |
| `goals` | Tracks savings or payoff goals. | `user_id`, `name`, `target_amount`, `current_amount`, `target_date` |
| `bills` | Tracks upcoming bills and payment status. | `user_id`, `name`, `amount`, `due_date`, `status` |
| `income_sources` | Stores recurring or expected income records. | `user_id`, `name`, `amount`, `frequency`, `next_date` |
| `subscriptions` | Tracks recurring charges, billing cadence, and monthly equivalents. | `user_id`, `name`, `amount`, `billing_cycle`, `next_charge_date`, `status` |
| `assistant_events` | Stores safe assistant interaction metadata for user workflows and import review. | `user_id`, `input_type`, `parsed_result`, `created_at` |

### Performance & Scaling

KaS Finance is structured for live traffic with clear separation between client rendering, protected server workflows, and database-backed financial records.

- Dashboard data is grouped by user and feature area so pages can load focused summaries instead of scanning unrelated records.
- Transaction and activity views are designed around date, type, category, and user ownership filters.
- Balance history is stored separately from current balances so charts and audit trails do not slow down summary reads.
- Subscription and budget calculations use normalized records so recurring totals and monthly progress can be derived consistently.
- Large imports are treated as structured review workflows before they become final transaction records.
- The public repository avoids exposing exact production traffic, private logs, query plans, or infrastructure limits.

### Optimization Metrics Tracked

The production application is monitored using performance and reliability signals that are safe to describe publicly without publishing sensitive telemetry.

| Metric Category | What It Demonstrates |
| --- | --- |
| Page load performance | Measures how quickly authenticated dashboard views become usable. |
| API response time | Tracks latency for protected reads and financial mutations. |
| Database query time | Identifies slow filters, summary reads, and history lookups. |
| Import processing time | Measures how long CSV/PDF-assisted workflows take from upload to review. |
| Error rate | Tracks failed requests, validation issues, and unexpected assistant parsing failures. |
| Deployment health | Confirms production builds, route availability, and post-deploy stability. |

Exact live traffic counts, private monitoring dashboards, and raw production metrics are not included in this public showcase.

## Local Setup

```bash
git clone https://github.com/kkotey14/KaSpublic.git
cd KaSpublic
npm install
npm run dev
```

Create a `.env.local` file with the required environment variables before running the app locally.

## Security

This repository is a public showcase version of KaS Finance. Production secrets, sensitive infrastructure settings, and private backend configuration are not included.

## Roadmap

- AI-powered financial insights
- Advanced analytics dashboard
- Recurring transaction automation
- Budget forecasting tools
- Multi-user collaboration support

## Author

Kingsley Kotey

- Portfolio: [kkotey.com](https://kkotey.com)
- LinkedIn: [Kingsley Kotey](https://linkedin.com/in/kingsley-kotey-476649278)

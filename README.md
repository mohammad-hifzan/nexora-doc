# Investment Platform API

A resilient backend service for evaluating investment portfolios, tracking asset valuations, and processing market transactions. Built as an API-only service emphasizing deterministic state transitions and strict data integrity.

## Architecture & Design Decisions

* **Data Integrity via PostgreSQL:** Uses `db/structure.sql` to leverage native PostgreSQL constraints, transactional advisory locks for balance reconciliation, and composite indexing on time-series valuations.
* **Idempotency & Concurrency:** Financial transactions implement idempotency keys via request headers to prevent double-charging or race conditions during network retries.
* **Background Processing:** Long-running valuation simulations and external API polling run asynchronously off the main request thread.

## Tech Stack

* **Runtime:** Ruby 4.0.x (YJIT enabled)
* **Framework:** Rails (API mode, edge)
* **Database:** PostgreSQL 16+
* **Application Server:** Puma (multi-threaded, cluster mode)
* **Testing:** RSpec, FactoryBot
* **Infrastructure:** Docker (multi-stage build)

## Prerequisites

* Docker & Docker Compose **or** Ruby 4.0+ and PostgreSQL 16+
* Bundler

## Local Setup

1. **Install dependencies:**
   ```bash
   bundle install

## Prepare the database:
Database connection settings live in config/database.yml. Sensitive values are managed via Rails encrypted credentials. The schema is tracked in db/structure.sql.

```
bin/rails db:prepare
```

## Start the application server:

```
bin/rails server
```

## Running Tests
Execute the automated test suite:

```
bundle exec rspec
```

## Docker
Build and run the containerized application:

```
docker build -t investment_platform .
docker run -p 3000:3000 investment_platform
```

## Project Layout

app/models — Domain models, state machines, and business rules

db/ — PostgreSQL migrations and structure.sql

spec/ — RSpec unit and integration test suite

config/ — Application runtime and environment configuration

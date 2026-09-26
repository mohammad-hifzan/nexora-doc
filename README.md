# Investment Platform

A Ruby on Rails API application for tracking and assessing investment
opportunities. This repository contains the domain models, persistence layer,
and test suite for the backend service.

## Tech Stack

- **Ruby** 4.0.6
- **Rails** (edge)
- **PostgreSQL** as the primary datastore
- **Puma** as the application server
- **RSpec** for testing
- **Docker** for containerized builds

## Requirements

- Ruby 4.0.6 (see `.ruby-version`)
- PostgreSQL 9.3+
- Bundler

## Getting Started

Install dependencies:

```bash
bundle install
```

Set up the database (create, load schema, run migrations):

```bash
bin/rails db:prepare
```

Start the server:

```bash
bin/rails server
```

## Configuration

Database connection settings live in `config/database.yml`. Sensitive values are
managed via Rails encrypted credentials and environment variables — never commit
secrets to the repository.

The schema is tracked in `db/structure.sql`. Apply pending migrations with:

```bash
bin/rails db:migrate
```

## Running Tests

```bash
bundle exec rspec
```

## Docker

Build and run the application using the provided `Dockerfile`:

```bash
docker build -t investment_platform .
```

## Project Layout

- `app/models` — domain models and business rules
- `db/` — schema and migrations
- `spec/` — RSpec test suite
- `config/` — application and environment configuration

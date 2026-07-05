# Hacking on Superset

This guide helps new contributors get a local development environment running.
For the full, authoritative contributing documentation, see the
[Apache Superset Developer Portal](https://superset.apache.org/developer_portal/)
and the guides linked from [CONTRIBUTING.md](CONTRIBUTING.md).

## Prerequisites

- Python 3.9+
- Node.js 18+ (manage with [nvm](https://github.com/nvm-sh/nvm))
- npm 9+
- Git

## Clone the repo

```bash
git clone https://github.com/tetratorus/superset.git
cd superset
```

## Python backend

```bash
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate

# Install the package in editable mode with dev extras
pip install -e ".[dev]"

# Initialize the database and create an admin user
superset db upgrade
superset fab create-admin
superset init

# Start the Flask dev server
superset run -p 8088 --with-threads --reload --debugger
```

## Frontend

```bash
cd superset-frontend
npm ci
npm run dev        # starts webpack-dev-server on port 9000
```

Visit `http://localhost:9000` (proxied to the backend on 8088).

## Pre-commit hooks

Pre-commit hooks are required; CI will reject code that doesn't pass them.

```bash
pip install pre-commit
pre-commit install

# Run against staged files
git add .
pre-commit run

# Or run against the entire repo
pre-commit run --all-files
```

## Running tests

```bash
# Python tests
pytest tests/unit_tests/

# Frontend tests
cd superset-frontend
npm run test
```

## Useful links

- [Developer Portal](https://superset.apache.org/developer_portal/) -- full contributor docs
- [Development Setup](https://superset.apache.org/developer_portal/contributing/development-setup) -- detailed environment setup
- [Submitting Pull Requests](https://superset.apache.org/developer_portal/contributing/submitting-pr)
- [Contribution Guidelines](https://superset.apache.org/developer_portal/contributing/guidelines)
- [Code Review Process](https://superset.apache.org/developer_portal/contributing/code-review)

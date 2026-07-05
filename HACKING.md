<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->

# Hacking on Superset

This is a quick-start for contributors who want to get a local development
environment running. It is intentionally short — the authoritative, always
up-to-date documentation lives in the official Superset docs.

## Official documentation

Start here. These guides are maintained by the community and take precedence
over anything in this file:

- [Contributing to Superset](CONTRIBUTING.md)
- [Contributing Overview](https://superset.apache.org/developer_portal/contributing/overview)
- [Development Setup](https://superset.apache.org/developer_portal/contributing/development-setup)
- [Submitting Pull Requests](https://superset.apache.org/developer_portal/contributing/submitting-pr)
- [Contribution Guidelines](https://superset.apache.org/developer_portal/contributing/guidelines)
- [Development How-tos](https://superset.apache.org/developer_portal/contributing/howtos)

## Prerequisites

- Python (see `setup.py`/`pyproject.toml` for the supported versions)
- Node.js and npm (for the frontend, under `superset-frontend/`)
- A running metadata database (SQLite works for local dev; PostgreSQL is
  recommended for anything beyond that)
- Redis (for caching and async queries) if you enable those features
- [`pre-commit`](https://pre-commit.com/) for running lint/format hooks

## Quick start with Docker Compose

The fastest way to get a full stack running locally:

```bash
git clone https://github.com/apache/superset.git
cd superset
docker compose up
```

Then open http://localhost:8088 and log in with `admin` / `admin`.

See the [development setup docs](https://superset.apache.org/developer_portal/contributing/development-setup)
for details and alternatives.

## Local (non-Docker) backend setup

```bash
# Create and activate a virtualenv
python -m venv venv
source venv/bin/activate

# Install Superset and development dependencies (editable install)
pip install -e ".[development]"

# Initialize the metadata database
superset db upgrade

# Create an admin user
superset fab create-admin

# Load example data (optional)
superset load_examples

# Initialize roles and permissions
superset init

# Run the development server
superset run -p 8088 --with-threads --reload --debugger
```

## Frontend setup

```bash
cd superset-frontend
npm ci
npm run dev-server   # serves the frontend against the backend on :8088
```

## Pre-commit hooks

Install the hooks once, then they run automatically on every commit:

```bash
pip install pre-commit
pre-commit install
```

Run all hooks against the whole tree before pushing (CI enforces this):

```bash
pre-commit run --all-files
```

## Running tests

```bash
# Python tests
pytest tests/unit_tests

# Frontend tests
cd superset-frontend && npm run test
```

## Getting help

- Join the [Superset Slack](http://bit.ly/join-superset-slack)
- Browse the [docs](https://superset.apache.org)
- Search existing [issues and pull requests](https://github.com/apache/superset/issues)

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

# Hacking on Apache Superset

This is a quick-start for new contributors. It points to the official
documentation and lists the basic steps for running Superset locally.

## Official documentation

The canonical, always-up-to-date contributor documentation lives in the
Apache Superset Developer Portal:

- [Developer Portal](https://superset.apache.org/developer_portal/)
- [Contributing Overview](https://superset.apache.org/developer_portal/contributing/overview)
- [Development Setup](https://superset.apache.org/developer_portal/contributing/development-setup)
- [Submitting Pull Requests](https://superset.apache.org/developer_portal/contributing/submitting-pr)
- [Contribution Guidelines](https://superset.apache.org/developer_portal/contributing/guidelines)

See also [`CONTRIBUTING.md`](CONTRIBUTING.md) and [`INSTALL.md`](INSTALL.md) at
the repo root. When in doubt, the Developer Portal is authoritative.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and Docker Compose
- [Git](https://git-scm.com/)
- For frontend work: [Node.js](https://nodejs.org/) (see
  `superset-frontend/.nvmrc` for the supported version) and `npm`
- For backend work: Python (see `setup.py` / `pyproject.toml` for the
  supported version)

## Quick start with Docker Compose (recommended)

The fastest way to get a development instance running:

```bash
# Clone your fork
git clone https://github.com/apache/superset.git
cd superset

# Start Superset in development mode with hot reloading
docker compose up
```

Once the containers are healthy, Superset is available at
<http://localhost:8088>. Log in with the default `admin` / `admin`
credentials.

More detail:
[Installing Superset locally using Docker Compose](https://superset.apache.org/docs/installation/docker-compose#installing-superset-locally-using-docker-compose).

## Running the backend and frontend natively

For a fuller development setup (running Flask and the frontend dev server
directly), follow the
[Development Setup](https://superset.apache.org/developer_portal/contributing/development-setup)
guide. The high-level steps are:

```bash
# Backend: create a virtualenv and install dev dependencies
python3 -m venv venv
source venv/bin/activate
pip install -e ".[development]"

# Initialize the metadata database, create an admin user and load examples
superset db upgrade
superset fab create-admin
superset init
superset load-examples  # optional

# Run the backend (defaults to http://localhost:8088)
superset run -p 8088 --with-threads --reload --debugger

# Frontend: in a separate shell
cd superset-frontend
npm ci
npm run dev  # dev server on http://localhost:9000
```

## Pre-commit checks

Superset uses [pre-commit](https://pre-commit.com/) to enforce formatting and
linting. Install and run it before pushing:

```bash
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

CI runs these same checks, so running them locally first saves round trips.

## Running tests

```bash
# Python
pytest tests/unit_tests/

# Frontend
cd superset-frontend
npm run test
```

See the [Development How-tos](https://superset.apache.org/developer_portal/contributing/howtos)
for more on testing, debugging, and other common workflows.
</content>
</invoke>

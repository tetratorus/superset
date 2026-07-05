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

Quick pointers for getting a local development environment up and running.

## Official Contributing Guide

The canonical source for setup instructions, coding standards, and contribution
workflow lives in the Apache Superset Developer Portal:

**<https://superset.apache.org/docs/contributing/>**

Topics covered there include:

- Setting up a Python virtualenv and installing backend dependencies
- Building the frontend with Node.js / npm
- Running the development server
- Database migrations
- Running the test suite (pytest, Jest, Playwright)
- Pre-commit hooks and linting

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/apache/superset.git
cd superset

# 2. Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install Python dependencies
pip install -e ".[dev]"

# 4. Install pre-commit hooks
pre-commit install

# 5. Install frontend dependencies and build
cd superset-frontend
npm ci
npm run build
cd ..

# 6. Initialize the database and start Superset
superset db upgrade
superset init
superset run -p 8088 --with-threads --reload
```

## More Resources

- [CONTRIBUTING.md](CONTRIBUTING.md) — contribution guidelines and Developer Portal link
- [UPDATING.md](UPDATING.md) — notes on breaking changes between releases

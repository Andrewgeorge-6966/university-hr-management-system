# University HR Management System

A full-stack human-resources management application designed around a university organizational model. The project combines a normalized MySQL database with stored routines, triggers, analytical views, a Node.js/Express REST API, and a React dashboard.

> **Project status:** academic full-stack database project. It demonstrates relational modeling and database programming in depth, but its shared-token administration and permissive development CORS configuration should be replaced before production use.

## Highlights

- Models universities, faculties, academic and administrative departments
- Manages employees, jobs, contracts, and active job assignments
- Tracks performance cycles, appraisals, objectives, KPIs, and appeals
- Manages training programs, enrollment, completion, and certificates
- Includes dashboard metrics and visualizations for workforce analysis
- Provides create, read, update, and delete workflows for core HR records
- Ships with synthetic seed data for a complete local demonstration

## Database Engineering

The MySQL script is the core of the project and contains:

| Database object | Count | Purpose |
|---|---:|---|
| Tables | 22 | HR, organization, performance, and training data |
| Stored procedures | 12 | Controlled multi-step business operations |
| Functions | 15 | Reusable calculations and summary metrics |
| Triggers | 6 | Business-rule enforcement and score automation |
| Views | 11 | Reporting-ready workforce and performance datasets |

Examples include weighted KPI-score calculation, employee job assignment, appraisal creation, appeal submission, training enrollment, certificate issuance, salary analysis, and department headcount reporting.

The checked-in seed records are fictional demonstration data. Employee contact details use reserved example domains and deliberately invalid phone-number ranges.

## Architecture

```text
React dashboard
      |
      | Axios / JSON REST API
      v
Node.js + Express
      |
      | mysql2 connection pool
      v
MySQL 8
  ├── normalized relational schema
  ├── stored procedures and functions
  ├── validation and automation triggers
  └── analytical views
```

```text
university-hr-management-system/
├── backend/
│   ├── config/              # MySQL connection pool
│   ├── middleware/          # Administrative write guard
│   ├── routes/              # REST resources and dashboard queries
│   ├── .env.example         # Safe configuration template
│   └── server.js            # Express entry point
├── database/
│   └── schema-and-seed.sql  # Schema, sample data, routines, triggers, and views
├── frontend/
│   ├── public/
│   └── src/                 # React pages, navigation, API client, and styles
└── README.md
```

## Technology Stack

| Layer | Technologies |
|---|---|
| Database | MySQL 8, SQL views, triggers, procedures, and functions |
| Backend | Node.js, Express 4, mysql2, dotenv, CORS |
| Frontend | React 18, React Router 6, Axios, Recharts, React Icons |
| Development | npm, nodemon, Create React App |

## Features

### Organization and employees

- University, faculty, and department hierarchy
- Employee directory, details, and employment status
- Academic and administrative department specializations
- Job definitions, contracts, reporting lines, and assignments

### Performance management

- Annual and mid-year performance cycles
- Employee appraisals and manager comments
- Job objectives and weighted KPI scoring
- Appeals and cross-cycle performance reporting

### Training management

- Training program catalog and approval status
- Employee enrollment and completion tracking
- Training and professional certificate records
- Completion analytics by program

### Dashboard

- Employee, job, department, and training totals
- Gender distribution and department headcount charts
- Recent appraisal summaries
- Performance and training visualizations

## Getting Started

### Prerequisites

- Node.js 18 or 20 LTS with npm
- MySQL 8.0+

### 1. Create and seed the database

The script recreates the local `HR` database, so use it only with a disposable development database:

```bash
mysql -u root -p < database/schema-and-seed.sql
```

### 2. Configure and run the API

```bash
cd backend
npm install
cp .env.example .env
```

Update `.env` with your local MySQL credentials and a long random development admin token:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_local_mysql_password
DB_NAME=HR
DB_PORT=3306
PORT=5001
ADMIN_TOKEN=replace_with_a_long_random_token
```

Start the API:

```bash
npm start
```

Verify it at `http://localhost:5001/api/health`.

### 3. Configure and run the React client

In a second terminal:

```bash
cd frontend
npm install
npm start
```

The browser client opens at `http://localhost:3000` and uses `http://localhost:5001/api` by default. To use a different API host, set `REACT_APP_API_URL` in an ignored frontend environment file.

## API Overview

| Route group | Capabilities |
|---|---|
| `/api/dashboard` | Summary statistics, distributions, and recent appraisals |
| `/api/employees` | Employee listing, details, assignments, performance, and CRUD |
| `/api/jobs` | Job listing, details, assignments, and CRUD |
| `/api/departments` | Organization hierarchy and department CRUD |
| `/api/performance` | Cycles, appraisals, KPI scores, and appeals |
| `/api/training` | Programs, employee training, enrollment, and program creation |

Create, update, and delete operations for employees, jobs, and departments require the `x-admin-token` request header. The frontend lets a developer enter this token for local demonstrations.

## Security and Production Notes

- Real credentials belong only in ignored `.env` files; `.env.example` contains placeholders.
- The current shared admin token is a development control, not a production authentication system.
- The token is stored in browser local storage by the demonstration client. Replace this with authenticated sessions and role-based authorization before deployment.
- Restrict CORS to trusted origins before exposing the API publicly.
- Modernize the Create React App toolchain and upgrade React Router before deployment; the current academic build retains known transitive dependency advisories.
- Add request validation, database migrations, automated tests, audit logging, and HTTPS for production use.
- The SQL setup script drops and recreates the `HR` database. Never run it against production data.

## Portfolio Scope

This repository demonstrates database design, SQL programming, REST API integration, and data-driven UI development. It should be evaluated as an academic portfolio project rather than a production-ready HR platform.

## License

No open-source license has been selected. All rights are reserved unless the project owner adds a license.

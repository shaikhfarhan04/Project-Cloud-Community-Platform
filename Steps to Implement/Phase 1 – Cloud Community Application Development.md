
# **Phase 1 – Cloud Community Application Development**



Phase 1 started

React + Flask + MySQL



We are going to build the actual application first, using a development setup that can later be migrated to AWS without rewriting the application.

**Our first milestone:** A working Cloud Community website with registration, login, resume upload, MySQL persistence and an admin dashboard.

We will use Docker Compose for local development so that the same application components can eventually be deployed to Kubernetes.

## **1. Phase 1 architecture**

**User / Admin Browser**

[http://localhost:3000](http://localhost:3000?utm_source=chatgpt.com)

**React Frontend + Nginx**

Registration • Login • Admin Dashboard

**Flask REST API**

Authentication • Registration • File validation • Admin APIs

**MySQL**

Users and registrations

**Local File Storage**

Resumes and documents

Later: replace local file storage with private Amazon S3; replace local MySQL with Amazon RDS.

### **Technology decisions**

| Component         | Technology                   |
| ----------------- | ---------------------------- |
| Frontend          | React + Vite                 |
| Backend           | Python Flask                 |
| API               | REST                         |
| ORM               | SQLAlchemy                   |
| Database          | MySQL 8                      |
| Authentication    | JWT                          |
| Password security | Werkzeug password hashing    |
| File uploads      | Flask secure upload handling |
| Testing           | Pytest                       |
| Containerization  | Docker + Docker Compose      |
| Source control    | Git + GitHub                 |

We will also implement role-based access control: normal users cannot access admin APIs.

**Important:** This is our development baseline, not yet a production security certification. Before public deployment we will add HTTPS, rate limiting, malware scanning, hardened session/token handling, database migration automation and additional security controls.

## **2. Project folder setup**

The complete downloadable project package is not ready yet: data analysis is temporarily unavailable. It should become available again in approximately 4 hours 19 minutes, although that is only an estimate.

Meanwhile, let's create the project structure directly on your Windows machine.

### **Step 1 – Create the project directory**

Open VS Code terminal and select PowerShell.

Run:

```
F:
cd F:\DevOps-Data

mkdir Cloud-Community-Platform
cd Cloud-Community-Platform

mkdir frontend
mkdir backend
mkdir database
mkdir docs
mkdir scripts
mkdir .github

mkdir .github\workflows
mkdir docs\architecture
```

Your initial folder structure:

```
Cloud-Community-Platform/
│
├── frontend/
├── backend/
├── database/
├── docs/
│   └── architecture/
├── scripts/
└── .github/
    └── workflows/
```

### **Step 2 – Verify installed tools**

Run these commands:

```
git --version
docker --version
docker compose version
node --version
npm --version
python --version
```

You should have:

- Git
- Docker Desktop
- Docker Compose
- Node.js and npm
- Python 3.12 or newer

If any command fails, we will fix that before proceeding.

### **Step 3 – Configure Git**

Initialize the repository:

```
git init
git branch -M main
```

Create `.gitignore`:

```
@'
.env
.env.*
!.env.example
node_modules/
.venv/
__pycache__/
.pytest_cache/
dist/
uploads/
*.log
'@ | Set-Content .gitignore
```

### **Step 4 – Configure our development environment**

Create `.env.example` in the root directory:

```
DB_PASSWORD=change_this_password
DB_ROOT_PASSWORD=change_this_root_password
JWT_SECRET_KEY=change_this_long_random_secret
FLASK_SECRET_KEY=change_this_another_secret
```

We will copy it to `.env` and replace the example values with strong secrets before starting Docker Compose.

Never push `.env` to GitHub.

## **3. Application implementation order**

We will write and test each component independently.

| Step | Component       | Expected result           |
| ---- | --------------- | ------------------------- |
| 1    | React           | Website opens             |
| 2    | Flask           | REST API responds         |
| 3    | MySQL           | Database connection works |
| 4    | Registration    | User data saved           |
| 5    | Authentication  | User can log in           |
| 6    | Resume upload   | File stored locally       |
| 7    | Admin dashboard | Admin can view members    |
| 8    | Docker Compose  | All services run together |

## **4. Initial testing checklist**

Once the application is implemented, these are our acceptance tests:

**Phase 1 acceptance checklist**

0/12 completed

Cloud Community homepage loads on port 3000

Registration form accepts valid user details

Registration rejects invalid email and weak password

Cloud platform selection works

Resume upload accepts PDF, DOC and DOCX

Registration data is saved in MySQL

Duplicate email registration is rejected

User login works

Normal user cannot access admin APIs

Admin can view registered members

Admin can download uploaded resumes

Docker containers restart successfully

## **5. First task for you**

Before we start implementing the individual files, run the following and share the output:

```
Write-Host "===== SYSTEM ====="
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion

Write-Host "===== GIT ====="
git --version

Write-Host "===== DOCKER ====="
docker --version
docker compose version

Write-Host "===== NODE ====="
node --version
npm --version

Write-Host "===== PYTHON ====="
python --version

Write-Host "===== PROJECT ====="
Get-Location
```

**Our next milestone:** Build the React frontend, Flask backend, MySQL database and Docker Compose configuration, with complete working source code.

We will not move to Terraform until the application works locally and passes the acceptance tests. This will give us a proper engineering workflow rather than deploying untested code to AWS.

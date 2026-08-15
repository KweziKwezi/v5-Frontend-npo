# UbuntuConnect — Unified Build

> **Branch:** `FrontEnd-v5-NPO-cases-done` (merged & cleaned)  
> This is the unified version combining all contributors' work with the completed NPO use cases.

---

## 📁 Project Structure

```
UbuntuConnect/
├── backend/                         # .NET 10 Web API
│   └── UbuntuConnectAPI/
│       ├── Controllers/             # All API controllers (Auth, NPO, Individual, Business, Admin, etc.)
│       ├── Data/                    # Entity Framework DbContext
│       ├── DTOs/Requests/           # Request Data Transfer Objects
│       ├── Filters/                 # Swagger auth filter
│       ├── Models/                  # Entity models
│       ├── Properties/              # Launch settings
│       ├── Program.cs              # App entry point (JWT, CORS, Swagger)
│       ├── appsettings.json        # Production config template
│       ├── appsettings.Development.json  # Local dev config
│       └── UbuntuConnectAPI.csproj # Project file
├── frontend/                        # React + Vite + TailwindCSS v4
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/          # Page components (dashboards, auth, landing)
│   │   │   │   ├── NPODashboard.tsx         # ✅ COMPLETE (real API)
│   │   │   │   ├── IndividualDashboard.tsx  # ✅ COMPLETE (real API)
│   │   │   │   ├── BusinessDashboard.tsx    # ⚠️ Mock data (pending API integration)
│   │   │   │   ├── AdminDashboard.tsx       # ⚠️ Mock data (pending API integration)
│   │   │   │   └── ui/                     # shadcn/ui components
│   │   │   └── routes.tsx           # All routes defined
│   │   ├── context/                 # AuthContext (JWT + role-based routing)
│   │   ├── services/                # API service layers
│   │   │   ├── npoService.ts       # ✅ NPO API service (complete)
│   │   │   └── individualService.ts # ✅ Individual API service (complete)
│   │   ├── lib/                     # Axios API client with JWT interceptor
│   │   └── styles/                  # Global styles, theme, fonts
│   ├── package.json
│   └── vite.config.ts
├── database/                        # SQL Server migrations
│   ├── migrations/                  # 002–024 (sequential schema migrations)
│   ├── 000_run_all_migrations.sql   # Master migration runner
│   └── seed_dummy_data.sql          # Realistic seed data with Unsplash images
├── docs/                            # Project documentation
│   ├── 00_PROJECT_CHARTER.md
│   ├── 01_BUSINESS_DOMAIN.md
│   ├── 01_PROJECT_OVERVIEW.md
│   ├── 02_SYSTEM_CONTEXT.md
│   ├── 03_FUNCTIONAL_REQUIREMENTS.md
│   ├── 04_NON_FUNCTIONAL_REQUIREMENTS.md
│   ├── 05_PROJECT_ARCHITECTURE.md
│   ├── 06_DATABASE_ARCHITECTURE.md
│   ├── 07_API_CONTRACT.md
│   ├── 08_BACKEND_ARCHITECTURE.md
│   ├── 09_FRONTEND_ARCHITECTURE.md
│   ├── 10_UI_UX_SPECIFICATION.md
│   └── 11_TESTING_STRATEGY.md
└── .gitignore
```

---

## 🚀 Getting Started

### Prerequisites
- [.NET 10 SDK](https://dotnet.microsoft.com/download)
- [Node.js 18+](https://nodejs.org/) with pnpm
- SQL Server (local or Azure)

### Backend Setup
```bash
cd backend/UbuntuConnectAPI
dotnet restore
dotnet run
```
API will be available at `http://localhost:5275` with Swagger UI.

### Frontend Setup
```bash
cd frontend
pnpm install
pnpm dev
```
App will be available at `http://localhost:5173`.

### Database Setup
Run the migrations in order against your SQL Server instance:
```bash
# Execute 000_run_all_migrations.sql or run each migration file individually
# Then optionally run seed_dummy_data.sql for test data
```

---

## 👥 User Roles & Dashboard Status

| Role | Dashboard | Status | API Integration |
|------|-----------|--------|-----------------|
| NPO | `/npo-dashboard` | ✅ Complete | Full CRUD: Posts, Projects/Fundraisers, Volunteers, Verification, Wallet, Follow System, Supporters |
| Individual | `/individual-dashboard` | ✅ Complete | Discover NPOs, Follow, Volunteer, Donate, Wallet, Community Feed, Profile Management |
| Business | `/business-dashboard` | ⚠️ UI Only | Mock data — needs API service integration |
| Admin | `/admin-dashboard` | ⚠️ UI Only | Mock data — needs API service integration |

---

## 🔑 Authentication Flow
- JWT-based authentication via `/api/Auth/login` and `/api/Auth/register`
- Tokens stored in localStorage
- Auto-redirect to role-specific dashboard on login
- 401 interceptor clears auth state and redirects to login

---

## 📋 What Was Merged

This build combines:
1. **NPO use cases** (fully implemented with real API) — Posts, Comments, Projects/Fundraisers, Volunteer Opportunities, Verification, Wallet/TopUp/Withdraw, Follow/Unfollow NPOs, Supporters view, Discover NPOs, Community Feed
2. **Individual use cases** (fully implemented with real API) — Discover & Follow NPOs, Volunteer Applications, Donations, Wallet, Impact Tracking, Community Updates, Profile Management
3. **Business use cases** (UI scaffold with mock data)
4. **Admin use cases** (UI scaffold with mock data)
5. **Shared infrastructure** — Auth, Wallet, Transactions, Database schema (24 migrations)
6. **Documentation** — Full project docs from charter to testing strategy

# Paisa IQ 💰
### Smart Personal Finance Management for India

Paisa IQ is a personal finance application designed to help users track expenses, manage budgets, monitor savings, analyze spending habits, and make informed financial decisions.

The project aims to combine a premium dark-mode interface, reliable financial calculations, privacy-focused data management, and optional AI-powered financial insights.

## 🚀 Project Goals

- Track income, expenses, transfers, and refunds.
- Monitor monthly spending and savings.
- Create monthly and category-based budgets.
- Analyze financial activity through charts and reports.
- Import and export transactions using CSV.
- Provide personalized spending insights through an optional AI Money Coach.
- Keep financial calculations deterministic and accurate.
- Support Indian currency formatting and the Asia/Kolkata timezone.
- Provide a responsive interface and a reliable Android experience.

## ✨ Core Features

### Dashboard
- Monthly income, expenses, remaining balance, and savings.
- Savings-rate tracking.
- Daily spending and daily-target monitoring.
- Category-wise spending visualization.
- Smart alerts and recent transactions.

### Transactions
- Add, edit, search, and filter transactions.
- Categorize transactions.
- Record payment methods, notes, and tags.
- Support recurring transactions.
- Group transactions by date.

### Budgets
- Set monthly spending limits.
- Create category-specific budgets.
- Track budget utilization.
- Receive alerts at 70%, 90%, and 100% utilization.
- Monitor savings goals.

### Analytics
- Daily, weekly, and monthly spending charts.
- Income-versus-expense comparisons.
- Savings-rate trends.
- Average daily spending.
- Recurring-versus-one-time expense analysis.

### AI Money Coach
- Answer questions about spending patterns.
- Generate understandable financial insights.
- Display suggested questions and insight cards.
- Use deterministic financial calculations as the source of all numerical claims.
- Require explicit user consent before sending financial context to an external AI provider.

**Disclaimer:** Paisa IQ is a financial tracking and educational tool, not a substitute for professional financial advice.

## 🛠️ Technology Stack

The final technology stack must be confirmed by inspecting the existing repository.

### Android Application
The proposed native Android implementation may use:

- Kotlin
- Jetpack Compose
- Material 3
- Navigation Compose
- ViewModel and Kotlin Coroutines
- Room for local persistence
- DataStore for application preferences
- Retrofit or Ktor for API communication
- JUnit for testing

### Backend
The proposed backend architecture may use:

- Python
- FastAPI
- Pydantic
- SQLite or another explicitly configured database
- A deterministic financial calculation and insights service
- An optional Google Gemini integration

### Existing Frontend
If the repository already contains a web frontend, preserve its established architecture unless a documented technical reason justifies a change.

Do not assume every proposed technology is already implemented.

## 🎨 Design System

Paisa IQ uses a premium dark-mode fintech design.

| Token | Value |
|---|---|
| Background | `#0B1020` |
| Surface | `#121A2E` |
| Secondary Surface | `#1A2440` |
| Border | `#26314F` |
| Primary Text | `#F5F7FA` |
| Muted Text | `#8A94A7` |
| Positive | `#C6FF3D` |
| Warning | `#FFA94D` |
| Danger | `#FF5A5F` |
| Information | `#4DA3FF` |

Design requirements:

- Use Inter typography where supported.
- Maintain consistent spacing, typography, and component behavior.
- Use tabular numerals for monetary values.
- Maintain accessible contrast and visible focus states.
- Avoid unnecessary visual clutter.
- Use the existing design tokens as the source of truth.

Refer to `docs/design/` for design-system documentation when available.

## 💱 Financial Data Rules

Financial correctness is a core requirement.

1. Store monetary amounts as integer paise. ₹1 = 100 paise.
2. Never use floating-point arithmetic for monetary calculations.
3. Store timestamps in UTC.
4. Calculate Indian calendar-day and month boundaries using `Asia/Kolkata`.
5. Display Indian currency using grouping such as `₹1,23,456.00`.
6. Display dates in `DD/MM/YYYY` format.
7. Support transaction types: `income`, `expense`, `transfer`, and `refund`.
8. Exclude transfers between a user's own accounts from income, expenses, and savings.
9. Link refunds to their original expenses and subtract refunds from the relevant expense totals. Never count refunds as income.
10. Soft-delete transactions using `deleted_at` and exclude deleted transactions from financial totals.

### Core Calculations

**Monthly expense**

`Monthly expense = eligible expenses − eligible refunds`

**Savings**

`Savings = monthly income − monthly expense`

**Savings rate**

`Savings rate = savings / monthly income × 100`

When monthly income is zero, display the savings rate as `—`.

**Month-over-month change**

`Change % = (current period − previous period) / previous period × 100`

If the previous period's value is zero, display `new` where appropriate.

These calculations must be implemented in a deterministic service layer and covered by automated tests.

## 🔐 Privacy and Security

- Keep API credentials and secrets out of the Android application and source control.
- Use a backend for protected third-party API integrations.
- Default AI consent to OFF.
- Do not send financial information to external AI services without explicit consent.
- Provide clear data export and account-deletion flows.
- Validate inputs on both client and server.
- Use secure authentication and appropriate session handling.
- Never expose private financial records through logs or error messages.
- Do not claim encryption, authentication, or other security controls are implemented until verified.

## 📂 Project Structure

The intended structure may resemble:

```text
paisa-iq/
├── docs/
│   ├── PAISA_IQ_SPEC.md
│   ├── IMPLEMENTATION_PLAN.md
│   ├── TASK_LIST.md
│   └── design/
├── android/
│   └── app/
├── backend/
│   ├── app/
│   ├── services/
│   └── tests/
├── README.md
└── .gitignore
```

Adapt this structure to the actual repository. Do not create duplicate applications or unnecessary directories.

## 🧪 Testing

The project should include tests for:

- Financial calculations and rounding.
- Transfers, refunds, and soft deletion.
- Month boundaries in `Asia/Kolkata`.
- Budget thresholds and duplicate alert prevention.
- Transaction validation.
- API authentication and authorization.
- AI consent enforcement.
- CSV import, duplicate detection, and error handling.
- Android UI states and navigation.
- Offline behavior and data persistence.

Run the relevant test suite after each implementation stage. Report actual test results; never fabricate successful builds or test output.

## ⚙️ Development Workflow

1. Inspect the existing repository and its documentation.
2. Identify the implemented features, missing requirements, and technical constraints.
3. Create `docs/IMPLEMENTATION_PLAN.md` and `docs/TASK_LIST.md`.
4. Review the plan before modifying the application.
5. Implement one stage at a time.
6. Run tests and verify the affected functionality.
7. Update the task list with actual results.
8. Stop for approval before proceeding to the next stage.

Preserve working functionality and minimize unnecessary changes.

## 🗺️ Roadmap

- [ ] Audit the existing codebase.
- [ ] Confirm architecture and implementation plan.
- [ ] Finalize design-system integration.
- [ ] Implement and verify transaction management.
- [ ] Implement budgets and financial calculations.
- [ ] Implement analytics and dashboard insights.
- [ ] Implement authentication and data security.
- [ ] Implement CSV import and export.
- [ ] Add optional AI Money Coach integration.
- [ ] Complete Android integration, where applicable.
- [ ] Run automated tests and usability checks.
- [ ] Prepare production deployment documentation.

Roadmap items should be checked off only after implementation and verification.

## 📌 Project Status

**Status:** In development.

Features, architecture, and deployment readiness must be verified against the current repository. This README describes project goals and proposed implementation choices; it does not claim that unimplemented features are complete.

## 📄 License

No license has been specified yet. Add a license before distributing the project publicly.

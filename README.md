<img width="1280" height="640" alt="SpeciFy-social-preview-transparent" src="https://github.com/user-attachments/assets/48276092-47c2-48eb-a336-cc4a19657b2a" />

# SpeciFy, Scheduling System

Full-stack academic scheduling optimization platform (*full documentation available here → GH Pages*)

---

# 🚨 Problem

Universities struggle to schedule special topics courses due to:

- Uncertain student interest
- Conflicting availability
- Manual coordination overhead

This application solves that by:

- Tracking student interest
- Collecting availability
- Automatically recommending optimal time slots

---

# 🚀 Demo

- Live URL: [www.specify.tools](https://www.specify.tools/)

### Demo Login Credentials

- **Student:** `student{any #, 1 through 10}@g.rwu.edu`
- **Professor:** `prof{any #, 1 through 10}@rwu.edu`

> Demo accounts bypass email verification for testing purposes.

---

# 🏗 Architecture Overview

SpeciFy follows a modern full-stack architecture:

- **Frontend:** Next.js (App Router)
- **Backend:** Next.js Server Actions
- **Database:** PostgreSQL 15
- **ORM:** Prisma
- **Authentication:** NextAuth (Email Magic Link via Resend)
- **Hosting:** Vercel

---

## 🔐 Authentication Flow (Resend Magic Link)

1. User enters university email
2. A secure magic link is sent via Resend
3. User clicks verification link
4. (a) If user exists → session created
4. (b) If user does not exist:
    - Role inferred from email domain
        - `@g.rwu.edu` → Student
        - `@rwu.edu` → Professor
    - User provides name
    - User record created in database
4. (c) If demo user, → demo session created**
6. Session established
7. User redirected to dashboard

---

## High-Level Application Flow

1. User authenticates via magic link
2. Role determined (Student or Professor)
3. Professors create courses via server actions
4. Students express interest via server actions
5. Students submit availability via server actions
6. Scheduling engine aggregates data
7. Optimal time slot is recommended

---

# ✨ MVP Features

## Authentication

- Passwordless login via email magic link
- Role-based access (Student / Professor)
- Automatic role inference from email domain
- Secure session management

## Course Management

- Professors create courses (server actions)
- Students browse open courses
- Course status lifecycle (draft → active → finalized)

## Interest Tracking

- Students express interest via server actions
- Duplicate prevention
- Aggregated interest counts

## Availability Submission

- Predefined weekly time slots
- Interactive schedule grid
- Editable availability

## Scheduling Engine

- Aggregates availability
- Compares against interest threshold
- Recommends optimal time slots

## CSV Exports

- Downloadable Recommendation file
- Downloadable Summary file
- Downloadable Detailed Summary file

---

# 🧠 Design Decisions

- **Next.js** – Unified frontend + server actions backend
- **TypeScript** – Strong typing for maintainability
- **Prisma ORM** – Type-safe queries and schema migrations
- **NextAuth (Email Provider)** – Secure authentication abstraction
- **Resend** – Reliable transactional email delivery
- **PostgreSQL 15** – Stable relational database
- **Vitest** – Fast TypeScript-native testing framework

---

# 🧰 Tech Stack

- Next.js
- TypeScript
- Tailwind CSS
- PostgreSQL 15
- Prisma ORM
- NextAuth
- Resend
- Vitest
- Vercel

---

# 📂 Project Structure

```
/app                → App Router pages and layouts
/app/courses        → Course browsing + UI logic
/app/dashboard      → Student + professor dashboards
/app/generated      → Prisma client (generated output)
/components         → Reusable UI components
/context            → Global session/user providers
/lib                → Prisma singleton, scheduling logic, utilities
/prisma             → Schema, migrations, seed scripts
/scripts            → Dev tooling + environment utilities
/types              → Shared TypeScript definitions
/tests              → Unit + integration tests (Vitest)
/docs               → Documentation and diagrams
```

---

# 🗄 Database Models (Core)

- User
- Course
- Interest
- Availability
- TimeSlot

---

# 🔌 Data Access Layer (Server Actions)

SpeciFy does NOT use a traditional REST API layer.

All mutations and queries are handled via **Next.js Server Actions**.

Core actions include:

- createUser()
- createCourse()
- getCourses()
- expressInterest()
- submitAvailability()
- getScheduleRecommendation()

All database access is performed through a **singleton Prisma client (`getPrismaClient`)**.

---

# 🔐 Security Notes

- Magic link authentication via Resend
- No passwords stored
- JWT-based session management via NextAuth
- Email domain validation for role assignment
- Secrets stored in environment variables
- `.env.local` is gitignored
- No credentials stored in source control

---

# ⚙️ Requirements

- Node.js 18+
- PostgreSQL 15+ (Supabase recommended)
- npm >=9 (or yarn)
- Next.js 16+
- TypeScript
- Prisma
- Resend account

---

# 🛠 Local Development Setup

## 1. Clone repository

```
git clone https://github.com/ZDowntime/SpeciFy.git
```

---

## 2. Install dependencies

```
npm install
```

---

## 3. Configure environment variables

Create `.env.local`:

```
DATABASE_URL=
EMAIL_SERVER=
EMAIL_FROM=
RESEND_API_KEY=
NEXTAUTH_SECRET=
NEXTAUTH_URL=http://localhost:3000
```

---

## 4. Run migrations

```
npx prisma migrate dev
```

---

## 5. Start development server

```
npm run dev
```

---

# 🧪 Testing (Vitest)

Run tests:

```
npm run test
```

Watch mode:

```
npx vitest
```

Coverage:

```
npx vitest run --coverage
```

Core flows tested:

- Authentication logic
- Role inference
- User creation
- Course creation (server actions)
- Interest submission (server actions)
- Availability submission (server actions)
- Scheduling algorithm

---

# 🗺 Roadmap

- Week 1 – Setup
- Week 2 – Authentication
- Week 3 – Course Management
- Week 4 – Interest Tracking
- Week 5 – Availability
- Week 6 – Scheduling Engine
- Week 7 – UI Polish
- Week 8 – Deployment

---

# 🚧 Known Limitations

- Assumes fixed weekly recurring time slots
- No timezone support
- No real-time updates

---

# 🔮 Future Enhancements

- Email notifications
- Advanced filtering
- Analytics dashboard
- Admin dashboard

---

# 📜 License

© 2026 Joel G. Vidal. All rights reserved. – See `LICENSE`

---

# 👥 Author

- **Rome Vidal**
    - Email: `romev.dev@gmail.com`
    - GitHub: [romevidal](https://github.com/romevidal)

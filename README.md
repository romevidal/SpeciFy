<img width="1280" height="640" alt="SpeciFy-social-preview-transparent" src="https://github.com/user-attachments/assets/48276092-47c2-48eb-a336-cc4a19657b2a" />

# SpeciFy Scheduling System

**Full-stack academic scheduling optimization platform (all source code is hosted in a private repository).**

Click here to view the **[Live Documentation / Final Report](https://romevidal.github.io/SpeciFy/)** or visit **[www.specify.tools](https://www.specify.tools/)** for the live demo.

---

# 🚨 Purpose

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

- **Student:** `student9@g.rwu.edu`
- **Professor:** `prof10@rwu.edu`

> Demo accounts bypass email verification for testing purposes following the above format using any number between 1 and 10.

---

# 🏗 Architecture Overview

SpeciFy follows a modern full-stack architecture:

- **Frontend:** Next.js ( App Router )
- **Backend:** Next.js ( Server Actions )
- **Database:** Supabase ( PostgreSQL 15 )
- **ORM:** Prisma Adapter ( Custom APIs )
- **Authentication:** NextAuth & Resend ( Email Magic Link )
- **DevOps:** GitHub Actions ( CI/CD Pipeline )
- **Hosting:** Vercel & GitHub Secrets

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
3. Professors create courses
4. Students express interest/submit availability
5. Scheduling engine aggregates data
6. Professors receive viewable analytics and downloadable datasets

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

- Downloadable Recommended Dataset
- Downloadable Selected Dataset
- Downloadable Full Dataset

---

# 🧠 Design Decisions

- **Next.js** – For a quick-start and unified frontend + backend (via server actions)
- **TypeScript** – For increased reliability and maintainability (via static typing)
- **Prisma ORM** – For type-safe querying and schema migrations
- **NextAuth (Email Provider)** – Secure authentication abstraction through domain specification
- **Resend** – For reliable transactional email delivery
- **PostgreSQL 15** – For a stable relational database
- **Vitest** – For it's fast TypeScript-native testing framework

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
- ...

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
- ...

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

# ⚙️ Environment Requirements

- Node.js 18+
- PostgreSQL 15+
- npm >= 9
- Next.js 16+
- TypeScript
- Prisma
- Resend
- Vitest

---

# 🧪 Testing (Vitest)

Core flows covered:

- Authentication logic
- Role inference
- User creation
- Course creation (server actions)
- Interest submission (server actions)
- Availability submission (server actions)
- Scheduling algorithm
- ...

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
- No notifications

---

# 🔮 Future Enhancements

- Email notifications
- Advanced filtering
- Analytics dashboard
- Admin dashboard
- Full mobile accessibility

---

# 📜 License

© 2026 Joel G. Vidal. All rights reserved. – See `LICENSE`

---

# 👥 Author

- **Rome Vidal**
    - Email: `romev.dev@gmail.com`
    - GitHub: [romevidal](https://github.com/romevidal)

# Collabifyy

Collabifyy is a platform connecting **Creators** and **Brands** for seamless collaboration. This project is built as a full-stack application using modern web technologies, designed for performance, type safety, and scalability.

## Tech Stack

* **Frontend:** React, TypeScript, Tailwind CSS, Vite
* **Backend:** Node.js, Express, Nodemailer (SMTP)
* **Database:** PostgreSQL (Neon DB), Drizzle ORM
* **Validation:** Zod (Shared schemas between front/back)
* **Authentication:** Google OAuth, Passport.js

---

## Project Structure

The project follows a monorepo-style structure to keep frontend and backend types in sync.

```text
├── client/                 # Frontend (React)
│   ├── src/
│   │   ├── components/     # Reusable UI components (buttons, cards)
│   │   ├── pages/          # Full page views (Landing, Dashboard)
│   │   ├── hooks/          # Custom React hooks (useAuth, etc.)
│   │   └── lib/            # Utilities & API client
│
├── server/                 # Backend (Node/Express)
│   ├── routes.ts           # All API endpoints defined here
│   ├── email.ts            # Email sending logic (Nodemailer)
│   └── storage.ts          # Database operations layer
│
├── shared/                 # Code shared between Frontend & Backend
│   └── schema.ts           # DB Tables & Zod Validation Schemas

```

---

## Getting Started

Follow these steps to set up the project locally.

### 1. Prerequisites

* Node.js (v18 or higher)
* npm (comes with Node)
* Git

### 2. Clone and Install

```bash
# Clone the repository (Use your fork if contributing!)
git clone [https://github.com/PushkargithubCSE/Collabifyy.git](https://github.com/PushkargithubCSE/Collabifyy.git)
cd Collabifyy

# Install dependencies for both client and server
npm install

```

### 3. Environment Setup (.env)

Create a `.env` file in the root directory. You will need the following credentials:

```env
# Database Credentials
DATABASE_URL=postgresql://user:password@host/dbname?sslmode=require

# Google OAuth (For Login)
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_CALLBACK_URL=http://localhost:5173/api/auth/callback/google

# Email Service (Gmail SMTP)
GMAIL_USER=your_email@gmail.com
GMAIL_APP_PASSWORD=your_app_password_here

```

### 4. Run the Development Server

This command starts both the Backend (Express) and Frontend (Vite) concurrently.

```bash
npm run dev

```

* **Frontend:** `http://localhost:5173`
* **Backend:** `http://localhost:5173/api`

---

## Database Management

We use **Drizzle ORM**. You rarely need to touch raw SQL.

* **Update Schema:** If you edit `shared/schema.ts` (e.g., adding a new field), run this to sync the database:
```bash
npm run db:push

```



---

## Key Features & Implementation

### 1. Waitlist System

* **Flow:** User submits form -> Data validated via Zod -> Saved to DB -> Confirmation Email sent.
* **Code Location:**
* Frontend: `client/src/pages/WaitlistPage.tsx`
* Backend: `server/routes.ts` (`POST /api/waitlist`)
* Email Logic: `server/email.ts`



### 2. Authentication

* Users sign in via Google.
* Session-based auth is handled via `server/replitAuth.ts` and `passport`.
* **Important:** Localhost login requires the `GOOGLE_CALLBACK_URL` to point to port 5173.

---

## Git Workflow (How to Contribute)

1. **Fork** the repository to your own GitHub account.
2. **Clone** your fork locally.
3. **Create a Branch** for your task:
```bash
git checkout -b feat/add-new-button

```


4. **Commit** your changes with clear messages:
```bash
git commit -m "feat: added new button to dashboard"

```


5. **Push** to your fork:
```bash
git push origin feat/add-new-button

```


6. **Open a Pull Request** on the main repository.

---

## Troubleshooting

* **Port 5173/3000 conflicts:** If `npm run dev` fails, check if another node process is running.
* **Email not sending:** Ensure `GMAIL_APP_PASSWORD` is correct and not your regular login password.
* **Redirect loop on Login:** Check your `GOOGLE_CALLBACK_URL` in `.env`.

```

### How to Add This:
1.  Create a file named `README.md` in your project folder (if one exists, overwrite it).
2.  Paste the content above.
3.  Run these commands to save it to your repo:

```bash
git add README.md
git commit -m "docs: add comprehensive README for project onboarding"
git push origin master

```
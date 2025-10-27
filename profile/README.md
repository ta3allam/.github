# 🧭 Ta3allam — Open Arabic–English Learning Platform

> **Ta3allam** is an open-source bilingual learning library — built to make quality education accessible across the Arabic world.  
> Fully self-hostable, scalable, and powered by modern web technologies.

![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)
![Supabase](https://img.shields.io/badge/Supabase-Postgres%20%7C%20Auth%20%7C%20Storage-3fcf8e?logo=supabase)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.x-38b2ac?logo=tailwind-css)
![Cloudflare](https://img.shields.io/badge/Cloudflare-CDN-orange?logo=cloudflare)
![License](https://img.shields.io/badge/License-MIT-blue)

---

## 📖 Table of Contents
- [1. Core User Roles](#1-core-user-roles--permissions)
- [2. Tech Stack](#2-tech-stack-mvp-v03)
- [3. User Flows](#3-user-flows-mvp-level)
- [4. MVP Feature Scope](#4-mvp-feature-scope)
- [5. Architecture](#5-architecture)
- [6. Localization](#6-localization-arabic-first)
- [7. Deployment Plan](#7-deployment--sovereignty-plan)
- [8. Contribution Model](#8-contribution-model)
- [9. Roadmap](#9-roadmap)
- [10. Vision](#10-vision)
- [License](#license)
- [Contributors](#contributors)

---

## **1. Core User Roles & Permissions**

| Role | Capabilities |
|------|---------------|
| **Guest** | Browse public lessons, categories, and resources |
| **Student** | Access full content, attempt quizzes, track progress |
| **Admin** | Manage lessons, categories, users, and uploads |

> *(Teacher role reintroduced in v0.4)*

---

## **2. Tech Stack (MVP v0.3)**

| Layer | Technology | Reason |
|-------|-------------|--------|
| **Frontend** | Next.js 15 (App Router) + TailwindCSS + DaisyUI | SEO, SSR/SSG for performance, RTL-ready UI |
| **Backend** | Supabase (Postgres + Auth + Storage) | Serverless, scalable, cost-efficient |
| **Hosting** | Vercel (App) + Cloudflare CDN | Fast edge delivery and global caching |
| **Auth** | Supabase Auth (Email/OTP) | Secure login, future OAuth integration |
| **Storage** | Supabase Storage + Cloudflare cache | Efficient PDFs, images, lesson media |
| **CI/CD** | GitHub Actions + Vercel Previews | Automated secure deployment |
| **Monitoring** | Sentry + Supabase Logs | Error tracking & metrics |
| **Localization** | `next-intl` / `next-i18next` | Arabic-first, LTR fallback |

---

## **3. User Flows (MVP-Level)**

**Guest**
1. Browse categories and lessons  
2. View lesson previews  

**Student**
1. Register / Log in  
2. Access full lessons  
3. Attempt quizzes  
4. Track completion  

**Admin**
1. Upload lessons (Markdown + media)  
2. Manage quizzes, categories, users  
3. Monitor submissions  

---

## **4. MVP Feature Scope**

✅ Guest & Student roles  
✅ Supabase Auth (email)  
✅ Markdown lessons  
✅ Quizzes (MCQ / True-False)  
✅ Lesson search & categories  
✅ Arabic RTL + English UI  
✅ Admin panel (CRUD)  
✅ Cloudflare CDN  

🚫 No AI / live chat / analytics (yet)

---

## **5. Architecture**

### 🧩 System Overview

```mermaid
graph TD
    subgraph "Frontend - Next.js (Vercel)"
        A[Lesson Browser]
        B[Quiz Interface]
        C[Admin Dashboard]
    end

    subgraph "Backend - Supabase"
        D[(PostgreSQL DB)]
        E[(Auth Service)]
        F[(Storage)]
    end

    subgraph "Infrastructure"
        G[Cloudflare CDN]
        H[GitHub Actions CI/CD]
    end

    A --> D
    B --> D
    C --> D
    A --> E
    B --> E
    C --> E
    C --> F
    D --> G
    E --> G
    F --> G
    H --> A
````

### 🧱 Class Diagram

```mermaid
classDiagram
    class User {
        +UUID id
        +string name
        +string email
        +string role // guest | student | admin
    }

    class Lesson {
        +UUID id
        +string title
        +string slug
        +string language
        +text markdownContent
        +UUID authorId
        +string categoryId
    }

    class Quiz {
        +UUID id
        +UUID lessonId
        +string title
        +json questions
    }

    class Attempt {
        +UUID id
        +UUID userId
        +UUID quizId
        +json answers
        +int score
    }

    User "1" --> "0..*" Attempt
    Lesson "1" --> "0..*" Quiz
    Quiz "1" --> "0..*" Attempt
```

---

## **6. Localization (Arabic First)**

* RTL layout via Tailwind’s `[dir="rtl"]`
* Consistent bilingual UX (Arabic / English)
* Arabic typography: *Tajawal*, *Noto Sans Arabic*
* Auto direction-switching for mixed content

---

## **7. Deployment & Sovereignty Plan**

**MVP Deployment**

* Frontend → Vercel
* Backend → Supabase
* CDN & DNS → Cloudflare
* CI/CD → GitHub Actions

**Future Self-Hosted Setup**

* PostgreSQL + PostgREST + MinIO
* Docker Compose orchestration
* Caddy reverse proxy (TLS)
* Replace hosted auth with self-managed JWT

---

## **8. Contribution Model**

* Lessons live in `/content/lessons/[lang]/[slug].md`
* Contributors add lessons or update metadata via PRs
* Admins review + publish via dashboard
* Lesson versions stored and tracked in Supabase

---

## **9. Roadmap**

| Version  | Focus                                 | Status         |
| -------- | ------------------------------------- | -------------- |
| **v0.1** | Core setup (Next.js, Supabase, CI/CD) | ✅ Done         |
| **v0.2** | Auth + Basic Admin panel              | ✅ Done         |
| **v0.3** | Markdown lessons, quizzes, analytics  | 🚧 In Progress |
| **v0.4** | Teacher role + institutions           | ⏳ Planned      |
| **v0.5** | AI-enhanced search & recommendations  | 🔜 Planned     |

---

## **10. Vision**

> “Ta3allam is built to democratize education in the Arabic world — sovereign, open, and bilingual.”
> Free for learners, self-hostable for institutions, and transparent for contributors.

---

## 🪪 License

Released under the **MIT License**.
See [`LICENSE`](./LICENSE) for details.

---

## 👥 Contributors

| Name                  | Role                     |
| --------------------- | ------------------------ |
| **MHA**             | Lead Architect & Founder |
---

**© 2025 Ta3allam Academy** — *Learn Today, Lead the future.*

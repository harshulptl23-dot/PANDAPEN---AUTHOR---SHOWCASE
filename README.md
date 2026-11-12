# 🐼 PandaPen — Full-Stack Web Novel & Publishing Platform

![Next.js](https://shields.io)
![TypeScript](https://shields.io)
![Tailwind CSS](https://shields.io)
![Deployed on Vercel](https://shields.io)

🔗 **Live Website:** [https://pandapen-pandapen-s-projects.vercel.app/](https://pandapen-pandapen-s-projects.vercel.app/)

> **Note:** This repository serves as a public architectural overview and case study for the PandaPen web application. The source code and story manuscripts are maintained in a private repository to protect original creative works and publishing credentials.

---

## Overview

**PandaPen** is a custom-engineered web novel platform and bespoke Content Management System (CMS) built with **Next.js (App Router)**, **TypeScript**, and **Tailwind CSS**. 

The platform was designed to solve two core problems:
1. **Distraction-Free Immersive Reading:** Providing readers with a fast, responsive, dark-themed reading environment tailored for long-form fantasy fiction.
2. **Streamlined Author Publishing:** Eliminating the friction of manual file formatting by providing a secure, browser-based admin portal to draft, edit, and organize chapters into structured Markdown files.

---

## Key Architectural Features

### 1. Reader Experience & Atmospheric UI
* **Custom Design System:** Built using CSS custom properties (`--void`, `--charcoal`, `--blue-mist`) paired with *Playfair Display* serif headings and *Inter* body copy to reduce eye strain during long reading sessions.
* **Interactive Constellation Engine (`ConstellationCanvas.tsx`):** A fixed HTML5 canvas background rendering subtle ambient particles across the viewport, engineered to automatically disable when `prefers-reduced-motion` is detected for accessibility.
* **Editorial Typography:** Custom CSS rules for chapter prose (`chapter-content`), featuring automatic drop-caps on opening paragraphs and glowing scene-break dividers.
* **Dynamic Story & Chapter Routing:** Nested Next.js dynamic routes (`/stories/[slug]/[chapter]`) that parse Markdown frontmatter and render chapters with zero client-side bloat.

### 2. Bespoke Markdown CMS & Admin Portal
* **Cookie-Based Authentication (`/api/admin/auth`):** Protects the author dashboard behind an access-code login screen, issuing `httpOnly`, `SameSite=Strict`, `Secure` session cookies with an 8-hour expiration window.
* **RESTful Chapter Management (`/api/admin/chapters`):** Implements full `GET`, `POST`, `PUT`, and `DELETE` route handlers to manage story chapters directly from the browser.
* **Automated File & Frontmatter Generation:** Parses and serializes YAML metadata (`title`, `publishedAt`) via `gray-matter`, automatically calculating sequential, zero-padded filenames (e.g., `001-beyond-familiar-walls.md`).

### 3. Monetisation & Compliance
* **AdSense Integration (`AdUnit.tsx`):** Modular, non-intrusive ad placements integrated via Next.js `<Script>` with `afterInteractive` loading strategy to preserve Core Web Vitals.
* **Dedicated Legal & Community Routes:** Includes a dedicated `/privacy` policy page, `/contact` hub, and thematic custom `not-found.tsx` (404) error handling.

---

## Project Structure

The codebase follows the Next.js App Router architecture, separating routing, reusable UI components, data-fetching utilities, and flat-file Markdown storage:

```text
pandapen/
├── app/
│   ├── about/
│   │   └── page.tsx              # Platform & lore overview
│   ├── admin/
│   │   ├── dashboard/
│   │   │   └── page.tsx          # Server-protected CMS dashboard view
│   │   └── page.tsx              # Admin access-code authentication screen
│   ├── api/
│   │   └── admin/
│   │       ├── auth/
│   │       │   └── route.ts      # Session cookie login & logout handlers
│   │       └── chapters/
│   │           └── route.ts      # CRUD API for Markdown chapter files
│   ├── contact/
│   │   └── page.tsx              # Reader & enquiry contact page
│   ├── privacy/
│   │   └── page.tsx              # Privacy & cookie disclosure page
│   ├── stories/
│   │   ├── [slug]/
│   │   │   ├── [chapter]/
│   │   │   │   └── page.tsx      # Dynamic chapter reader view
│   │   │   └── page.tsx          # Story overview & chapter index
│   │   └── page.tsx              # Main story library catalog
│   ├── globals.css               # Design tokens, drop-caps, & responsive utilities
│   ├── layout.tsx                # Root shell (Navbar, Footer, Canvas, Analytics/Ads)
│   ├── not-found.tsx             # Custom atmospheric 404 page
│   └── page.tsx                  # Landing page (Hero, Featured Stories, CTA)
├── components/
│   ├── AdminDashboard.tsx        # Client-side chapter editor & management UI
│   ├── AdUnit.tsx                # Modular Google AdSense wrapper
│   ├── ConstellationCanvas.tsx   # HTML5 ambient particle background
│   ├── Footer.tsx                # Site navigation & copyright footer
│   ├── Navbar.tsx                # Responsive top navigation bar
│   └── StoryCard.tsx             # Reusable story preview card
├── content/
│   └── where-secrets-find-us/    # Structured Markdown chapter manuscripts
│       ├── 001-beyond-familiar-walls.md
│       ├── 002-strangers-and-roommates.md
│       └── ...
├── lib/
│   └── stories.ts                # Metadata registry & gray-matter parsing helpers
├── next.config.js                # Next.js configuration
├── tailwind.config.ts            # Custom colour palette & font family extensions
└── vercel.json                   # Vercel deployment configuration
```

---

## Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Framework** | Next.js (App Router, Server Components, Route Handlers) |
| **Language** | TypeScript |
| **Styling** | Tailwind CSS + Custom CSS Variables |
| **Content Engine** | Markdown + `gray-matter` (YAML Frontmatter) |
| **Authentication** | Next.js `cookies()` API (`httpOnly` session tokens) |
| **Deployment & Hosting** | Vercel |

---

## Future Technical Roadmap

- [ ] **Git-Backed / Database Storage:** Transition chapter persistence from local filesystem writes to a serverless database or GitHub Octokit API integration for live mobile publishing in production.
- [ ] **Reader Preferences:** Persist custom font sizes, line spacing, and reading progress via `localStorage`.
- [ ] **Interactive Chapter Reactions:** Add lightweight, low-latency reader reactions at the end of each chapter.

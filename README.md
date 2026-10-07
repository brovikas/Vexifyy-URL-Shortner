# ⚡ Serverless URL Shortener

A fast, scalable URL shortening service built with React, Vercel Serverless Functions, and MongoDB. Convert long URLs into clean short links with automatic QR code generation — deployed at the edge with zero server management.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/brovikas/Serverless-URL-Shortener)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)

---

## 📌 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Deployment](#deployment)
- [Screenshots](#screenshots)
- [Future Enhancements](#future-enhancements)

---

## Overview

The Serverless URL Shortener transforms long, unwieldy URLs into compact, shareable links using randomly generated 8-character slugs. Every shortened URL is backed by MongoDB for persistence and comes with a generated QR code for instant mobile sharing.

```
https://vexifyy.vercel.app

```

---

## Features

| Feature | Description |
|---|---|
| 🔗 **URL Shortening** | Generates a unique 8-character slug for any valid URL |
| ↗️ **Instant Redirect** | Seamlessly redirects short links to the original destination |
| 📱 **QR Code Generation** | Auto-generates a scannable QR code for every shortened link |
| ✅ **URL Validation** | Rejects malformed or invalid URLs before storage |
| ☁️ **Serverless Backend** | Powered by Vercel Functions — no server to manage or maintain |
| 📐 **Responsive UI** | Fully optimized for desktop, tablet, and mobile |

---

## Tech Stack

**Frontend**
- [React.js](https://react.dev/) — UI framework
- [Vite](https://vitejs.dev/) — build tool and dev server
- [Tailwind CSS](https://tailwindcss.com/) — utility-first styling
- [Axios](https://axios-http.com/) — HTTP client

**Backend**
- [Node.js](https://nodejs.org/) — runtime
- [Vercel Serverless Functions](https://vercel.com/docs/functions) — API layer

**Database**
- [MongoDB](https://www.mongodb.com/) — document store
- [Mongoose](https://mongoosejs.com/) — ODM / schema modeling

**Utilities**
- `qrcode` — QR code generation
- React Hooks — state and side-effect management

---

## Architecture

```
User
 │
 ▼
React Frontend  (Vite + Tailwind)
 │
 ▼  POST /api/shorten
Vercel Serverless Function
 │         │
 │    Validate URL
 │    Generate slug
 │         │
 ▼         ▼
MongoDB  ←  Store { slug, originalUrl, createdAt }
 │
 ▼
Return short URL + QR code to client

────────────────────────────────────
GET /:slug  →  Lookup slug  →  301 Redirect
```

---

## Project Structure

```
Serverless-URL-Shortener/
│
├── api/                  # Vercel Serverless Functions
│   ├── shorten.js        # POST — create short URL
│   └── [slug].js         # GET  — resolve and redirect
│
├── config/               # Database connection
├── models/               # Mongoose schemas
├── public/               # Static assets
│
├── src/
│   ├── components/       # React components
│   ├── App.jsx
│   └── main.jsx
│
├── .env.example
├── .gitignore
├── vercel.json           # Vercel routing config
├── vite.config.js
├── package.json
└── README.md
```

---

## Getting Started

### Prerequisites

- Node.js `>= 18.0.0`
- A [MongoDB Atlas](https://www.mongodb.com/atlas) cluster (free tier works)
- [Vercel CLI](https://vercel.com/docs/cli) (optional, for local serverless emulation)

### Installation

**1. Clone the repository**
```bash
git clone https://github.com/brovikas/Serverless-URL-Shortener.git
cd Serverless-URL-Shortener
```

**2. Install dependencies**
```bash
npm install
```

**3. Configure environment variables**

Copy the example file and fill in your values:
```bash
cp .env.example .env
```

```env
MONGODB_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/urlshortener
BASE_URL=http://localhost:5173
```

**4. Start the development server**
```bash
npm run dev
```

The app will be available at `http://localhost:5173`.

> **Note:** To test serverless functions locally, use `vercel dev` instead of `npm run dev`.

---

## Deployment

The project is designed for one-click deployment on [Vercel](https://vercel.com).

**Steps:**

1. Push your project to a GitHub repository.
2. Go to [vercel.com](https://vercel.com) → **New Project** → import your repo.
3. Add the following environment variables in the Vercel dashboard:

   | Key | Value |
   |-----|-------|
   | `MONGODB_URI` | Your MongoDB connection string |
   | `BASE_URL` | Your Vercel deployment URL (e.g. `https://your-app.vercel.app`) |

4. Click **Deploy**.

Vercel automatically handles routing via `vercel.json` and deploys serverless functions from the `/api` directory.

---

## Learning Outcomes

This project covers the following full-stack concepts:

- React.js component architecture and hooks
- Serverless function design and deployment
- REST API development and URL routing
- MongoDB schema modeling with Mongoose
- QR code generation in a web context
- Environment variable management
- CI/CD via Vercel's GitHub integration
- Git workflow and version control best practices



## License

This project is open source and available under the [MIT License](LICENSE).

<div align="center">

# ⚡ InvoiceFlow

### The Enterprise-Grade Invoice Management Platform

[![Live Demo](https://img.shields.io/badge/🌐_Live_Demo-invoiceflow--orpin.vercel.app-7c3aed?style=for-the-badge&labelColor=0b1326)](https://invoiceflow-orpin.vercel.app)
[![Next.js](https://img.shields.io/badge/Next.js-16-000?style=for-the-badge&logo=next.js)](https://nextjs.org)
[![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://expressjs.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://mongodb.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://typescriptlang.org)

<br/>

> **Create, send, and automate beautiful invoices.**  
> Track payments, manage inventory, generate PDFs — and scale across teams — all from one unified platform.

<br/>

[🚀 Get Started](#-quick-start) · [📖 Features](#-features) · [🏗️ Architecture](#-architecture) · [⚙️ Tech Stack](#%EF%B8%8F-tech-stack) · [🔥 Innovations](#-unique-innovations)

---

</div>

<br/>

## 🚀 Project Overview

**InvoiceFlow** is a full-stack, multi-tenant invoice management system built for modern businesses. It combines a premium glassmorphic UI with a battle-hardened Node.js backend to deliver an end-to-end billing experience — from invoice creation and automated recurring billing to Razorpay payment collection and real-time financial analytics.

### Who is it for?

| Persona | How InvoiceFlow Helps |
|---------|----------------------|
| **Freelancers** | Create professional invoices in seconds, send via email, get paid online |
| **Small Businesses** | Manage clients, products, expenses, vendors, and team members in one place |
| **Agencies & Teams** | Multi-tenant workspaces with role-based access (Admin · Accountant · Viewer) |
| **Enterprises** | RESTful API (v1), webhook integrations, and automated billing pipelines |

<br/>

## 🌐 Live Demo

| Environment | URL |
|-------------|-----|
| **Frontend (Vercel)** | [invoiceflow-orpin.vercel.app](https://invoiceflow-orpin.vercel.app) |
| **Backend API (Render)** | [invoiceflow-agxy.onrender.com/api](https://invoiceflow-agxy.onrender.com/api) |

> **Demo Credentials:** Register a free account on the live site to explore all features instantly.

<br/>

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          CLIENT LAYER                                       │
│                                                                             │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │                    Next.js 16 (App Router)                           │   │
│  │  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌──────────────┐  │   │
│  │  │  Landing    │  │  Auth      │  │  Dashboard │  │  Payment     │  │   │
│  │  │  Page       │  │  (Login/   │  │  (Route    │  │  Portal      │  │   │
│  │  │  (SSR)      │  │  Register) │  │  Group)    │  │  (/p/inv/*)  │  │   │
│  │  └────────────┘  └────────────┘  └─────┬──────┘  └──────────────┘  │   │
│  │                                        │                            │   │
│  │  ┌─────────────────────────────────────┴──────────────────────────┐ │   │
│  │  │              Shared Services Layer                              │ │   │
│  │  │  Zustand Auth Store │ Axios Interceptors │ Token Refresh        │ │   │
│  │  └────────────────────────────────────────────────────────────────┘ │   │
│  └──────────────────────────────────────────────────────────────────────┘   │
│                                    │ HTTPS                                  │
└────────────────────────────────────┼────────────────────────────────────────┘
                                     │
┌────────────────────────────────────┼────────────────────────────────────────┐
│                          API LAYER │                                        │
│                                    ▼                                        │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │                    Express.js + TypeScript                           │   │
│  │                                                                      │   │
│  │  ┌─── Middleware Pipeline ───────────────────────────────────────┐   │   │
│  │  │ Helmet → CORS → Rate Limiter → Mongo Sanitize → Auth → RBAC │   │   │
│  │  └──────────────────────────────────────────────────────────────┘   │   │
│  │                                                                      │   │
│  │  ┌─── Route Modules ────────────────────────────────────────────┐   │   │
│  │  │ /api/auth      │ /api/invoices   │ /api/clients              │   │   │
│  │  │ /api/products  │ /api/recurring  │ /api/team                 │   │   │
│  │  │ /api/company   │ /api/reports    │ /api/notifications        │   │   │
│  │  │ /api/payments  │ /api/operations │ /api/audit                │   │   │
│  │  │ /api/pdf       │ /api/v1 (ext)  │ /api/health               │   │   │
│  │  └──────────────────────────────────────────────────────────────┘   │   │
│  │                                                                      │   │
│  │  ┌─── Service Layer ────────────────────────────────────────────┐   │   │
│  │  │ InvoiceService  │ PDFService    │ EmailService               │   │   │
│  │  │ ReportsService  │ CacheService  │ WebhookService             │   │   │
│  │  │ RecurringService│ AuditService  │ ClientIntelligenceService  │   │   │
│  │  │ ProductService  │ DashboardSvc  │                            │   │   │
│  │  └──────────────────────────────────────────────────────────────┘   │   │
│  └──────────────────────────────────────────────────────────────────────┘   │
│                           │              │              │                    │
└───────────────────────────┼──────────────┼──────────────┼────────────────────┘
                            │              │              │
┌───────────────────────────┼──────────────┼──────────────┼────────────────────┐
│                    DATA & │ INFRA LAYER  │              │                    │
│                           ▼              ▼              ▼                    │
│           ┌──────────────────┐ ┌──────────────┐ ┌──────────────────┐        │
│           │   MongoDB Atlas  │ │ Upstash Redis│ │   BullMQ Workers │        │
│           │                  │ │              │ │                  │        │
│           │ • Users          │ │ • JWT Cache  │ │ • PDF Generation │        │
│           │ • Companies      │ │ • Rate Limit │ │ • Email Dispatch │        │
│           │ • Invoices       │ │ • API Cache  │ │ • Cron Jobs      │        │
│           │ • Clients        │ │              │ │   (Overdue,      │        │
│           │ • Products       │ └──────────────┘ │    Reminders,    │        │
│           │ • Expenses       │                  │    Recurring)    │        │
│           │ • Vendors        │ ┌──────────────┐ └──────────────────┘        │
│           │ • Notifications  │ │   Razorpay   │                            │
│           │ • AuditLogs      │ │   Gateway    │ ┌──────────────────┐        │
│           │ • Webhooks       │ │              │ │   SMTP (Gmail)   │        │
│           │ • RecurringInv   │ │ • Orders     │ │   Email Service  │        │
│           │ • ApiKeys        │ │ • Verify     │ └──────────────────┘        │
│           └──────────────────┘ └──────────────┘                            │
└─────────────────────────────────────────────────────────────────────────────┘
```

<br/>

## 🎯 Features

### 📊 Financial Intelligence Dashboard

A real-time command center with animated KPI cards, revenue trajectory charts, asset liquidity donut rings, and operational intelligence metrics including growth velocity, collection delay, enterprise value (CLTV), and ML-based revenue projections.

- **4 Primary KPIs** — Gross Volume, Active Issuance, Capital Pending, Realized Revenue
- **5 Intelligence Metrics** — Growth Velocity, Mean Collection Delay, Enterprise Value, Revenue Projection, Fulfillment Efficiency
- **Interactive Revenue Chart** — 6-month bar chart with hover tooltips
- **Transaction Ledger** — Live-synced recent invoice activity with status indicators

---

### 🧾 Invoice Management

Full lifecycle invoice management with professional PDF generation.

- **Create / Edit / Duplicate** invoices with line items, tax breakdowns (CGST/SGST/IGST), discounts, and custom notes
- **Status Workflow** — `Draft → Sent → Paid / Partially Paid / Overdue / Cancelled`
- **Partial Payments** — Record multiple payments against a single invoice with balance tracking
- **One-Click PDF** — Server-rendered, print-ready PDFs with company branding, QR codes, and HSN codes
- **Email Delivery** — Send invoices directly to clients with PDF attachment via SMTP
- **Payment Links** — Shareable public URLs for client-facing payment portals

---

### 🔄 Automated Recurring Billing

Set-and-forget recurring invoice schedules.

- **Flexible Intervals** — Weekly, Monthly, Quarterly, or custom day-of-month
- **Auto-Generation** — BullMQ cron worker creates invoices at midnight daily
- **Toggle On/Off** — Pause and resume any recurring schedule instantly
- **Template System** — Each recurring entry stores a full invoice template with line items

---

### 💳 Razorpay Payment Portal

A public-facing, branded payment page that clients can use to pay invoices instantly.

- **Razorpay Checkout** — Secure payment gateway integration with order creation and signature verification
- **UPI QR Codes** — Auto-generated QR codes for instant UPI payments (GPay, PhonePe, Paytm)
- **PDF Download** — Clients can download the invoice PDF from the payment page
- **Real-Time Status** — Invoice automatically marked as paid upon successful payment verification

---

### 👥 Multi-Tenant Architecture

True workspace isolation with instant organization switching.

- **Tenant Isolation** — Every data query is scoped to `companyId` via middleware
- **Organization Switching** — Users can belong to multiple companies and switch instantly from the sidebar
- **Role-Based Access Control** — Three permission tiers:

| Role | Permissions |
|------|------------|
| `Admin` | Full access — invoices, team, settings, API keys, billing |
| `Accountant` | Create/edit invoices, manage clients, products, expenses |
| `Viewer` | Read-only dashboard and invoice viewing |

---

### 📦 Product & Inventory Intelligence

Live inventory catalog with automatic invoice-to-product sync.

- **Product Catalog** — Name, SKU, HSN code, unit price, tax configuration, stock tracking
- **Bi-directional Sync** — Update a price on an invoice and it syncs back to inventory
- **Intelligence Dashboard** — Revenue-per-product analytics, top sellers, margin analysis

---

### 💰 Expense & Vendor Management

Track operational costs alongside revenue for complete financial visibility.

- **Expense Tracking** — Log expenses by category, vendor, date, and amount
- **Vendor Registry** — Maintain a vendor directory with contact details
- **Expense Analytics** — Category-wise breakdown and monthly trend analysis

---

### 📈 Advanced Reports & Analytics

Comprehensive financial reporting with export capabilities.

- **Overview Tab** — Revenue vs. expenses, net profit, collection rates
- **P&L Statement** — Income and expense breakdown with profit margins
- **Cash Flow Analysis** — Inflow vs. outflow tracking over time
- **Category Breakdown** — Revenue by client, product, and status
- **CSV/XLSX Export** — Download reports for accounting software integration

---

### 🔔 Notifications & Activity Audit

Stay informed with in-app notifications and a complete audit trail.

- **Real-Time Notifications** — Overdue alerts, payment confirmations, team invites
- **Audit Log** — Every action (create, update, delete, status change) is logged with timestamp, user, and diff
- **Webhook Dispatch** — External webhook events fired on `invoice.overdue`, `invoice.paid`, etc.

---

### 👨‍💼 Team Management

Invite and manage team members with granular role assignment.

- **Email Invitations** — Invite team members by email with auto-generated temporary passwords
- **Role Assignment** — Assign Admin, Accountant, or Viewer roles
- **Force Password Change** — New members must change password on first login

---

### 🔌 External API (v1)

RESTful API for programmatic access, secured with API key authentication.

- `GET /api/v1/invoices` — List invoices
- `POST /api/v1/invoices` — Create invoice
- `GET /api/v1/invoices/:id` — Get invoice
- `GET /api/v1/clients` — List clients
- `POST /api/v1/clients` — Create client

---

### ⚙️ Company Settings

White-label your workspace with full branding control.

- **Company Profile** — Name, address, GSTIN, PAN, contact details
- **Branding** — Primary color, logo URL, custom invoice prefix
- **UPI Integration** — Configure UPI ID for QR code payment collection
- **Default Templates** — Set default notes, terms & conditions for all invoices
- **API Key Management** — Generate and manage API keys for external integrations

<br/>

## ⚙️ Tech Stack

### Frontend

| Technology | Purpose |
|-----------|---------|
| **Next.js 16** (App Router) | React framework with file-based routing, SSR, and RSC |
| **React 19** | UI rendering with latest concurrent features |
| **TypeScript 5** | End-to-end type safety |
| **Tailwind CSS 4** | Utility-first styling with PostCSS integration |
| **Framer Motion** | Declarative animations and page transitions |
| **Zustand** | Lightweight state management with localStorage persistence |
| **React Hook Form + Zod** | Performant forms with schema-based validation |
| **Recharts** | Composable charting library for dashboard visualizations |
| **Axios** | HTTP client with interceptors for JWT refresh |
| **Lucide React** | Modern icon library |
| **date-fns** | Lightweight date formatting |
| **react-hot-toast** | Non-blocking toast notifications |
| **QRCode** | Dynamic UPI QR code generation |

### Backend

| Technology | Purpose |
|-----------|---------|
| **Node.js + Express** | High-performance REST API server |
| **TypeScript** | Full type safety across the backend |
| **MongoDB + Mongoose** | Document database with schema validation |
| **BullMQ + Redis** | Job queues for PDF generation, email dispatch, and cron tasks |
| **Upstash Redis** | Serverless Redis for caching, rate limiting, and queues |
| **JWT (Access + Refresh)** | Stateless authentication with automatic token refresh |
| **Razorpay SDK** | Payment gateway integration with order and signature verification |
| **Nodemailer** | SMTP-based transactional email delivery |
| **Helmet** | HTTP security headers |
| **express-rate-limit** | Tiered rate limiting (general, auth, signup, AI) |
| **express-mongo-sanitize** | NoSQL injection prevention |
| **Puppeteer** | Server-side PDF rendering with custom templates |

### Infrastructure

| Service | Purpose |
|---------|---------|
| **Vercel** | Frontend hosting with edge network and automatic deployments |
| **Render** | Backend hosting with managed Node.js runtime |
| **MongoDB Atlas** | Cloud-hosted database cluster |
| **Upstash** | Serverless Redis (queues + cache) |
| **Gmail SMTP** | Transactional email delivery |

<br/>

## 🔥 Unique Innovations

### 1. 🧠 Financial Intelligence Engine

Not just a dashboard — a **decision-support system**. The dashboard computes real-time intelligence metrics:
- **Growth Velocity** — Month-over-month revenue growth rate
- **Mean Collection Delay** — Average days between invoice send and payment
- **Customer Lifetime Value (CLTV)** — Aggregated revenue per client
- **Revenue Forecasting** — Next-month revenue prediction based on historical trends
- **Fulfillment Efficiency** — Percentage of invoices successfully collected

### 2. 🔄 Bi-Directional Inventory Sync

When you add a product to an invoice, the system automatically syncs:
- Price changes from invoice → product catalog
- Stock adjustments on invoice creation
- HSN/SAC code inheritance from product master data

### 3. 🏢 True Multi-Tenancy with Hot Switching

Unlike simple per-user accounts, InvoiceFlow implements **organizational multi-tenancy**:
- A single user can belong to multiple companies
- Switch between organizations instantly from the sidebar — no logout required
- Each company has completely isolated data (invoices, clients, products, settings)
- Role-based permissions are scoped per company

### 4. ⚡ Automated Dunning Pipeline

A fully automated collections workflow powered by BullMQ cron workers:
```
Invoice Sent → [2 days before due] Gentle Reminder Email
             → [Past due date] Auto-mark as Overdue
             → In-app Notification + Email + Webhook dispatch
```

### 5. 🎨 White-Label Payment Portal

Every invoice generates a unique public payment link (`/p/invoice/:token`). The payment page:
- Renders with the **company's branding** (logo, primary color)
- Shows a complete invoice preview with line items and tax breakdown
- Offers **Razorpay checkout** + **UPI QR code** for instant payment
- Allows PDF download without authentication

### 6. 🇮🇳 GST-Native Tax Engine

Purpose-built for Indian businesses with first-class GST support:
- Automatic **CGST/SGST** split for intra-state transactions
- **IGST** calculation for inter-state transactions
- **HSN/SAC code** tracking per line item
- GSTIN validation and display on invoices and PDFs

### 7. 🔐 Defense-in-Depth Security

Multiple layers of protection at every level:

| Layer | Protection |
|-------|-----------|
| **Transport** | HTTPS enforcement in production |
| **Headers** | Helmet security headers (CSP, HSTS, etc.) |
| **Auth** | JWT with access + refresh token rotation |
| **Rate Limiting** | 4-tier rate limiting (general, auth, signup, AI) |
| **Injection** | MongoDB sanitization against NoSQL injection |
| **Tenant** | Middleware-enforced data isolation per company |
| **RBAC** | Route-level role checking (Admin/Accountant/Viewer) |
| **Audit** | Every mutation logged with user, timestamp, and diff |

<br/>

## 🚀 Quick Start

### Prerequisites

- **Node.js** 18+
- **MongoDB** instance (local or Atlas)
- **Redis** instance (local or Upstash)

### 1. Clone the repository

```bash
git clone https://github.com/bansal1806/invoiceflow.git
cd invoiceflow
```

### 2. Backend Setup

```bash
cd invoiceflow-backend
npm install
```

Create a `.env` file:

```env
PORT=4000
MONGODB_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net/invoiceflow
JWT_SECRET=<your-jwt-secret>
JWT_REFRESH_SECRET=<your-refresh-secret>
JWT_EXPIRES_IN=15m
JWT_REFRESH_EXPIRES_IN=7d
CLIENT_URL=http://localhost:3000
REDIS_URL=rediss://<your-upstash-url>
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=<your-email>
SMTP_PASS=<your-app-password>
SMTP_FROM=no-reply@yourdomain.com
RAZORPAY_KEY_ID=<your-razorpay-key>
RAZORPAY_KEY_SECRET=<your-razorpay-secret>
```

Start the server:

```bash
npm run dev
```

### 3. Frontend Setup

```bash
cd invoiceflow-frontend
npm install
```

Create a `.env.local` file:

```env
NEXT_PUBLIC_API_URL=http://localhost:4000/api
```

Start the development server:

```bash
npm run dev
```

### 4. Open the app

Navigate to [http://localhost:3000](http://localhost:3000) and register your first account.

<br/>

## 📁 Project Structure

```
invoiceflow/
├── invoiceflow-frontend/          # Next.js 16 App
│   ├── src/
│   │   ├── app/
│   │   │   ├── (dashboard)/       # Protected route group
│   │   │   │   ├── dashboard/     # Financial intelligence
│   │   │   │   ├── invoices/      # CRUD + detail + edit
│   │   │   │   ├── recurring/     # Recurring billing
│   │   │   │   ├── clients/       # Client management
│   │   │   │   ├── products/      # Product catalog
│   │   │   │   ├── expenses/      # Expense tracking
│   │   │   │   ├── vendors/       # Vendor registry
│   │   │   │   ├── reports/       # Analytics (4 tabs)
│   │   │   │   ├── team/          # Team management
│   │   │   │   ├── settings/      # Company settings
│   │   │   │   └── activity/      # Audit log viewer
│   │   │   ├── login/             # Auth (login + register)
│   │   │   ├── change-password/   # Forced password change
│   │   │   ├── p/invoice/[token]/ # Public payment portal
│   │   │   └── page.tsx           # Landing page
│   │   ├── components/
│   │   │   ├── layout/            # Sidebar, TopBar
│   │   │   ├── reports/           # Report tab components
│   │   │   └── settings/          # Settings tab components
│   │   └── lib/
│   │       ├── api.ts             # Axios instance + API helpers
│   │       ├── auth-store.ts      # Zustand auth state
│   │       └── ui-utils.ts        # Formatting utilities
│   └── public/                    # Static assets & favicons
│
├── invoiceflow-backend/           # Express.js API
│   ├── src/
│   │   ├── server.ts              # App entry + middleware chain
│   │   ├── config/                # Database connection
│   │   ├── controllers/           # Route handlers
│   │   ├── models/                # Mongoose schemas (12 models)
│   │   ├── routes/                # Express routers (13 modules)
│   │   ├── services/              # Business logic (12 services)
│   │   ├── middleware/            # Auth, Tenant, ApiKey
│   │   ├── queues/                # BullMQ workers (PDF, Email, Cron)
│   │   └── lib/                   # Redis client, utilities
│   └── dist/                      # Compiled output
│
└── README.md
```

<br/>

## 📄 License

This project is proprietary software. All rights reserved. See the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with 🔥 by [Shourya Bansal](https://github.com/bansal1806)**

⚡ *InvoiceFlow — Financial clarity, beautifully engineered.*

</div>

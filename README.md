# LincolnPacker — Kickback Web Application

**Short description:**\
LincolnPacker (Kickback) is a web application that mirrors the mobile experience for a lead marketplace connecting sellers (lead submitters) and buyers (contractors). It supports auto-payment flows, Stripe Connect integration, wallets & payouts, admin-ready structure, and scalable architecture for future features.

---

## 1. Project Overview

LincolnPacker (Kickback) is a lead marketplace web application where sellers submit leads and buyers purchase them. The platform handles lead validation, automatic buyer matching, autopay billing, fee splitting, holding period for fraud protection, and Stripe Connect payouts to sellers.

This repository contains the web application codebase (frontend + backend), Stripe payment integration, and QA documentation.

**Figma Design (Client Request):**\
[View Figma Project →](https://www.figma.com/design/dLbJpUwbG0x2M52IGaSlZV/lincolnpacker-%7C%7C-WebGenius-%7C%7C-FO721480BCC03?node-id=28384-544&p=f&t=WBZjbLJhvpkgagRc-0)

---

## 2. Key Features

- **Authentication:** Sign Up / Sign In, Forgot / Reset Password
- **Dashboards:** Buyer and Seller dashboards for separate workflows
- **Lead Management:** Submit Leads, My Leads, Buy Leads, Client Details
- **Notifications:** Real-time updates for transactions and lead assignments
- **Wallet & Payout:** Track pending and available balances, request withdrawals
- **Purchase History:** Full billing and transaction log
- **Account Settings:** Manage profile, payment methods, and preferences
- **Policies:** Terms of Service & Privacy Policy pages
- **Stripe Integration:** Autopay, instant payouts, ACH transfers via Stripe Connect
- **Admin Structure:** Ready for scaling to admin dashboards and role-based management

---

## 3. Payment Flow

### 1️⃣ Lead Submission

- **Seller Action:** Submit a new lead.
- **System Action:** Validates data (fraud checks, region/industry match).
- **Status:** Lead moves to *Reviewed*.

### 2️⃣ Lead Assignment & Buyer Billing

- **System Action:** Automatically matches the lead with an eligible buyer (autopay or manual accept).
- **Trigger:** Buyer’s saved payment method is charged.
- **Funds Flow:** Full price captured → Kickback’s Stripe platform account.
- **Status:** Buyer sees “Lead Purchased,” Seller sees “Pending Payment.”

### 3️⃣ Platform Fee Split

- Example: Lead = \$60 → Kickback keeps \$20, Seller earns \$40.
- Seller’s balance marked as “Pending Earnings.”

### 4️⃣ Holding Period (Fraud Buffer)

- Duration: **3–7 days** (configurable or until month-end).
- Purpose: Prevent chargebacks and allow lead verification.
- Seller Dashboard shows “Pending Balance: \$40.”

### 5️⃣ Seller Balance Becomes Withdrawable

- After holding period, funds move to *Available Balance*.
- Seller may withdraw or enable automatic payouts.
- Payout options: Bank transfer (ACH) or Instant Debit (fee-based).
- Flow: Kickback → Stripe Connect → Seller Bank.

### 6️⃣ Final State

- Buyer: Lead visible and billed.
- Seller: Balance withdrawable.
- Kickback: Platform fee retained.

---

## 4. Architecture & Technologies

**Tech Stack:**

- **Frontend:** React + TypeScript + Tailwind CSS
- **Backend:** Node.js (Express/NestJS)
- **Database:** PostgreSQL
- **Payments:** Stripe Connect (autopay, fee split, payout automation)
- **Auth:** JWT-based authentication
- **Queue Management:** Redis + BullMQ (delayed payouts, webhook handling)
- **Storage:** S3-compatible service for attachments
- **Monitoring:** Sentry or similar logging system
- **Deployment:** GitHub Actions + Docker + cloud hosting (Vercel, Render, or AWS)

---

## 5. Testing & QA Process

Testing was conducted separately for **Seller** and **Buyer** user roles. Each bug was recorded, triaged, and tracked via Notion.

| Testing Stage       | Description                                                                                  |
| ------------------- | -------------------------------------------------------------------------------------------- |
| **Initial Testing** | Full functional testing for buyer and seller modules (dashboard, lead submission, payments). |
| **Bug Reporting**   | All issues recorded in Notion under separate sheets for Seller and Buyer.                    |
| **Re-testing**      | Verified fixed issues and closed upon confirmation.                                          |
| **Pending**         | Some bugs still open and under developer review.                                             |

**Bug Tracking Format:**

```
BUG_ID | Feature | Bug Title | Description | Severity | Priority | Labels | Buyer Type | Actual Result | Expected Result | Attachment | Status | Developer Comment | Resolution Date | Date Reported
```

**Notion Links:**

- Seller QA: [Seller Bug Sheet](https://www.notion.so/291a27313a3e804f8227c092cee9249a?v=291a27313a3e817fbd9e000cae65fbc4)
- Buyer QA: [Buyer Bug Sheet](https://www.notion.so/291a27313a3e806fb22fd2ecb3578aea?v=291a27313a3e813a9b41000c63420c39)

---

## 6. Bug Reporting & Notion Links

Use Notion to manage QA lifecycle and assign bugs to developers with updates tracked per status (Open, Fixed, Retested, Closed). Include Notion URLs in pull request descriptions or commit messages when resolving related issues.

---

## 7. Deployment

- Configure production and staging environments with separate Stripe API keys.
- Set up secure webhook handling for payment events.
- CI/CD pipeline: GitHub Actions for testing, linting, and deploying to staging or production.
- Hosting options: Frontend (Vercel/Netlify), Backend (Render/Heroku/AWS ECS).

---

## 8. Contribution Guidelines

- Use feature branches (`feat/<name>`) for new functionality.
- Follow **Conventional Commits**: `feat`, `fix`, `chore`, `docs`, `test`, `refactor`.
- All PRs must:
  - Reference a Notion bug ID or feature card.
  - Include tests or QA verification.
  - Pass lint and build checks.

---

## 9. Repository Description & Tags

**GitHub Description:**

> LincolnPacker — Kickback Web Application: a lead marketplace with Stripe Connect autopay, wallet payouts, and admin-ready scalability.

**Suggested Tags:**

```
lead-marketplace, stripe, stripe-connect, payments, autopay, react, nodejs, typescript, postgres, redis, docker, saas, marketplace, fintech
```




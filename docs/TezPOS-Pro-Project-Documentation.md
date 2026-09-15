# TezPOS Pro — Restaurant POS System
### Project Documentation v1.0

---

## 1. Project Overview

**Project Name:** TezPOS Pro
**Type:** Multi-role Restaurant Management & POS System
**Target Market:** Pakistan (Small dhabas to multi-branch restaurant chains)
**Core Idea:** A complete restaurant operating system — QR table ordering, real-time kitchen display, role-based staff access, billing (manual payment recording), inventory, and analytics — built offline-first for Pakistan's connectivity realities.

---

## 2. Tech Stack

| Layer | Technology |
|---|---|
| Backend (Core) | Python Django + Django REST Framework |
| Backend (Real-time) | FastAPI / Django Channels (WebSockets for KDS) |
| Frontend | HTML5, CSS3, Bootstrap, Tailwind CSS, JavaScript |
| Database (Cloud) | PostgreSQL |
| Database (Local cache) | SQLite (offline-first sync) |
| Background Jobs | Celery + Redis |
| Hosting (MVP) | Hostinger / VPS |
| Hosting (Scale) | AWS / DigitalOcean |
| Design | White & Yellow primary, Blue accents — animated UI throughout |

---

## 3. User Roles & Permissions

| Role | Access |
|---|---|
| **Super Admin / Owner** | Full system, multi-branch view, financial reports, staff management, override transactions |
| **Branch Manager** | Single branch full control, staff/shift mgmt, discount creation, sales reports |
| **Cashier** | Billing, manual payment method entry (Cash/Card/Bank), limited discount, void needs manager approval |
| **Waiter** | Table assign, order taking, order status update, own performance view |
| **Kitchen Staff / Chef** | KDS access only, order status updates, inventory consumption log |
| **Inventory Manager** *(optional)* | Stock in/out, low-stock alerts, supplier records |
| **Accountant** *(optional)* | Financial reports, expense tracking, payroll — no order access |

Implementation: Django `Groups & Permissions` + custom `Role` model + `@role_required()` view decorator + role-based frontend rendering.

---

## 4. Core Modules

1. **Order Management** — QR table ordering, dine-in/takeaway/delivery, order modification audit trail
2. **Kitchen Display System (KDS)** — Real-time WebSocket queue, color-coded urgency, recipe-linked inventory deduction
3. **Billing Engine** — Split bills, multi-payment (manual entry, no gateway for now), FBR-style tax calculation, digital receipts (WhatsApp/SMS)
4. **Inventory Management** — Stock tracking, wastage log, low-stock alerts
5. **Staff Management** — Attendance, shift scheduling, performance tracking, commission calculation
6. **Analytics Dashboard** — Sales trends, best-sellers, peak-hour heatmap, profit margin per dish
7. **Multi-Branch Command Center** — Centralized dashboard, branch comparison, centralized menu/pricing push
8. **Customer Experience** — Loyalty/points system, feedback capture, CRM (repeat customer preferences)
9. **Offline-First Architecture** — Local SQLite cache with background sync to PostgreSQL
10. **Integrations** — WhatsApp Business API, Foodpanda/Cheetay order sync, accounting export (future: JazzCash/Easypaisa)

---

## 5. Payment Handling (Current Scope)

- No payment gateway integration in this phase.
- Cashier manually selects payment method at checkout: **Cash / Card / Bank Transfer / Other**.
- System just records amount + method against invoice — no live transaction processing.

---

## 6. MVP (Phase 1) vs Phase 2 Roadmap

### Phase 1 — MVP
- Core order taking (QR + manual)
- Basic KDS
- Billing with manual payment recording
- Role-based access (Admin, Manager, Cashier, Waiter, Kitchen)
- Basic inventory
- Single-branch support

### Phase 2 — Top-Level Features
- Multi-branch command center
- AI demand forecasting & dead-stock detection
- Loyalty/CRM system
- WhatsApp + delivery aggregator integration
- Face-recognition attendance
- Payment gateway integration (JazzCash/Easypaisa)

---

## 7. Suggested Git Repository Structure

```
tezpos-pro/
├── backend/
│   ├── core/                  # Django project settings
│   ├── apps/
│   │   ├── accounts/          # Users, roles, permissions
│   │   ├── orders/            # Order management
│   │   ├── kitchen/           # KDS logic (Channels consumers)
│   │   ├── billing/           # Invoicing, payments (manual)
│   │   ├── inventory/         # Stock management
│   │   ├── branches/          # Multi-branch logic
│   │   └── analytics/         # Reports & dashboards
│   ├── requirements.txt
│   └── manage.py
├── frontend/
│   ├── static/
│   │   ├── css/
│   │   ├── js/
│   │   └── img/
│   ├── templates/
│   │   ├── admin/
│   │   ├── manager/
│   │   ├── cashier/
│   │   ├── waiter/
│   │   └── kitchen/
├── docs/
│   ├── TezPOS-Pro-Project-Documentation.md
│   ├── api-endpoints.md
│   └── db-schema.md
├── .gitignore
├── README.md
└── docker-compose.yml (optional, for Postgres + Redis local dev)
```

### Git Setup Commands
```bash
mkdir tezpos-pro && cd tezpos-pro
git init
echo "venv/
__pycache__/
*.pyc
.env
db.sqlite3
node_modules/" > .gitignore
git add .
git commit -m "Initial project structure — TezPOS Pro"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

### Branching Strategy
- `main` — production-ready code
- `develop` — active development
- `feature/<module-name>` — e.g. `feature/kitchen-display`, `feature/billing-engine`
- `hotfix/<issue>` — urgent fixes

---

## 8. Next Steps

1. Finalize database schema (ERD) for `orders`, `roles`, `inventory`, `branches`
2. Set up Django project + apps skeleton per structure above
3. Build role/permission system first (foundation for everything else)
4. Build order → KDS → billing flow (MVP core loop)
5. Add inventory + reports
6. Move to Phase 2 features once MVP is stable

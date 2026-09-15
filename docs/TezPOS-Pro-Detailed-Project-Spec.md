# TezPOS Pro — Detailed Project Specification & Team Module Division
### Version 2.0 — Full Build Document

---

## 1. Project Summary

**Name:** TezPOS Pro
**Type:** Multi-role Restaurant POS + Management System
**Market:** Pakistan (single dhaba → multi-branch chains)
**Payment scope (current phase):** No gateway — cashier manually records payment method (Cash / Card / Bank / Other)
**Repo:** github.com/danishmalik7570-a11y/Resturant-POS-Software

---

## 2. Full Tech Stack

| Layer | Technology |
|---|---|
| Backend (core) | Python, Django, Django REST Framework |
| Backend (real-time) | Django Channels (WebSockets) for KDS |
| Frontend | HTML5, CSS3, Bootstrap, Tailwind CSS, JavaScript |
| DB (cloud) | PostgreSQL |
| DB (local/offline) | SQLite (sync cache) |
| Background jobs | Celery + Redis |
| Auth | Django auth + custom Role/Permission layer |
| Hosting (MVP) | Hostinger / VPS |
| Hosting (scale) | AWS / DigitalOcean |
| UI Theme | White + Yellow primary, Blue accents, top-level animations |

---

## 3. Database Schema (Core Tables — ERD Outline)

```
User (id, name, phone, email, password, role_id, branch_id, is_active)
Role (id, name, permissions_json)
Branch (id, name, address, city, is_active)
Category (id, name, branch_id)
MenuItem (id, name, price, category_id, is_available, image, description)
Table (id, table_number, branch_id, qr_code, status)
Order (id, table_id, waiter_id, status, order_type, created_at)
OrderItem (id, order_id, menu_item_id, quantity, notes, status)
Invoice (id, order_id, total, tax, discount, payment_method, cashier_id, created_at)
InventoryItem (id, name, unit, quantity, low_stock_threshold, branch_id)
StockLog (id, inventory_item_id, change_qty, reason, created_at)
Attendance (id, user_id, check_in, check_out, date)
Shift (id, user_id, branch_id, start_time, end_time)
Feedback (id, order_id, rating, comment, created_at)
```

---

## 4. Module Breakdown (for Team Division)

Divide the repo into independent Django apps so each team member can work in parallel without merge conflicts.

| # | Module (Django App) | Responsibility | Suggested Owner |
|---|---|---|---|
| 1 | `accounts` | User auth, roles, permissions, staff management | Backend Lead |
| 2 | `branches` | Branch CRUD, multi-branch switching logic | Backend Dev 1 |
| 3 | `menu` | Categories, menu items, pricing, availability | Backend Dev 1 |
| 4 | `orders` | Order creation, table assignment, order lifecycle | Backend Dev 2 |
| 5 | `kitchen` | KDS — WebSocket consumers, order queue, status updates | Backend Dev 2 (Channels experience needed) |
| 6 | `billing` | Invoice generation, manual payment recording, tax calc | Backend Dev 1 |
| 7 | `inventory` | Stock tracking, low-stock alerts, stock logs | Backend Dev 3 |
| 8 | `staff` | Attendance, shifts, performance | Backend Dev 3 |
| 9 | `analytics` | Reports, dashboards, sales charts | Backend Lead / Dev 3 |
| 10 | `frontend/admin` | Owner/Manager dashboard UI | Frontend Dev 1 |
| 11 | `frontend/cashier` | Cashier billing screen UI | Frontend Dev 1 |
| 12 | `frontend/waiter` | Waiter order-taking UI (QR + manual) | Frontend Dev 2 |
| 13 | `frontend/kitchen` | KDS display UI | Frontend Dev 2 |

**Rule:** Har module apni Django app ke andar independent rahe — models, views, urls, templates sab module-specific folder mein, taake team ek dusre ke code pe overlap na kare.

---

## 5. Git Workflow for Team

```
main        → stable, production-ready only
develop     → integration branch, sab features yahan merge honge
feature/*   → individual work, e.g. feature/kitchen-display, feature/billing-module
```

### Steps for each team member:
```bash
git clone https://github.com/danishmalik7570-a11y/Resturant-POS-Software.git
cd Resturant-POS-Software
git checkout develop        # ya develop branch bana lo agar nahi hai
git checkout -b feature/<your-module-name>
# apna kaam karo, commit karo
git push origin feature/<your-module-name>
# phir GitHub pe Pull Request bana kar develop mein merge karo
```

### Access / Token Note
- Agar kisi collaborator ko push karte waqt authentication issue aaye, unhe khud apna **Personal Access Token** generate karna chahiye (GitHub → Settings → Developer settings → Tokens) — shared token use karna security risk hai, har member apna alag token use kare.
- Ya better: GitHub repo ke **Settings → Collaborators** se team members ko directly invite kar do, phir woh apne GitHub account se SSH/HTTPS login karke push kar sakenge — token share karne ki zaroorat hi nahi rahegi.

---

## 6. Development Phases

### Phase 1 — Foundation (Week 1-2)
- `accounts` app: roles, auth, permissions
- `branches` + `menu` apps
- Basic Django project structure + PostgreSQL setup

### Phase 2 — Core Loop (Week 3-4)
- `orders` app (QR + manual order creation)
- `kitchen` app (KDS with WebSockets)
- `billing` app (manual payment recording, invoice generation)

### Phase 3 — Operations (Week 5-6)
- `inventory` app
- `staff` app (attendance, shifts)
- Role-based frontend dashboards for all 5 roles

### Phase 4 — Intelligence (Week 7+)
- `analytics` app (reports, dashboards)
- Offline-first sync (SQLite ↔ PostgreSQL)
- Multi-branch command center

### Phase 5 — Future
- WhatsApp Business API integration
- Payment gateway (JazzCash/Easypaisa)
- AI demand forecasting

---

## 7. Next Immediate Action Items

1. Team ko repo pe collaborator invite karo (token sharing avoid karo)
2. `develop` branch banao aur usse protect karo (main pe direct push disable)
3. Har member apna assigned module (section 4) `feature/*` branch pe shuru kare
4. Daily/weekly short sync — kaun se module mein kya progress hai

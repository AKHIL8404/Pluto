# 🌾 KrishiMart — Farm-to-Consumer E-commerce

A complete, production-ready agricultural marketplace where Indian farmers sell directly to customers — no middlemen.

> **You are not a developer. That's fine.** This README walks you through every single step. Do them in order, replace each `YOUR_xxx_HERE` placeholder, and you'll have a live website on the internet.

---

## 📦 What you got in this folder

```
agri-ecommerce/
├── DEMO.html                      ← Open this in any browser to see the full live site (no setup!)
├── README.md                      ← You are here
├── database/
│   └── schema-with-demo-data.sql  ← Run this on Aiven MySQL to create all tables + demo data
├── backend/                       ← Spring Boot REST API (Java)
│   ├── pom.xml
│   └── src/main/java/com/krishimart/...
└── frontend/                      ← Angular 17 web app
    ├── package.json
    └── src/app/...
```

---

## 1️⃣ Architecture & Roles

### High-level architecture

```
┌──────────────────┐    HTTPS/JSON    ┌─────────────────────┐    JPA     ┌────────────────┐
│  Angular SPA     │ ───────────────► │  Spring Boot API    │ ─────────► │  MySQL (Aiven) │
│  (Vercel)        │ ◄─────────────── │  (Render)           │ ◄───────── │                │
└──────────────────┘   JWT in header  └─────────┬───────────┘            └────────────────┘
                                                │
                                                │  Paytm Payment Gateway
                                                ▼
                                       ┌─────────────────────┐
                                       │ securegw.paytm.in   │
                                       └─────────────────────┘
```

### Three user roles

| Role | What they can do | How they sign up |
|---|---|---|
| 👤 **Customer** | Browse products, add to cart, place orders, pay with Paytm, track orders | Self-register on `/register` |
| 🚜 **Farmer** | List & manage products, view orders for their products, see revenue | Self-register; needs admin approval to be verified |
| 🛡 **Admin** | Approve farmers, view all orders, see GMV/stats, manage users | Created manually in the database (cannot self-register) |

### Backend layered architecture

```
Controller (HTTP)  →  Service (Business logic)  →  Repository (JPA)  →  Database
     │                       │
     │                       └─ JWT validation, RBAC checks
     └─ Request/response DTOs, validation annotations
```

---

## 2️⃣ Database (MySQL on Aiven)

### Tables (all in 3rd Normal Form)

| Table | Purpose | Key columns |
|---|---|---|
| `roles` | Static lookup: CUSTOMER / FARMER / ADMIN | `id`, `name` |
| `users` | All accounts (customers, farmers, admins) | `id`, `email` *(unique)*, `mobile` *(unique)*, `password_hash`, `role_id` *(FK)*, `is_verified` |
| `categories` | Product categories | `id`, `name`, `slug`, `emoji` |
| `products` | All product listings | `id`, `farmer_id` *(FK→users)*, `category_id` *(FK)*, `price`, `stock_qty`, `is_active` |
| `orders` | Customer orders | `id`, `order_number`, `customer_id` *(FK)*, `total_amount`, `status` |
| `order_items` | Line items per order | `id`, `order_id` *(FK)*, `product_id` *(FK)*, `farmer_id` *(FK)*, `quantity`, `unit_price` |
| `payments` | Payment attempts (Paytm) | `id`, `order_id` *(FK)*, `gateway`, `gateway_txn_id`, `status` |

### How to set it up

1. Sign up at **[aiven.io](https://aiven.io)** (free trial available).
2. Click **Create service** → choose **MySQL** → free or hobbyist tier → AWS Mumbai (lowest latency for India) → name it `krishimart-db`.
3. Wait ~3 minutes for the service to come up.
4. Open the service → **Overview** tab → copy these values somewhere safe:
   - **Service URI** (looks like `mysql://avnadmin:abc...@krishimart-db-xxx.aivencloud.com:12345/defaultdb?ssl-mode=REQUIRED`)
   - **Host**, **Port**, **User**, **Password**, **Database name**
5. Open the service → **Quick connect** → click **MySQL CLI** OR use a tool like **MySQL Workbench** / **DBeaver** to connect.
6. Open the file `database/schema-with-demo-data.sql` in any text editor, copy the entire contents, paste into your SQL tool, and run it.
7. ✅ Done. Your database now has 14 demo users, 6 categories, 12 products, and 5 sample orders.

### Demo logins (password is `password123` for all)
- 🛡 Admin: `admin@krishimart.in`
- 🚜 Farmer: `ramesh@farm.in`
- 👤 Customer: `anita.s@email.com`

---

## 3️⃣ Spring Boot Backend

### What's included

- **JWT authentication** — token-based, no sessions.
- **Role-based access control** — `@PreAuthorize` on protected endpoints.
- **BCrypt password hashing**.
- **Paytm payment integration** with the proper AES-CBC checksum signature.
- **Global exception handler** — clean JSON errors for the frontend.
- **CORS configured** — so your frontend on Vercel can talk to your backend on Render.

### Tech stack

- Java 17, Spring Boot 3.3.4, Spring Security, Spring Data JPA
- MySQL Connector
- jjwt 0.12.6 for JWT
- Lombok, validation, web

### Run locally

```bash
cd backend
# Edit src/main/resources/application.properties — fill in your DB URL + secrets
./mvnw spring-boot:run
# Backend starts at http://localhost:8080
```

### REST API endpoints

| Method | URL | Auth | Description |
|---|---|---|---|
| POST | `/api/auth/register` | Public | Create a Customer or Farmer account |
| POST | `/api/auth/login` | Public | Returns JWT token + user info |
| GET | `/api/categories` | Public | List all active categories |
| GET | `/api/products?category=&q=&page=&size=` | Public | Paged product list with filters |
| GET | `/api/products/{id}` | Public | Single product |
| POST | `/api/orders` | Customer | Place a new order |
| GET | `/api/orders/me` | Customer | My orders |
| GET | `/api/orders/{id}` | Customer | Single order |
| GET | `/api/farmer/products` | Farmer | My listed products |
| POST | `/api/farmer/products` | Farmer | Create a new product |
| DELETE | `/api/farmer/products/{id}` | Farmer | Soft-delete my product |
| GET | `/api/farmer/orders` | Farmer | Orders containing my products |
| GET | `/api/admin/stats` | Admin | Top-line dashboard metrics |
| GET | `/api/admin/farmers/pending` | Admin | Farmers awaiting approval |
| POST | `/api/admin/farmers/{id}/approve` | Admin | Verify a farmer |
| GET | `/api/admin/orders` | Admin | All orders |
| POST | `/api/payments/paytm/initiate?orderId=` | Customer | Start a payment, returns redirect URL |
| POST | `/api/payments/paytm/callback` | Public | Paytm POSTs here when payment finishes |
| GET | `/api/payments/status/{orderId}` | Customer | Check payment status |

### Sample request — register a customer

```bash
curl -X POST http://localhost:8080/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "fullName": "Ravi Kumar",
    "email": "ravi@test.in",
    "mobile": "9876543210",
    "password": "password123",
    "role": "CUSTOMER"
  }'
```

### `application.properties` — what to fill in

The file `backend/src/main/resources/application.properties` already has placeholders. **Replace every `YOUR_xxx_HERE` value:**

```properties
# ─── DATABASE (from your Aiven service) ───────────────────────
spring.datasource.url=YOUR_AIVEN_DB_URL_HERE
# Example: jdbc:mysql://krishimart-db-xxx.aivencloud.com:12345/defaultdb?sslMode=REQUIRED
spring.datasource.username=YOUR_AIVEN_USERNAME_HERE
spring.datasource.password=YOUR_AIVEN_PASSWORD_HERE

# ─── JWT (make up a long random string, 32+ characters) ───────
jwt.secret=YOUR_JWT_SECRET_AT_LEAST_32_CHARS_LONG_HERE
jwt.expiration-ms=86400000

# ─── Paytm (from business.paytm.com → Developer Settings) ────
paytm.merchant-id=YOUR_PAYTM_MID_HERE
paytm.merchant-key=YOUR_PAYTM_MERCHANT_KEY_HERE
paytm.website=WEBSTAGING
paytm.industry-type=Retail
paytm.channel-id=WEB
paytm.api-host=securegw-stage.paytm.in
paytm.callback-url=YOUR_BACKEND_URL_HERE/api/payments/paytm/callback
paytm.frontend-redirect-url=YOUR_FRONTEND_URL_HERE/orders

# ─── CORS (your frontend domain) ──────────────────────────────
app.cors.allowed-origins=http://localhost:4200,YOUR_FRONTEND_URL_HERE
```

> 💡 **Pro tip:** On Render you don't need to edit this file — set them as environment variables instead (see Section 6).

---

## 4️⃣ Angular Frontend

### What's included

- **Angular 17** with standalone components and lazy-loaded routes.
- **Tailwind CSS** with the KrishiMart brand palette pre-configured.
- **JWT auth** — token stored in `localStorage`, attached to every request via HTTP interceptor.
- **Role guards** — `/farmer` requires Farmer/Admin role, `/admin` requires Admin role.
- **Reactive cart** using Angular signals, persisted in localStorage.
- **Fully responsive** — works on mobile, tablet, desktop.

### Folder structure

```
frontend/src/app/
├── app.component.ts          ← Shell (navbar + outlet + footer)
├── app.routes.ts             ← All routes with guards
├── core/
│   ├── models/               ← TypeScript interfaces
│   ├── services/             ← AuthService, ProductService, OrderService, etc.
│   ├── interceptors/         ← JWT interceptor
│   └── guards/               ← authGuard, roleGuard
├── shared/components/        ← Navbar, Footer, ProductCard
└── features/
    ├── home/                 ← Landing page
    ├── products/             ← List + detail
    ├── cart/                 ← Cart page
    ├── orders/               ← Checkout + my-orders
    ├── auth/                 ← Login + register
    ├── farmer/               ← Farmer dashboard
    └── admin/                ← Admin dashboard
```

### Run locally

```bash
cd frontend
npm install
npm start
# Opens at http://localhost:4200
```

### `environment.ts` — what to fill in

`frontend/src/environments/environment.ts` (development — **no edits needed** if backend is on localhost):
```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:8080/api'
};
```

`frontend/src/environments/environment.prod.ts` (production — **REPLACE the placeholder**):
```typescript
export const environment = {
  production: true,
  apiUrl: 'YOUR_BACKEND_URL_HERE/api'
  // Example after deployment: 'https://krishimart-backend.onrender.com/api'
};
```

---

## 5️⃣ Payment Flow (Paytm)

```
┌──────────┐    1. POST /api/orders          ┌──────────┐
│ Customer │ ──────────────────────────────► │ Backend  │
│ (Angular)│                                  │ creates  │
│          │ ◄────────── orderId ──────────  │ order    │
└──────────┘                                  └──────────┘
     │
     │ 2. POST /api/payments/paytm/initiate?orderId=N
     ▼
┌──────────┐                                  ┌──────────┐
│ Backend  │ ─── builds AES checksum ──────► │  Paytm   │
│          │     /initiateTransaction         │   API    │
│          │ ◄────── txnToken + URL ────────  │          │
└──────────┘                                  └──────────┘
     │
     │ 3. returns showPaymentPage URL to frontend
     ▼
┌──────────┐    4. window.location = url     ┌──────────┐
│ Customer │ ──────────────────────────────► │  Paytm   │
│          │                                  │   pays   │
└──────────┘                                  └──────────┘
                                                   │
                                  5. POSTs to      │
                                  /paytm/callback  │
                                                   ▼
                                              ┌──────────┐
                                              │ Backend  │
                                              │ verifies │
                                              │ checksum │
                                              │ + calls  │
                                              │ /v3/order│
                                              │ /status  │
                                              │ marks    │
                                              │ PAID     │
                                              └──────────┘
                                                   │
                                  6. redirect to   │
                                  frontend /orders │
                                                   ▼
                                              ┌──────────┐
                                              │ Customer │
                                              │ sees     │
                                              │ "PAID"   │
                                              └──────────┘
```

### How to get Paytm credentials

1. Go to **[business.paytm.com](https://business.paytm.com)** and sign up.
2. Verify your email + mobile.
3. Go to **Developer Settings → API Keys**.
4. For **testing**, use the **Staging credentials** they provide instantly:
   - `MID` (Merchant ID) — e.g. `KrishM45112233445566`
   - `Merchant Key` — a 16-character alphanumeric string
   - Website: `WEBSTAGING`
   - Industry Type: `Retail`
   - Host: `securegw-stage.paytm.in`
5. To **go live**, complete KYC (PAN, GST, bank details, business proof). Paytm will issue production credentials. Then switch:
   - Website to `DEFAULT`
   - Host to `securegw.paytm.in`

> ⚠ **Callback URL:** Paytm will POST the payment result to `YOUR_BACKEND_URL_HERE/api/payments/paytm/callback`. The backend (a) verifies the checksum, (b) confirms via Paytm's `/v3/order/status` API, (c) marks the order PAID, then (d) redirects the user back to your frontend `/orders` page.

> 🧪 **Sandbox test cards/UPI:** Paytm provides test credentials in their docs. UPI: `success@paytm` for success, `failure@paytm` for failure. Test card: `4242 4242 4242 4242` (any expiry/CVV).

---

## 6️⃣ Deployment Checklist

### ✅ Step-by-step (do them in order)

#### Step 1 — Push code to GitHub
1. Create a free GitHub account if you don't have one.
2. Create **two repositories**: `krishimart-backend` and `krishimart-frontend`.
3. Upload the `backend/` folder to the first repo, `frontend/` to the second.
   - Easiest way: install **GitHub Desktop**, drag the folder in, click **Publish**.

#### Step 2 — Create the database (Aiven)
1. Sign up at [aiven.io](https://aiven.io).
2. Create a **MySQL** service (free tier or hobbyist) in Mumbai region.
3. Wait for it to be **Running** (~3 min).
4. Run `database/schema-with-demo-data.sql` via Aiven's SQL console or MySQL Workbench.
5. ✏️ **Save these values** for later:
   - `JDBC URL` (transform Service URI: `mysql://USER:PASS@HOST:PORT/DB?ssl-mode=REQUIRED` becomes `jdbc:mysql://HOST:PORT/DB?sslMode=REQUIRED`)
   - `Username`
   - `Password`

#### Step 3 — Get Paytm sandbox credentials
1. Sign up at [business.paytm.com](https://business.paytm.com).
2. Use staging/sandbox credentials (instant) for testing. Save:
   - MID (Merchant ID)
   - Merchant Key
   - Website (`WEBSTAGING` for sandbox)

#### Step 4 — Deploy backend to Render
1. Sign up at [render.com](https://render.com) (free tier available).
2. Click **New** → **Web Service** → connect your GitHub `krishimart-backend` repo.
3. Configure:
   - **Name:** `krishimart-backend`
   - **Region:** Singapore (closest to India)
   - **Runtime:** Docker (auto-detected) OR set Build Command: `./mvnw clean package -DskipTests`
   - **Start Command:** `java -jar target/krishimart-backend-1.0.0.jar`
   - **Instance Type:** Free
4. Scroll to **Environment Variables** → add ALL of these:

   | Key | Value |
   |---|---|
   | `SPRING_DATASOURCE_URL` | `jdbc:mysql://your-aiven-host:port/defaultdb?sslMode=REQUIRED` |
   | `SPRING_DATASOURCE_USERNAME` | `avnadmin` (from Aiven) |
   | `SPRING_DATASOURCE_PASSWORD` | (from Aiven) |
   | `JWT_SECRET` | A 32+ character random string. Use [random.org](https://www.random.org/strings/) |
   | `PAYTM_MERCHANT_ID` | (your MID from business.paytm.com) |
   | `PAYTM_MERCHANT_KEY` | (your Merchant Key) |
   | `PAYTM_WEBSITE` | `WEBSTAGING` (or `DEFAULT` for live) |
   | `PAYTM_INDUSTRY_TYPE` | `Retail` |
   | `PAYTM_CHANNEL_ID` | `WEB` |
   | `PAYTM_API_HOST` | `securegw-stage.paytm.in` (or `securegw.paytm.in` for live) |
   | `PAYTM_CALLBACK_URL` | `YOUR_RENDER_URL_HERE/api/payments/paytm/callback` |
   | `PAYTM_FRONTEND_REDIRECT_URL` | `YOUR_VERCEL_URL_HERE/orders` (you'll know this after Step 5) |
   | `APP_CORS_ALLOWED_ORIGINS` | `http://localhost:4200,YOUR_VERCEL_URL_HERE` |

5. Click **Create Web Service**. Wait ~5 minutes for first build.
6. ✏️ **Save your Render URL**: `https://krishimart-backend.onrender.com`

#### Step 5 — Deploy frontend to Vercel
1. Sign up at [vercel.com](https://vercel.com) with your GitHub account.
2. Click **Add New Project** → import `krishimart-frontend`.
3. Configure:
   - **Framework Preset:** Angular
   - **Build Command:** `npm run build`
   - **Output Directory:** `dist/krishimart-frontend/browser`
   - **Install Command:** `npm install`
4. Before clicking deploy: **edit `src/environments/environment.prod.ts`** in your repo first. Replace `YOUR_BACKEND_URL_HERE` with your Render URL from Step 4. Push the change.
5. Click **Deploy**. Wait ~3 minutes.
6. ✏️ **Save your Vercel URL**: `https://krishimart-frontend.vercel.app`

#### Step 6 — Wire frontend URL back into backend
1. Go back to Render → your `krishimart-backend` service → **Environment**.
2. Update three variables to use your real Vercel URL:
   - `APP_CORS_ALLOWED_ORIGINS` → `http://localhost:4200,https://krishimart-frontend.vercel.app`
   - `PAYTM_FRONTEND_REDIRECT_URL` → `https://krishimart-frontend.vercel.app/orders`
3. Click **Save Changes** → backend restarts automatically.

#### Step 7 — Test it!
1. Open your Vercel URL.
2. Try logging in with `admin@krishimart.in` / `password123` → you should land on the admin dashboard.
3. Try registering a new customer, adding items to cart, and checking out.
4. The Paytm sandbox lets you "pay" with test UPI (`success@paytm`) or test cards.

### 📋 Final checklist

- [ ] Aiven MySQL service running, schema SQL executed
- [ ] Paytm sandbox credentials obtained
- [ ] GitHub repos created with code pushed
- [ ] Render backend deployed, all 11 env vars set
- [ ] `JWT_SECRET` is at least 32 random characters
- [ ] Vercel frontend deployed
- [ ] `environment.prod.ts` updated with Render URL
- [ ] Render `APP_CORS_ALLOWED_ORIGINS` includes Vercel URL
- [ ] Paytm callback URL configured in business.paytm.com dashboard
- [ ] Demo login works on the live site

---

## 🆘 Common problems & fixes

| Problem | Fix |
|---|---|
| `CORS error` in browser console | Add your Vercel URL to `APP_CORS_ALLOWED_ORIGINS` on Render and restart |
| `401 Unauthorized` everywhere | Logout and login again — token may be expired |
| Backend crashes on Render with "Communications link failure" | Wrong Aiven URL/password, or Aiven service is paused. Restart Aiven service |
| `403 Forbidden` on farmer endpoints | The user is registered as farmer but `is_verified=false`. Login as admin and approve them |
| Paytm payment redirects but order stays PENDING | Callback URL not reachable. Make sure `PAYTM_CALLBACK_URL` points to your live Render backend |
| `npm install` fails with peer-dep errors | Run `npm install --legacy-peer-deps` |
| Render free tier sleeps after 15 min | First request after sleep takes ~30s. Upgrade to paid tier ($7/mo) to keep it always-on |

---

## 📞 Support

- **Want to see the site instantly without setup?** Open `DEMO.html` in any browser (Chrome, Firefox, Safari). It's a fully working visual demo with all 3 role views.
- For Aiven help: [help.aiven.io](https://help.aiven.io)
- For Render help: [render.com/docs](https://render.com/docs)
- For Vercel help: [vercel.com/docs](https://vercel.com/docs)
- For Paytm integration: [business.paytm.com/docs](https://business.paytm.com/docs)

Made with 💚 for Indian farmers.

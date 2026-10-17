# Jai Bhagwan Hardware & Sanitary — Online Billing & Inventory Software

**Location:** Plot No. 12, Kamala Nehru Nagar, Ajmer Road, Jaipur, Rajasthan, India  
**Operating Hours:** 9:00 AM – 8:00 PM  
**Contact:** +91 9829012345 | info@jaibhagwanhardware.com  
**GSTIN (Rajasthan):** `08AABPJ1234F1Z5` (State Code: `08`)  

---

## 🌟 Executive Overview
A production-ready retail billing, GST invoicing, inventory tracking, and customer ledger software engineered specifically for **Jai Bhagwan Hardware & Sanitary**, Jaipur. It handles counter sales for CPVC/PVC pipes, fittings, sanitaryware, taps, faucets, water tanks, adhesives, and general hardware with decimal-safe financial calculations and dual print capabilities (A4 GST Invoices and 80mm POS Thermal Receipts).

---

## 🏗️ Technology Stack
- **Frontend:** React 19 + Vite + Tailwind CSS + Lucide Icons
- **Backend:** Node.js + Express REST API (CORS & JSON body parsing)
- **Database:** Supabase PostgreSQL with Row Level Security (RLS) & transactional consistency
- **Calculation Engine:** Decimal-safe Indian GST monetary calculation engine (CGST 9% + SGST 9% for Intra-state Rajasthan; IGST 18% for Inter-state)
- **Print Engine:** Dedicated `@media print` CSS engine for:
  1. **A4 Tax Invoices** (Indian retail format with HSN breakdown, bank details, amount in words, signatory box)
  2. **80mm POS Thermal Receipts** (compact counter memo format for roll printers)
- **PDF Generation:** Client-side vector PDF generation via `jsPDF` + `jspdf-autotable`
- **WhatsApp Integration:** Instant Click-to-Chat sharing with validated Indian mobile number format (`91XXXXXXXXXX`) and pre-filled billing messages.

---

## 📁 Repository Structure
```
software for billiung hardware and saintary/
├── client/                     # React + Vite + Tailwind CSS Frontend
│   ├── index.html
│   ├── vite.config.js
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   ├── src/
│   │   ├── main.jsx
│   │   ├── App.jsx             # Main router & print trigger coordinator
│   │   ├── index.css           # Tailwind base + dedicated @media print stylesheets
│   │   ├── components/
│   │   │   ├── Sidebar.jsx     # Navigation sidebar with store badges
│   │   │   ├── Header.jsx      # Top shortcuts bar (F2, F4, Ctrl+Enter)
│   │   │   ├── PrintA4Invoice.jsx    # Professional A4 Indian GST Tax Invoice
│   │   │   ├── PrintThermalReceipt.jsx# 80mm POS thermal receipt memo
│   │   │   ├── InvoiceSuccessModal.jsx# 1-Click print, PDF, and WhatsApp modal
│   │   │   └── WhatsAppModal.jsx      # WhatsApp click-to-chat generator
│   │   ├── pages/
│   │   │   ├── Dashboard.jsx   # Live KPIs from DB, recent bills & low-stock alerts
│   │   │   ├── BillingScreen.jsx# Fast counter POS with keyboard shortcuts
│   │   │   ├── Products.jsx    # Products catalog & manual stock adjustments
│   │   │   ├── Customers.jsx   # Customer directory with credit ledger
│   │   │   ├── InvoiceHistory.jsx# Invoice registers, reprint, & due settlements
│   │   │   ├── Purchases.jsx   # Supplier inward bills & auto stock increment
│   │   │   ├── Inventory.jsx   # Stock movement audit ledger (immutable audit trail)
│   │   │   ├── Reports.jsx     # GSTR-1 HSN breakdown & tender split
│   │   │   └── Settings.jsx    # Shop profile, GSTIN, bank & printer settings
│   │   └── services/
│   │       ├── api.js          # REST API client
│   │       ├── pdfGenerator.js # jsPDF invoice builder
│   │       └── numberToWords.js# Indian numbering (Lakhs, Crores, Paise)
├── server/                     # Node.js + Express Backend
│   ├── server.js               # Express application entrypoint
│   ├── config/
│   │   ├── supabase.js         # Supabase connection initializer
│   │   └── memoryStore.js      # In-memory transactional repository
│   ├── routes/
│   │   ├── products.js         # /api/products
│   │   ├── customers.js        # /api/customers
│   │   ├── invoices.js         # /api/invoices (Atomic invoice finalize transaction)
│   │   ├── purchases.js        # /api/purchases (Inward stock increment)
│   │   ├── inventory.js        # /api/inventory (Audit movements & low-stock)
│   │   ├── reports.js          # /api/reports (Dashboard KPIs & GST summary)
│   │   ├── settings.js         # /api/settings (Store profile & rules)
│   │   └── whatsapp.js         # /api/whatsapp (Click-to-chat generator)
│   └── utils/
│       ├── calculations.js     # Decimal-safe Indian GST billing math
│       └── numberToWords.js    # Indian Rupee converter
├── supabase/
│   ├── schema.sql              # PostgreSQL schema with RLS and foreign keys
│   └── seed.sql                # Authentic hardware & sanitary items (Astral, Jaquar, Cera, Dr Fixit)
├── .env.example
├── package.json                # Root orchestration script
└── README.md
```

---

## ⚡ Quick Start on Windows

### 1. Install Dependencies
Open PowerShell or Command Prompt in the project folder and run:
```powershell
npm run install:all
```
*(This automatically installs root, client, and server dependencies)*

### 2. Run the Application Locally
Run both the Backend (Port `5000`) and the Frontend (Port `5173`) with one command:
```powershell
npm run dev
```

Open your browser at:
👉 **Frontend:** [http://localhost:5173](http://localhost:5173)  
👉 **Backend API:** [http://localhost:5000/api](http://localhost:5000/api)  
👉 **API Health Check:** [http://localhost:5000/api/health](http://localhost:5000/api/health)  

---

## 🗄️ Supabase Database Setup

### Step 1: Create a Supabase Project
1. Log in to [supabase.com](https://supabase.com) and create a new project (e.g. `jai-bhagwan-hardware`).
2. Go to **Project Settings** -> **API** and copy your `Project URL`, `anon public key`, and `service_role secret key`.

### Step 2: Run SQL Schema and Seed
1. Open the **SQL Editor** in your Supabase dashboard.
2. Copy and paste the contents of [`supabase/schema.sql`](supabase/schema.sql) and click **Run**.
3. Copy and paste the contents of [`supabase/seed.sql`](supabase/seed.sql) and click **Run**.

### Step 3: Configure Environment Variables
Update your `server/.env` file:
```env
PORT=5000
NODE_ENV=production
CLIENT_URL=http://localhost:5173

SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key-here
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key-here
DEFAULT_BUSINESS_ID=00000000-0000-0000-0000-000000000001
```

*(Note: The system includes a built-in persistent fallback store pre-seeded with authentic Astral, Ashirvad, Jaquar, and Sintex hardware items, so you can test all features right out of the box even before entering Supabase credentials!)*

---

## 🚀 Production Deployment

### Frontend Deployment (Vercel)
1. Push your code to GitHub.
2. Import the repository in [Vercel](https://vercel.com).
3. Set **Root Directory** to `client`.
4. Add Environment Variable:
   - `VITE_API_URL` = `https://your-backend-api.onrender.com/api`
5. Deploy.

### Backend Deployment (Render / Railway)
1. In [Render](https://render.com), create a **Web Service**.
2. Set **Root Directory** to `server`.
3. Build Command: `npm install`
4. Start Command: `node server.js`
5. Add Environment Variables:
   - `PORT` = `5000`
   - `SUPABASE_URL` = `https://your-project.supabase.co`
   - `SUPABASE_SERVICE_ROLE_KEY` = `your-service-role-key`
   - `CLIENT_URL` = `https://your-frontend.vercel.app`

---

## 🖨️ Printing Instructions
The application includes a dual print stylesheet:
1. **A4 Invoice**: Click **"Print A4 Invoice"** from the bill screen or invoice history. The print layout hides all web menus, navigation bars, and buttons, producing an authentic Indian retail GST invoice with bank account details, UPI ID, amount in words, and authorized signatory box.
2. **80mm POS Thermal Receipt**: Click **"80mm Thermal"** to print on compact 80mm roll printers for rapid checkout.

---

## 💬 WhatsApp Integration
- Click **"Share WhatsApp"** on any finalized bill.
- The system automatically sanitizes the customer mobile number (prepending `91` for Indian numbers).
- It creates a pre-formatted, easy-to-read message summarizing invoice number, shop details, item quantities, total amount, and balance due.
- Click **"Open WhatsApp Chat"** to open WhatsApp Web or Desktop.
- Click **"Download PDF"** to easily attach the invoice document to the conversation.

---

## 🧪 Comprehensive Verification Checklist (All 14 Test Scenarios)
1. **Register / Configure Owner**: Go to **Settings** -> edit shop name, Jaipur address, phone, GSTIN, and bank details -> click Save.
2. **Add a Product**: Go to **Products** -> click "+ Add New Product" -> enter price, GST rate (e.g. 18%), and initial stock.
3. **Add an Unsaved Item**: Go to **New Bill (F2)** -> click "+ Custom Item" -> type an unsaved item directly in the row with custom quantity and rate.
4. **Create Invoice with Multiple Products**: Search products (e.g., "Astral", "Jaquar") -> add multiple lines -> verify real-time price & tax calculations.
5. **Verify Math Calculations**: Verify Subtotal, Discount %, Taxable Value, CGST (50%), SGST (50%), and Grand Total rounding.
6. **Save Invoice**: Press `Ctrl+Enter` or click "Finalize & Print Bill". Confetti triggers and the success dialog appears.
7. **Verify Stock Deduction**: Return to **Products** or **Stock Audit Trail** -> observe that stock decremented exactly once.
8. **Print A4 and Thermal Receipt**: Test both "Print A4 Invoice" and "80mm Thermal" from the modal.
9. **Download PDF**: Click "Download PDF" and verify the generated vector invoice PDF.
10. **Open WhatsApp**: Click "Share WhatsApp" and verify the formatted message and click-to-chat URL.
11. **Reprint Invoice**: Go to **Invoice History** -> click preview/print on any past invoice.
12. **Test Partial Payments & Credit**: In Billing, enter a partial amount received (e.g., ₹500 on a ₹1,200 bill). Notice remaining balance marked as "Balance Due", and settle it later via **Invoice History** -> "Collect Due".
13. **Negative Stock Guard**: Attempt to bill more than available stock when "Allow Negative Stock" is disabled -> observe validation message.
14. **Responsive UI**: Resize your browser window or test on a tablet/mobile device.

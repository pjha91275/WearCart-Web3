# WearCart - Hybrid Web2 & Web3 Apparel E-commerce & Business Management System

**WearCart** is a modern full-stack hybrid apparel e-commerce and enterprise business management platform. It offers a traditional retail experience combined with decentralized Web3 payments and smart contracts. Customers can browse clothing items, apply coupons, and checkout using either traditional cards/UPI (via Razorpay) or cryptocurrency (ETH on Ethereum/Sepolia) directly via connected Web3 wallets. Administrators are equipped with comprehensive tools for managing inventory, orders, invoices, payments, and vendor purchases.

---

## 👥 Development Team
This is a collaborative team project designed and built by:
*   **Prince Jha**
*   **Sachin Jha**

---

## 🎥 Demo Video
*   **Web3 & Hybrid Version (This Repository)**: [Google Drive Link](https://drive.google.com/file/d/1NZvMiRhoOE7sJ5BwIPprgbdPwUftHSQN/view?usp=drive_link)

---

## ⚡ Key Highlights & Advancements

*   **Hybrid Payment Gateway**: Supports both traditional electronic payments (Credit/Debit Cards, UPI, NetBanking via **Razorpay**) and decentralized blockchain payments (**ETH** via a Solidity smart contract).
*   **Web3 Wallet Integration**: Out-of-the-box wallet connectivity supporting MetaMask, Rainbow, and other wallets using **RainbowKit** and **Wagmi** on the frontend.
*   **Decentralized Smart Contracts**: A custom-built Solidity smart contract (`ApparelMarketplace.sol`) deployed on the Ethereum Sepolia network handles on-chain product listings, decentralized stock queries, item purchases, and secure contract fund withdrawals.
*   **Enterprise Administration**: Fully integrated back-office system for tracking sale orders, vendor purchase orders, generating customer invoices, logging vendor bills, tracking incoming payments, and generating sales/purchase reports.
*   **Automatic Stock Control**: Inventory quantities automatically sync in real-time, reducing stock upon sale order confirmations (both Web2 and Web3) and increasing stock when vendor purchase orders are confirmed.
*   **Automated Invoicing Engine**: Configurable system setting to automatically generate and issue customer invoices immediately after checkout payments are verified.

---

## 🛠️ Tech Stack

### Frontend (Customer Portal)
*   **Framework**: Next.js 14 (App Router)
*   **Library**: React, TypeScript
*   **Styling**: Tailwind CSS
*   **Web3 Integration**: RainbowKit, Wagmi, Viem, TanStack React Query
*   **State Management**: Zustand

### Backend (Admin API)
*   **Server**: Node.js, Express.js
*   **Database**: PostgreSQL
*   **ORM**: Sequelize ORM
*   **Authentication**: JWT (JSON Web Tokens) with role-based access controls
*   **Payment APIs**: Razorpay Node SDK

### Smart Contracts (Blockchain Layer)
*   **Language**: Solidity (v0.8.19)
*   **Networks**: Sepolia Testnet, Ethereum Mainnet

---

## 📂 Project Structure

```
WearCart-Web2&Web3/
├── backend/                  # Express.js Rest API & DB Services
│   ├── api/                  # Server entry point (server.js)
│   ├── config/               # Database connection configurations (PostgreSQL/Supabase)
│   ├── controllers/          # Business logic controllers (auth, products, sales, payments, coupons)
│   ├── middleware/           # Authentication & role authorization middleware
│   ├── models/               # Sequelize PostgreSQL models
│   ├── routes/               # Express routing endpoints
│   ├── seeds/                # Initial database seed scripts
│   └── scripts/              # Migration utilities
├── frontend/                 # Next.js 14 Web Application
│   ├── app/                  # Web App pages & routing (cart, checkout, admin, orders)
│   ├── components/           # Reusable UI elements (Header, ProductCard, Web3Provider)
│   ├── store/                # Zustand client-side global stores
│   └── utils/                # Web3 configurations, smart contract address, & ABI (web3.ts)
└── web3/                     # Smart Contract project directory
    └── contracts/            # Solidity smart contracts (ApparelMarketplace.sol)
```

---

## ⚙️ Setup & Installation

Follow these steps sequentially to set up and run the hybrid system locally.

### 1. Prerequisites
Ensure you have the following installed on your machine:
*   [Node.js (v18+)](https://nodejs.org/)
*   [PostgreSQL (v12+)](https://www.postgresql.org/) OR a [Supabase](https://supabase.com/) Account
*   [Git](https://git-scm.com/)
*   [WalletConnect Project ID](https://cloud.walletconnect.com/) (Required for RainbowKit connection on the frontend)

---

### 2. Backend Setup

1.  Navigate into the `backend` directory:
    ```bash
    cd backend
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Create a `.env` file in the root of the `backend` directory:
    ```env
    PORT=5000
    NODE_ENV=development
    JWT_SECRET=your_jwt_secret_key
    FRONTEND_URL=http://localhost:3000

    # PostgreSQL Database Credentials
    DB_HOST=localhost                # Or your Supabase Host
    DB_PORT=5432                     # Or your Supabase transaction port (e.g. 6543)
    DB_USER=postgres                 # Or your Supabase User
    DB_PASSWORD=your_password        # Or your Supabase Database Password
    DB_NAME=wearcart                 # Or your Supabase Database Name
    DB_SSL=false                     # Set to true if using Supabase or host requiring SSL
    ```
4.  Create the database in PostgreSQL:
    ```sql
    CREATE DATABASE wearcart;
    ```
5.  Seed the database (Creates tables and populates sample data):
    ```bash
    npm run seed
    ```
6.  Start the Express backend server:
    ```bash
    npm run dev
    ```
    The server will boot up at `http://localhost:5000`.

---

### 3. Frontend Setup

1.  Navigate into the `frontend` directory:
    ```bash
    cd frontend
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Create a `.env.local` file in the root of the `frontend` directory:
    ```env
    NEXT_PUBLIC_API_URL=http://localhost:5000/api
    NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=your_walletconnect_project_id
    ```
4.  Start the Next.js development server:
    ```bash
    npm run dev
    ```
    The application will run locally at `http://localhost:3000`.

---

### 4. Smart Contract Integration

The smart contract is written in Solidity and compiled for deployment.
*   **Contract Code**: [ApparelMarketplace.sol](./web3/contracts/ApparelMarketplace.sol)
*   **Deployment**: The contract should be compiled and deployed on an EVM-compatible chain (e.g., Sepolia Testnet). Once deployed, replace the `CONTRACT_ADDRESS` variable in [web3.ts](./frontend/utils/web3.ts):
    ```typescript
    export const CONTRACT_ADDRESS = 'YOUR_DEPLOYED_CONTRACT_ADDRESS';
    ```

---

## 🗄️ Database Models

*   **Users**: Stores user profiles for portal shoppers and internal admin users (distinguished by roles).
*   **Contacts**: Represents customers and vendors including addresses and configuration.
*   **Products**: Contains catalog item descriptions, categories, pricing, tax information, and current inventory stock level.
*   **Payment Terms**: Defines conditions of payments (e.g., immediate payment, or 15/30-day terms with early-payment discounts).
*   **Discount Offers**: Defines global discount promotions, percentage cuts, and applicable date ranges.
*   **Coupon Codes**: Unique voucher strings linked to discount offers, featuring validation controls (restricted by contact or usage limits).
*   **Sale Orders**: Client purchase receipts, recording totals, items, payment method (`crypto`/`razorpay`), and transaction verification hash (`txHash`).
*   **Purchase Orders**: Procurement documents issued to suppliers for inventory restock.
*   **Customer Invoices**: Sales invoices generated from sale orders for finance tracking.
*   **Vendor Bills**: Logged supplier invoices derived from purchase orders.
*   **Payments**: System transaction log capturing payment date, amount, payment method (cash, card, bank transfer, online, crypto), and verification reference ID.

---

## 🔌 API Endpoints

### 🔐 Authentication
*   `POST /api/auth/register` - Register a new customer user profile
*   `POST /api/auth/login` - Authenticate users and retrieve JWT tokens
*   `GET /api/auth/me` - Retrieve authenticated user profile payload

### 🏷️ Products Catalog
*   `GET /api/products` - Retrieve products list (supports category, type, and search queries)
*   `GET /api/products/:id` - Fetch details for a specific product
*   `POST /api/products` - Add a new apparel product (Internal Admin only)
*   `PUT /api/products/:id` - Update existing product info/stock (Internal Admin only)
*   `DELETE /api/products/:id` - Remove product from catalog (Internal Admin only)

### 📦 Sales Orders & Invoicing
*   `POST /api/sale-orders` - Create a new sale order (stores `txHash` and payment details)
*   `GET /api/sale-orders` - Retrieve list of all orders
*   `GET /api/sale-orders/:id` - Fetch single order details with items
*   `POST /api/sale-orders/:id/invoice` - Manually create an invoice from a sale order (Internal Admin only)

### 💳 Payment Gateways
*   `POST /api/payments/create-order` - Create a Razorpay transaction order
*   `POST /api/payments/verify` - Verify Razorpay payment signature hashes

### 🎟️ Coupon Management
*   `POST /api/coupons/validate` - Validate coupon strings before checkout applies
*   `GET /api/coupons` - Retrieve list of all system coupons (Internal Admin only)

---

## 📝 Features & Policy Implementations

### Automatic Stock Synchronization
*   **Deduction**: On checkout completion (sale order confirmed), the SQL database updates product quantities.
*   **Replenishment**: On confirming vendor purchase orders, inventory counts increase.

### Configurable Automated Invoicing
*   An `automatic_invoicing` system setting toggles generation modes.
*   When **enabled**: The server spawns customer invoices instantly upon payment verification.
*   When **disabled**: Administrative users must click "Create Invoice" on individual sales files.

### Payment Terms & Early Payment Discounts
*   Define custom early-payment incentives (e.g., 2% off if paid within 10 days).
*   System calculates dynamic discounts on base values or invoice totals.

### Expiry-Validated Coupon Codes
*   Checks expiration status, usage frequency, and profile-based contact restrictions before certifying checkouts.

---

## ⚖️ License
This project is licensed under the **ISC License**.

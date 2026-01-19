# 💳 Payment Gateway - Low Level Design

## 📖 Overview
A payment processing system that handles transactions between customers and merchants through multiple payment methods. This LLD focuses on transaction processing, payment method handling, and security.

---

## 🧩 Core Entities/Components
- **Customer** - Initiates payment
- **Merchant** - Receives payment
- **Transaction** - Payment record with status
- **PaymentMethod** - Credit Card, Debit Card, UPI, Wallet
- **PaymentProcessor** - Processes payment through providers
- **PaymentProvider** - External gateway (Stripe, Razorpay, PayPal)
- **TransactionManager** - Manages transaction lifecycle
- **RefundManager** - Handles refunds and cancellations

---

## 🔄 System Workflow

```
┌──────────────┐
│   Customer   │
│ Initiates    │
│  Payment     │
└──────┬───────┘
       │
       ▼
┌─────────────────────┐
│  Select Payment     │
│  Method             │
│  - Credit Card      │
│  - Debit Card       │
│  - UPI              │
│  - Wallet           │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Enter Details      │
│  - Card number      │
│  - CVV              │
│  - Amount           │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│ TransactionManager  │
│ Create Transaction  │
│ Status: PENDING     │
│ Generate Txn ID     │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Validate Payment   │
│  - Check balance    │
│  - Verify details   │
│  - Fraud check      │
└──────┬──────────────┘
       │
       ├─── INVALID ──► Status: FAILED
       │                Return error
       │
       └─── VALID ──┐
                    ▼
             ┌──────────────────┐
             │ PaymentProcessor │
             │ Route to Provider│
             │ (Stripe/Razorpay)│
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │ Process Payment  │
             │ Deduct amount    │
             └────────┬─────────┘
                      │
                      ├─── SUCCESS ──┐
                      │               ▼
                      │        ┌─────────────┐
                      │        │   Update    │
                      │        │   Status:   │
                      │        │  SUCCESS    │
                      │        └──────┬──────┘
                      │               │
                      │               ▼
                      │        ┌─────────────┐
                      │        │   Credit    │
                      │        │  Merchant   │
                      │        │   Account   │
                      │        └──────┬──────┘
                      │               │
                      │               ▼
                      │        ┌─────────────┐
                      │        │   Send      │
                      │        │ Confirmation│
                      │        └─────────────┘
                      │
                      └─── FAILURE ──► Status: FAILED
                                       Notify customer

Refund Flow:
┌─────────────────────┐
│  Refund Request     │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Validate Txn       │
│  Check eligibility  │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Process Refund     │
│  Status: REFUNDED   │
└─────────────────────┘
```

---

## 🎨 UML Class Diagram

![Class Diagram](uml/class-diagram.png)

The UML diagram shows relationships between:
- Customer and Transaction (1:N)
- Merchant and Transaction (1:N)
- Transaction and PaymentMethod (N:1)
- PaymentProcessor and PaymentProvider (1:N)

---

## 💻 Code Structure

The `code/` folder contains Java implementation with:

- **Customer.java** - Customer entity
- **Merchant.java** - Merchant account
- **Transaction.java** - Transaction with status tracking
- **PaymentMethod.java** - Abstract payment method
- **CreditCard.java** - Credit card payment
- **DebitCard.java** - Debit card payment
- **UPI.java** - UPI payment
- **Wallet.java** - Digital wallet payment
- **PaymentProcessor.java** - Core payment processing
- **PaymentProvider.java** - External gateway interface
- **TransactionManager.java** - Transaction lifecycle
- **RefundManager.java** - Refund handling
- **Main.java** - Demo scenarios

---

## 🎯 Design Goals & Learning Outcomes

✅ **Multiple payment methods** - Support various payment types  
✅ **Transaction state management** - Track payment lifecycle  
✅ **Security** - Handle sensitive payment data  
✅ **Idempotency** - Prevent duplicate transactions  
✅ **Refund handling** - Process cancellations and refunds  
✅ **Provider abstraction** - Support multiple payment gateways  

---

## 📂 Project Structure
```
payment-gateway/
├── uml/
│   └── class-diagram.png
├── code/
│   └── *.java
└── README.md
```

---

**Interview Ready** | **Clean Code** | **Beginner Friendly**

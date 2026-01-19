# ⚡ Zepto Quick Commerce - Low Level Design

## 📖 Overview
A quick commerce platform that delivers groceries and essentials in 10 minutes. This LLD focuses on inventory management, order fulfillment from dark stores, and rapid delivery assignment.

---

## 🧩 Core Entities/Components
- **Customer** - Places orders for quick delivery
- **DarkStore** - Micro-warehouse with inventory
- **Product** - Items available for purchase
- **Inventory** - Stock management per dark store
- **Order** - Customer order with items
- **DeliveryPartner** - Delivers from dark store to customer
- **OrderRouter** - Routes order to nearest dark store
- **InventoryManager** - Manages stock levels

---

## 🔄 System Workflow

```
┌──────────────┐
│   Customer   │
│ Opens App    │
└──────┬───────┘
       │
       ▼
┌─────────────────────┐
│  Detect Location    │
│  Find nearest       │
│  Dark Store         │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Browse Products    │
│  - Groceries        │
│  - Snacks           │
│  - Beverages        │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Add to Cart        │
│  Check availability │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Place Order        │
│  Promise: 10 mins   │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  OrderRouter        │
│  Route to nearest   │
│  Dark Store with    │
│  stock available    │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  InventoryManager   │
│  Reserve items      │
│  Reduce stock       │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Assign Partner     │
│  Nearest available  │
│  at Dark Store      │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Pick Items         │
│  Status: PICKING    │
│  ⏱ Timer: 2 mins    │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Pack Order         │
│  Status: PACKED     │
│  ⏱ Timer: 1 min     │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Out for Delivery   │
│  Status: DISPATCHED │
│  ⏱ Timer: 7 mins    │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Delivered          │
│  Status: DELIVERED  │
│  ⏱ Total: 10 mins ✓ │
└─────────────────────┘

Dark Store Selection:
┌─────────────────────────────────┐
│  Customer Location: (lat, lng) │
│         ↓                       │
│  Find Dark Stores within 2km   │
│         ↓                       │
│  Check inventory availability  │
│         ↓                       │
│  Select nearest with stock     │
└─────────────────────────────────┘
```

---

## 🎨 UML Class Diagram

![Class Diagram](uml/class-diagram.png)

The UML diagram shows relationships between:
- Customer and Order (1:N)
- DarkStore and Inventory (1:N)
- Order and OrderItem (1:N)
- DeliveryPartner and DarkStore (N:1)

---

## 💻 Code Structure

The `code/` folder contains Java implementation with:

- **Customer.java** - Customer with location
- **DarkStore.java** - Micro-warehouse with location
- **Product.java** - Product entity
- **Inventory.java** - Stock per dark store
- **Order.java** - Order with delivery time promise
- **OrderItem.java** - Items in order
- **DeliveryPartner.java** - Partner assigned to dark store
- **OrderRouter.java** - Route to optimal dark store
- **InventoryManager.java** - Stock management
- **Main.java** - Demo scenarios

---

## 🎯 Design Goals & Learning Outcomes

✅ **Location-based routing** - Find nearest dark store  
✅ **Real-time inventory** - Check stock availability  
✅ **Time-bound delivery** - 10-minute promise tracking  
✅ **Stock reservation** - Prevent overselling  
✅ **Partner assignment** - Optimize for speed  
✅ **Dark store management** - Micro-warehouse operations  

---

## 📂 Project Structure
```
zepto-quick-commerce/
├── uml/
│   └── class-diagram.png
├── code/
│   └── *.java
└── README.md
```

---

**Interview Ready** | **Clean Code** | **Beginner Friendly**

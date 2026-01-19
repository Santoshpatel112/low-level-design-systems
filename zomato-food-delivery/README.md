# 🍔 Zomato Food Delivery - Low Level Design

## 📖 Overview
A food delivery platform that connects customers with restaurants, manages orders, assigns delivery partners, and tracks deliveries in real-time. This LLD focuses on order management and delivery assignment logic.

---

## 🧩 Core Entities/Components
- **Customer** - Places orders, tracks delivery
- **Restaurant** - Menu, availability, location
- **Menu** - Food items with prices
- **Order** - Customer's food order with items
- **DeliveryPartner** - Picks up and delivers orders
- **OrderManager** - Handles order lifecycle
- **DeliveryAssigner** - Assigns nearest available partner
- **Payment** - Handles payment processing

---

## 🔄 System Workflow

```
┌──────────────┐
│   Customer   │
│ Browses Menu │
└──────┬───────┘
       │
       ▼
┌─────────────────────┐
│   Select Items      │
│   Add to Cart       │
│   Choose Restaurant │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│   Place Order       │
│   - Validate items  │
│   - Calculate total │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│   Payment           │
│   Process payment   │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  OrderManager       │
│  Create Order       │
│  Status: PLACED     │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│ DeliveryAssigner    │
│ Find nearest        │
│ available partner   │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Assign Partner     │
│  Status: CONFIRMED  │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Restaurant         │
│  Prepares Food      │
│  Status: PREPARING  │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Partner Pickup     │
│  Status: PICKED_UP  │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Delivery           │
│  Status: DELIVERED  │
│  ⭐ Rate & Review   │
└─────────────────────┘
```

---

## 🎨 UML Class Diagram

![Class Diagram](uml/class-diagram.png)

The UML diagram shows relationships between:
- Customer and Order (1:N)
- Restaurant and Menu (1:N)
- Order and OrderItem (1:N)
- DeliveryPartner and Order (1:N)

---

## 💻 Code Structure

The `code/` folder contains Java implementation with:

- **Customer.java** - Customer entity with address
- **Restaurant.java** - Restaurant with menu and location
- **Menu.java** - Menu items and pricing
- **Order.java** - Order with items and status
- **OrderItem.java** - Individual item in order
- **DeliveryPartner.java** - Partner with location and availability
- **OrderManager.java** - Order lifecycle management
- **DeliveryAssigner.java** - Partner assignment algorithm
- **Payment.java** - Payment processing
- **Main.java** - Demo scenarios

---

## 🎯 Design Goals & Learning Outcomes

✅ **Order state management** - Track order through multiple states  
✅ **Delivery assignment** - Nearest partner algorithm  
✅ **Real-time tracking** - Update order status  
✅ **Restaurant availability** - Handle open/closed status  
✅ **Payment integration** - Process different payment methods  

---

## 📂 Project Structure
```
zomato-food-delivery/
├── uml/
│   └── class-diagram.png
├── code/
│   └── *.java
└── README.md
```

---

**Interview Ready** | **Clean Code** | **Beginner Friendly**

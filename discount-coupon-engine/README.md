# 🎟️ Discount Coupon Engine - Low Level Design

## 📖 Overview
A coupon management system that creates, validates, and applies discount coupons to orders. This LLD focuses on coupon types, validation rules, and discount calculation logic.

---

## 🧩 Core Entities/Components
- **Coupon** - Discount code with rules
- **CouponType** - Percentage, Flat, BuyXGetY, FreeShipping
- **User** - Customer applying coupon
- **Order** - Shopping cart with items
- **CouponValidator** - Validates coupon eligibility
- **DiscountCalculator** - Calculates final discount
- **CouponManager** - Creates and manages coupons
- **UsageTracker** - Tracks coupon usage per user

---

## 🔄 System Workflow

```
┌──────────────┐
│   Admin      │
│ Create Coupon│
└──────┬───────┘
       │
       ▼
┌─────────────────────┐
│  Define Coupon      │
│  - Code: SAVE20     │
│  - Type: Percentage │
│  - Value: 20%       │
│  - Min Order: ₹500  │
│  - Max Discount: ₹200│
│  - Valid Till: Date │
│  - Usage Limit: 100 │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Store Coupon       │
│  Status: ACTIVE     │
└─────────────────────┘


Customer Flow:
┌──────────────┐
│   Customer   │
│ Has Cart     │
│ Total: ₹800  │
└──────┬───────┘
       │
       ▼
┌─────────────────────┐
│  Enter Coupon Code  │
│  "SAVE20"           │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  CouponValidator    │
│  Check:             │
│  ✓ Coupon exists?   │
│  ✓ Is active?       │
│  ✓ Not expired?     │
│  ✓ Usage limit OK?  │
│  ✓ User eligible?   │
│  ✓ Min order met?   │
└──────┬──────────────┘
       │
       ├─── INVALID ──► Show error message
       │                "Coupon expired"
       │
       └─── VALID ──┐
                    ▼
             ┌──────────────────┐
             │DiscountCalculator│
             │ Calculate:       │
             │ Cart: ₹800       │
             │ 20% = ₹160       │
             │ Max: ₹200 ✓      │
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │  Apply Discount  │
             │  Original: ₹800  │
             │  Discount: -₹160 │
             │  Final: ₹640     │
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │  Update Usage    │
             │  User: +1        │
             │  Total: +1       │
             └────────┬─────────┘
                      │
                      ▼
             ┌──────────────────┐
             │  Show Success    │
             │  "₹160 saved!"   │
             └──────────────────┘

Coupon Types:
┌─────────────────────────────────────┐
│ 1. Percentage: 20% off             │
│ 2. Flat: ₹100 off                  │
│ 3. BuyXGetY: Buy 2 Get 1 Free      │
│ 4. FreeShipping: No delivery charge│
└─────────────────────────────────────┘
```

---

## 🎨 UML Class Diagram

![Class Diagram](uml/class-diagram.png)

The UML diagram shows relationships between:
- Coupon and CouponType (inheritance)
- User and CouponUsage (1:N)
- Order and Coupon (N:1)
- CouponValidator and Coupon (dependency)

---

## 💻 Code Structure

The `code/` folder contains Java implementation with:

- **Coupon.java** - Base coupon entity
- **PercentageCoupon.java** - Percentage discount
- **FlatCoupon.java** - Flat amount discount
- **BuyXGetYCoupon.java** - Buy X Get Y free
- **FreeShippingCoupon.java** - Free delivery
- **User.java** - Customer entity
- **Order.java** - Shopping cart
- **CouponValidator.java** - Validation logic
- **DiscountCalculator.java** - Discount computation
- **CouponManager.java** - CRUD operations
- **UsageTracker.java** - Track usage limits
- **Main.java** - Demo scenarios

---

## 🎯 Design Goals & Learning Outcomes

✅ **Multiple coupon types** - Percentage, flat, BOGO, free shipping  
✅ **Validation rules** - Expiry, usage limits, min order value  
✅ **Discount calculation** - Apply max discount caps  
✅ **Usage tracking** - Per-user and global limits  
✅ **Stacking logic** - Handle multiple coupons (if allowed)  
✅ **Strategy pattern** - Different discount strategies  

---

## 📂 Project Structure
```
discount-coupon-engine/
├── uml/
│   └── class-diagram.png
├── code/
│   └── *.java
└── README.md
```

---

**Interview Ready** | **Clean Code** | **Beginner Friendly**

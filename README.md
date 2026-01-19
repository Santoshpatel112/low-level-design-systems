# 🚀 Low-Level Design (LLD) Systems

This repository contains **Low-Level Design (LLD)** implementations of popular real-world systems.
Each project focuses on **clean object-oriented design**, **UML class diagrams**, and **clear workflows**
to understand how large systems are structured internally.

This repository is useful for:
- LLD interview preparation
- Improving OOP and design pattern knowledge
- Learning real-world system workflows

---

## 📂 Projects Included

| Project | Description |
|-------|------------|
| 🍔 Zomato Food Delivery | Order, delivery, and payment lifecycle |
| 🎵 Spotify Music Player | Playback state, playlist, and queue handling |
| 💳 Payment Gateway | Transaction processing and failure handling |
| 🎟️ Discount Coupon Engine | Rule-based discount and validation system |
| ⚡ Zepto Quick Commerce | 10-minute delivery with inventory logic |
| 💖 Tinder Dating App | Swipe, match detection, and interactions |

---

## 📁 Repository Structure

```text
project-name/
├── uml/        # UML class diagram
├── code/       # Machine-level implementation
└── README.md   # Project explanation

### 🔄 Workflow Diagram
```
User Opens App → Browse Profiles → Swipe Action
                                       ↓
                              ┌────────┴────────┐
                              │                 │
                         Swipe Right       Swipe Left
                          (LIKE)            (PASS)
                              │                 │
                              ↓                 ↓
                    Store in Database    Record & Move On
                              ↓
                    Check: Did other user
                    already like me?
                              ↓
                    ┌─────────┴─────────┐
                    │                   │
                   YES                 NO
                    │                   │
                    ↓                   ↓
            Create Match!         Wait for reciprocal
                    ↓
            Notify Both Users
                    ↓
            Enable Chat
```

### 💻 Core Components
- **User** - Profile data, preferences, location
- **Profile** - Bio, photos, age, gender
- **Swipe** - User action (LIKE/PASS) with timestamp
- **Match** - Bidirectional like record
- **MatchingEngine** - Core logic to detect mutual likes
- **ProfileFeed** - Algorithm to fetch relevant profiles
- **NotificationService** - Send match alerts

[📖 View Full Documentation →](tinder-dating-app/README.md)

---

## 🍔 Zomato Food Delivery

**Location:** `zomato-food-delivery/`  
**Complexity:** High | **Design Patterns:** State, Observer, Strategy, Factory

### 📝 What It Does
Zomato is a food delivery platform connecting customers, restaurants, and delivery partners. Customers browse menus, place orders, make payments, and track deliveries in real-time. The system manages the complete order lifecycle through 7 states, coordinates between multiple actors, and uses location-based algorithms to assign the nearest available delivery partner for efficient delivery.

### 🎯 Real-World Problem Solved
- **Challenge:** How to coordinate multiple entities (customer, restaurant, delivery partner) and manage complex order state transitions while ensuring timely delivery?
- **Solution:** Implement a state machine for orders, use geospatial algorithms to find the nearest delivery partner, provide real-time tracking, and notify all parties at each stage of the order lifecycle.

### 🔑 Key Features
- **Restaurant Management** - Menu items, pricing, availability, operating hours
- **Order Placement** - Add items to cart, apply coupons, checkout
- **Payment Integration** - Multiple payment methods (Card, UPI, Wallet, COD)
- **Smart Partner Assignment** - Location-based algorithm to find nearest partner
- **Order State Machine** - Track order through 7 states (PLACED → DELIVERED)
- **Real-time Tracking** - Live location updates of delivery partner
- **Rating & Reviews** - Post-delivery feedback system


### 🔄 Workflow Diagram
```
Customer → Browse Restaurants → Select Items → Add to Cart
                                                     ↓
                                            Apply Coupon (Optional)
                                                     ↓
                                              Place Order
                                                     ↓
                                            ┌────────┴────────┐
                                            │   PLACED        │
                                            └────────┬────────┘
                                                     ↓
                                            Process Payment
                                                     ↓
                                            ┌────────┴────────┐
                                            │  CONFIRMED      │
                                            └────────┬────────┘
                                                     ↓
                                    Restaurant Accepts & Prepares
                                                     ↓
                                            ┌────────┴────────┐
                                            │  PREPARING      │
                                            └────────┬────────┘
                                                     ↓
                                              Food Ready
                                                     ↓
                                            ┌────────┴────────┐
                                            │    READY        │
                                            └────────┬────────┘
                                                     ↓
                                    Assign Nearest Delivery Partner
                                                     ↓
                                            ┌────────┴────────┐
                                            │  PICKED_UP      │
                                            └────────┬────────┘
                                                     ↓
                                          Partner Delivers
                                                     ↓
                                            ┌────────┴────────┐
                                            │  DELIVERED      │
                                            └─────────────────┘
```

### 💻 Core Components
- **Customer** - User account, addresses, order history
- **Restaurant** - Menu, location, operating hours
- **Order** - Order details, items, status, total
- **DeliveryPartner** - Partner profile, location, availability
- **OrderManager** - Manages order lifecycle and state transitions
- **DeliveryAssigner** - Assigns nearest available partner
- **PaymentProcessor** - Handles payment processing

[📖 View Full Documentation →](zomato-food-delivery/README.md)

---

## 🎵 Spotify Music Player

**Location:** `spotify-music-player/`  
**Complexity:** Low-Medium | **Design Patterns:** Singleton, Command, State

### 📝 What It Does
Spotify is a music streaming platform where users can play songs, create playlists, follow artists, and discover new music. The system manages a vast music library, handles playback controls (play, pause, skip, seek), maintains user libraries, and provides features like shuffle, repeat, and queue management for a seamless listening experience.

### 🎯 Real-World Problem Solved
- **Challenge:** How to manage music playback state, handle queue operations, and provide seamless user experience with features like shuffle, repeat, and queue manipulation?
- **Solution:** Implement a Player with state management (PLAYING/PAUSED/STOPPED), use a Queue data structure for upcoming songs, and apply command pattern for playback controls with undo/redo capabilities.

### 🔑 Key Features
- **Playback Controls** - Play, pause, skip, previous, seek
- **Queue Management** - View and reorder upcoming songs
- **Shuffle Mode** - Randomize playback order
- **Repeat Mode** - Repeat one song or entire playlist
- **User Library** - Liked songs, saved albums, followed artists
- **Playlist Management** - Create, edit, share playlists
- **Search & Discovery** - Find music by title, artist, album


### 🔄 Workflow Diagram
```
User Opens App → Search/Browse Music → Select Song
                                           ↓
                                    ┌──────┴──────┐
                                    │   Options   │
                                    └──────┬──────┘
                                           ↓
                    ┌──────────────────────┼──────────────────────┐
                    │                      │                      │
              Play Now              Add to Queue           Add to Playlist
                    ↓                      ↓                      ↓
            ┌───────────────┐      ┌──────────────┐      ┌──────────────┐
            │ Player Loads  │      │ Queue Updated│      │Playlist Saved│
            │ State: PLAYING│      └──────────────┘      └──────────────┘
            └───────┬───────┘
                    ↓
        ┌───────────┴───────────┐
        │   Playback Controls   │
        │  ⏸ Pause  ⏭ Skip     │
        │  🔀 Shuffle 🔁 Repeat │
        │  🔊 Volume  ⏮ Previous│
        └───────────┬───────────┘
                    ↓
            Song Ends → Check Repeat Mode
                    ↓
        ┌───────────┴───────────┐
        │                       │
    Repeat One            Repeat All/Off
        │                       │
    Replay Song          Play Next in Queue
        │                       │
        └───────────┬───────────┘
                    ↓
            Continue Playback
```

### 💻 Core Components
- **User** - Account, preferences, subscriptions
- **Song** - Title, artist, album, duration
- **Playlist** - User-created song collections
- **Player** - Playback engine with state management
- **Queue** - Ordered list of upcoming songs
- **Library** - User's saved content

[📖 View Full Documentation →](spotify-music-player/README.md)

---

## 💳 Payment Gateway

**Location:** `payment-gateway/`  
**Complexity:** Medium-High | **Design Patterns:** Strategy, Factory, State

### 📝 What It Does
A payment gateway system that processes online transactions securely. It supports multiple payment methods (Credit/Debit Card, UPI, Wallet, Net Banking), handles transaction lifecycle management, performs fraud detection, manages refunds, and integrates with external payment providers. The system ensures secure, reliable, and compliant payment processing for e-commerce platforms.

### 🎯 Real-World Problem Solved
- **Challenge:** How to securely process payments through multiple payment methods while handling failures, ensuring idempotency, and managing refunds?
- **Solution:** Use Strategy pattern for different payment methods, implement transaction state machine, add fraud detection checks, ensure idempotent operations, and provide comprehensive refund management with proper audit trails.

### 🔑 Key Features
- **Multiple Payment Methods** - Card, UPI, Wallet, Net Banking
- **Transaction Management** - Complete lifecycle tracking
- **Fraud Detection** - Real-time security checks
- **Refund Processing** - Full and partial refunds
- **Idempotency** - Prevent duplicate transactions
- **Payment Provider Integration** - Connect with external gateways
- **Transaction History** - Complete audit trail


### 🔄 Workflow Diagram
```
Customer Initiates Payment → Select Payment Method
                                      ↓
                    ┌─────────────────┼─────────────────┐
                    │                 │                 │
                  Card              UPI            Wallet
                    │                 │                 │
                    └─────────────────┼─────────────────┘
                                      ↓
                            Enter Payment Details
                                      ↓
                            Validate Payment Info
                                      ↓
                            ┌─────────┴─────────┐
                            │                   │
                          Valid             Invalid
                            │                   │
                            ↓                   ↓
                    Fraud Detection        Reject & Notify
                            ↓
                    ┌───────┴───────┐
                    │               │
                  Safe          Suspicious
                    │               │
                    ↓               ↓
            Process Payment    Block & Alert
                    ↓
        ┌───────────┴───────────┐
        │                       │
     Success                 Failure
        │                       │
        ↓                       ↓
  ┌──────────┐          ┌──────────┐
  │ COMPLETED│          │  FAILED  │
  └────┬─────┘          └────┬─────┘
       │                     │
       ↓                     ↓
Credit Merchant        Retry/Refund
       ↓
Send Confirmation
```

### 💻 Core Components
- **Customer** - User account and payment methods
- **Transaction** - Payment details and status
- **PaymentMethod** - Strategy interface for different methods
- **PaymentProcessor** - Core payment processing logic
- **FraudDetector** - Security and validation checks
- **RefundManager** - Handle refund requests
- **PaymentProvider** - External gateway integration

[📖 View Full Documentation →](payment-gateway/README.md)

---

## 🎟️ Discount Coupon Engine

**Location:** `discount-coupon-engine/`  
**Complexity:** Medium | **Design Patterns:** Strategy, Factory, Chain of Responsibility

### 📝 What It Does
A flexible coupon management system that handles multiple discount types (Percentage, Flat, BuyXGetY, Free Shipping), validates coupon eligibility, calculates discounts with maximum caps, tracks usage limits (per-user and global), and supports coupon stacking logic. The system enables e-commerce platforms to run promotional campaigns effectively while preventing abuse.

### 🎯 Real-World Problem Solved
- **Challenge:** How to create a flexible discount system that supports multiple coupon types, validates complex rules, prevents misuse, and calculates accurate discounts?
- **Solution:** Use Strategy pattern for different discount types, implement validation chain for eligibility checks, track usage limits in database, and apply business rules for stacking and maximum discount caps.

### 🔑 Key Features
- **Multiple Coupon Types** - Percentage, Flat, BuyXGetY, Free Shipping
- **Validation Rules** - Expiry, usage limits, min order value, user eligibility
- **Discount Calculation** - Accurate calculation with max caps
- **Usage Tracking** - Per-user and global usage limits
- **Coupon Stacking** - Define which coupons can be combined
- **Admin Management** - Create, update, deactivate coupons
- **Analytics** - Track coupon performance and usage


### 🔄 Workflow Diagram
```
Admin Creates Coupon → Define Coupon Type
                              ↓
                    ┌─────────┼─────────┐
                    │         │         │
              Percentage   Flat    BuyXGetY
                    │         │         │
                    └─────────┼─────────┘
                              ↓
                    Set Validation Rules
                    (Expiry, Min Order, Limits)
                              ↓
                    Store as ACTIVE Coupon
                              ↓
Customer Applies Coupon → Enter Coupon Code
                              ↓
                    Validate Coupon
                              ↓
        ┌───────────────────┼───────────────────┐
        │                   │                   │
    Is Valid?         Is Expired?        Usage Limit?
        │                   │                   │
        ↓                   ↓                   ↓
      YES                  NO                 Exceeded
        │                   │                   │
        ↓                   └─────────┬─────────┘
Check Min Order Value               │
        ↓                           ↓
    ┌───┴───┐                  Reject Coupon
    │       │                       ↓
  Met    Not Met              Show Error Message
    │       │
    ↓       ↓
Calculate  Reject
Discount
    ↓
Apply to Order
    ↓
Update Usage Count
    ↓
Show Final Price
```

### 💻 Core Components
- **Coupon** - Coupon details and rules
- **DiscountStrategy** - Interface for discount types
- **CouponValidator** - Validation chain
- **DiscountCalculator** - Calculate final discount
- **UsageTracker** - Track usage limits
- **CouponManager** - Admin operations

[📖 View Full Documentation →](discount-coupon-engine/README.md)

---

## ⚡ Zepto Quick Commerce

**Location:** `zepto-quick-commerce/`  
**Complexity:** High | **Design Patterns:** Strategy, Observer, Factory

### 📝 What It Does
Zepto is a 10-minute grocery delivery system using dark stores (micro-warehouses) strategically located in neighborhoods. The system detects customer location, routes orders to the nearest dark store with available inventory, reserves stock in real-time, assigns delivery partners, and ensures ultra-fast delivery through optimized picking, packing, and routing algorithms.

### 🎯 Real-World Problem Solved
- **Challenge:** How to deliver groceries in 10 minutes while managing inventory across multiple dark stores, preventing overselling, and optimizing delivery routes?
- **Solution:** Use location-based routing to select nearest dark store, implement real-time inventory management with stock reservation, optimize picking/packing workflows, and use smart delivery partner assignment with time-bound tracking.

### 🔑 Key Features
- **Dark Store Management** - Micro-warehouses with local inventory
- **Location-Based Routing** - Select nearest store with stock
- **Real-time Inventory** - Live stock updates and synchronization
- **Stock Reservation** - Prevent overselling during order processing
- **10-Minute Promise** - Time-bound delivery tracking
- **Optimized Picking** - Efficient warehouse picking routes
- **Smart Partner Assignment** - Assign based on location and availability


### 🔄 Workflow Diagram
```
Customer Opens App → Detect GPS Location
                            ↓
                Find Dark Stores within 2km
                            ↓
                    ┌───────┴───────┐
                    │               │
              Store A (1.2km)  Store B (1.8km)
                    │               │
                    └───────┬───────┘
                            ↓
                Browse Available Products
                (Only items in stock at nearest store)
                            ↓
                Add Items to Cart
                            ↓
                Place Order (10-min promise)
                            ↓
                Route to Optimal Dark Store
                            ↓
                Reserve Stock (Lock Inventory)
                            ↓
                    ┌───────┴───────┐
                    │               │
              Stock Available   Out of Stock
                    │               │
                    ↓               ↓
            Assign Partner    Suggest Alternative
                    ↓
            ┌───────┴───────┐
            │   Time Split  │
            │ Pick: 2 min   │
            │ Pack: 1 min   │
            │ Deliver: 7min │
            └───────┬───────┘
                    ↓
            Partner Picks Items
                    ↓
            Pack & Verify Order
                    ↓
            Out for Delivery
                    ↓
            Deliver to Customer
                    ↓
            ┌───────┴───────┐
            │               │
        On Time        Delayed
        (< 10min)      (> 10min)
            │               │
            ↓               ↓
        Success      Compensation
```

### 💻 Core Components
- **Customer** - User account and location
- **DarkStore** - Micro-warehouse with inventory
- **Product** - Items with stock levels
- **Order** - Order details with time tracking
- **InventoryManager** - Real-time stock management
- **StoreRouter** - Select optimal dark store
- **DeliveryPartner** - Partner with location tracking

[📖 View Full Documentation →](zepto-quick-commerce/README.md)

---

## 🎓 Learning Path

### Recommended Order by Complexity

1. **Beginner:** Spotify Music Player (simple state management)
2. **Intermediate:** Discount Coupon Engine (validation logic)
3. **Intermediate:** Tinder Dating App (matching algorithms)
4. **Advanced:** Payment Gateway (security & transactions)
5. **Advanced:** Zomato Food Delivery (state machines)
6. **Expert:** Zepto Quick Commerce (location-based optimization)

---

## 💡 Key Concepts Covered

✅ **Object-Oriented Design** - Classes, inheritance, polymorphism, encapsulation  
✅ **Design Patterns** - Strategy, Factory, Observer, State, Singleton, Builder  
✅ **SOLID Principles** - Single responsibility, Open/closed, Liskov substitution  
✅ **State Management** - Order states, transaction states, player states  
✅ **Algorithm Design** - Matching, routing, discount calculation  
✅ **Real-world Systems** - Production-ready architectures  
✅ **Location-based Services** - Geospatial algorithms and routing  
✅ **Payment Processing** - Security, fraud detection, refunds  

---

## 🎯 Design Patterns Used

| Pattern | Projects |
|---------|----------|
| **Strategy** | Payment Gateway, Coupon Engine, Zomato, Zepto |
| **Factory** | Payment Gateway, Coupon Engine, Zomato |
| **Observer** | Tinder (notifications), Zomato (order updates), Zepto |
| **State** | Zomato (order states), Payment Gateway (transaction states), Spotify |
| **Singleton** | All projects (managers/controllers) |
| **Builder** | Tinder (profile), Zomato (order) |
| **Command** | Spotify (playback controls) |
| **Chain of Responsibility** | Coupon Engine (validation chain) |

---

## 🛠️ Tech Stack

- **Language:** Java
- **Paradigm:** Object-Oriented Programming (OOP)
- **Design:** SOLID Principles
- **Documentation:** UML Class Diagrams
- **Visualization:** ASCII Workflow Diagrams

---

## 📖 How to Use This Repository

### For Interview Preparation:
1. **Study the workflow diagrams** to understand system flow
2. **Review UML diagrams** to see class relationships
3. **Read the code** to understand implementation details
4. **Practice explaining** the design decisions

### For Learning:
1. **Start with simpler projects** (Spotify, Coupon Engine)
2. **Progress to complex ones** (Zomato, Zepto)
3. **Implement variations** to deepen understanding
4. **Compare different approaches** across projects

### For Portfolio:
1. **Clone and customize** the projects
2. **Add your own features** and improvements
3. **Document your changes** in project READMEs
4. **Showcase in interviews** and on your resume

---

## 🤝 Contributing

Feel free to:
- Suggest improvements to existing designs
- Add new features or variations
- Fix bugs or optimize code
- Improve documentation
- Add more system design projects

---

## 📝 License

This repository is open source and available for educational purposes.

---

## 🌟 Project Highlights

| Project | Complexity | Key Learning | Real-World Use |
|---------|-----------|--------------|----------------|
| **Tinder** | Medium | Bidirectional matching | Dating apps, social networks |
| **Zomato** | High | State machines, multi-actor coordination | Food delivery, logistics |
| **Spotify** | Low-Medium | State management, queue operations | Music/video streaming |
| **Payment Gateway** | Medium-High | Security, transaction management | E-commerce, fintech |
| **Coupon Engine** | Medium | Validation chains, discount logic | E-commerce promotions |
| **Zepto** | High | Location-based routing, inventory | Quick commerce, grocery delivery |

---

**Built with ❤️ for learning Low-Level Design concepts**

*Perfect for interview preparation, portfolio building, and understanding real-world system design!*

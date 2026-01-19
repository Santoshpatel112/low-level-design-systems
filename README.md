# 🚀 Low-Level Design (LLD) Systems - Portfolio

A comprehensive collection of **real-world system design projects** implemented with clean code, UML diagrams, and detailed workflows. Perfect for interview preparation and understanding object-oriented design patterns.

---

## 📚 Table of Contents

1. [Tinder Dating App](#-tinder-dating-app)
2. [Zomato Food Delivery](#-zomato-food-delivery)
3. [Spotify Music Player](#-spotify-music-player)
4. [Payment Gateway](#-payment-gateway)
5. [Discount Coupon Engine](#-discount-coupon-engine)
6. [Zepto Quick Commerce](#-zepto-quick-commerce)

---

## 💕 Tinder Dating App

**Location:** `tinder-dating-app/`  
**Complexity:** Medium | **Design Patterns:** Observer, Strategy, Builder

### 📝 What It Does
Tinder is a location-based dating app where users create profiles, browse potential matches, and swipe right (like) or left (pass) on other profiles. When two users mutually like each other, a "match" is created, enabling them to chat. The system handles millions of swipes daily and must efficiently detect mutual likes in real-time.

### 🎯 Real-World Problem Solved
- **Challenge:** How to efficiently match users based on mutual interest without revealing who liked whom until both parties express interest?
- **Solution:** Store swipes in a database and check for bidirectional likes. Only create a match when User A likes User B AND User B has already liked User A.

### 🔑 Key Features
- **Profile Management** - Users create profiles with photos, bio, age, gender, and location
- **Preference Filtering** - Set age range, distance radius, and gender preferences
- **Swipe Mechanism** - Swipe right to like, left to pass
- **Matching Algorithm** - Detect mutual likes and create matches instantly
- **Real-time Notifications** - Both users get notified when a match occurs
- **Chat System** - Matched users can message each other
- **Profile Feed** - Algorithm to show relevant profiles based on preferences

### 🏗️ System Architecture
```
┌─────────────────────────────────────────────────────────────┐
│                        TINDER SYSTEM                        │
└─────────────────────────────────────────────────────────────┘

┌──────────┐         ┌──────────────┐         ┌──────────┐
│  User A  │────────▶│ ProfileFeed  │◀────────│  User B  │
└──────────┘         └──────────────┘         └──────────┘
     │                      │                       │
     │ Swipe Right         │                       │ Swipe Right
     ▼                      ▼                       ▼
┌──────────────────────────────────────────────────────────┐
│              MatchingEngine (Core Logic)                 │
│  - Check if User B already liked User A?                 │
│  - If YES → Create Match                                 │
│  - If NO → Store swipe, wait for reciprocal              │
└──────────────────────────────────────────────────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │   Match?    │
                    └─────────────┘
                      /         \
                    NO           YES
                    │             │
              ─────────┐    ┌──────────┐
            │  Store   │    │  Create  │
            │  Swipe   │    │  Match   │
            └──────────┘    └──────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │ Notify Both     │
                         │ "It's a Match!" │
                         └─────────────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │  Enable Chat    │
                         │   A ↔ B         │
                         └─────────────────┘
```

### 🔄 Detailed Workflow

**Step 1: User Opens App**
```
User A logs in → System fetches User A's preferences
                 (Age: 25-35, Distance: 10km, Gender: Female)
```

**Step 2: Profile Feed Generation**
```
ProfileFeed Algorithm:
1. Find users within 10km radius
2. Filter by age range (25-35)
3. Filter by gender preference
4. Exclude already swiped profiles
5. Exclude matched profiles
6. Return stack of profiles
```

**Step 3: Swipe Action**
```
User A sees User B's profile
   │
   ├─ Swipe LEFT (Pass)
   │  └─ Store: SwipeRecord(userA, userB, PASS, timestamp)
   │     └─ Show next profile
   │
   └─ Swipe RIGHT (Like)
      └─ Store: SwipeRecord(userA, userB, LIKE, timestamp)
         └─ Check: Did User B already like User A?
```

**Step 4: Match Detection**
```
MatchingEngine.checkMatch(userA, userB):
   │
   ├─ Query: SELECT * FROM swipes 
   │         WHERE user_id = userB 
   │         AND target_user_id = userA 
   │         AND action = 'LIKE'
   │
   ├─ If NOT FOUND:
   │  └─ No match yet, wait for User B to swipe
   │
   └─ If FOUND:
      └─ MATCH! Create Match record
         └─ Match(userA, userB, timestamp)
```

**Step 5: Notification & Chat**
```
Match Created
   │
   ├─ Send push notification to User A: "You matched with User B!"
   ├─ Send push notification to User B: "You matched with User A!"
   │
   └─ Create ChatRoom(matchId, userA, userB)
      └─ Enable messaging between users
```

### 💻 Core Components

| Component | Responsibility |
|-----------|---------------|
| **User** | Profile data, preferences, location |
| **Profile** | Bio, photos, age, gender |
| **Swipe** | User action (LIKE/PASS) with timestamp |
| **Match** | Bidirectional like record |
| **Chat** | Messaging between matched users |
| **MatchingEngine** | Core logic to detect mutual likes |
| **ProfileFeed** | Algorithm to fetch relevant profiles |
| **NotificationService** | Send match alerts |

### 🎓 What You'll Learn

✅ **Bidirectional Matching Logic** - How to efficiently detect mutual interest  
✅ **Observer Pattern** - Notify users when matches occur  
✅ **Builder Pattern** - Construct complex profile objects  
✅ **Database Indexing** - Optimize swipe queries for performance  
✅ **Real-time Notifications** - Push notifications to both users  
✅ **Privacy Design** - Don't reveal who liked whom until mutual  
✅ **Scalability** - Handle millions of swipes per day  

### 🔧 Technical Challenges

1. **Performance:** How to quickly check if User B liked User A?
   - **Solution:** Index swipes table on (user_id, target_user_id, action)

2. **Race Conditions:** What if both users swipe       ▼             ▼
          sly?
   - **Solution:** Use database transactions to prevent duplicate matches

3. **Privacy:** Don't show who liked you until you like them back
   - **Solution:** Only reveal match after bidirectional confirmation

[📖 View Full Documentation →](tinder-dating-app/README.md)

---

## 🍔 Zomato Food Delivery

**Location:** `zomato-food-delivery/`  
**Complexity:** High | **Design Patterns:** State, Observer, Strategy, Factory

### 📝 What It Does
Zomato is a food delivery platform that connects hungry customers with restaurants and delivery partners. Customers browse menus, place orders, make payments, and track their food in real-time. The system coordinates between three actors: customers, restaurants, and delivery partners, managing the entire order lifecycle from placement to delivery.

### 🎯 Real-World Problem Solved
- **Challenge:** How to coordinate multiple entities (customer, restaurant, delivery partner) and manage order state transitions while ensuring timely delivery?
- **Solution:** Implement a state machine for orders, use location-based algorithms to assign the nearest available delivery partner, and provide real-time status updates to all parties.

### 🔑 Key Features
- **Restaurant Management** - Menu items, pricing, availability, operating hours
- **Order Placement** - Add items to cart, apply coupons, checkout
- **Payment Integration** - Multiple payment methods (card, UPI, wallet, COD)
- **Smart Partner Assignment** - Find nearest available delivery partner
- **Order State Machine** - Track order through 7 states
- **Real-time Tracking** - Live location updates of delivery partner
- **Ra       Reviews** - Post-delivery feedback system

### 🏗️ System Architecture
```
┌─────────────────────────────────────────────────────────────────┐
│                     ZOMATO DELIVERY SYSTEM                      │
└─────────────────────────────────────────────────────────────────┘

┌──────────┐         ┌────────────┐         ┌─────────────────┐
    stomer │────────▶│ Restaurant │────────▶│ DeliveryPartner │
└──────────┘         └────────────┘         └─────────────────┘
     │                     │                         │
     │ Browse Menu         │ Prepare Food            │ Deliver
     ▼                                    ↓
                                Partner Picks Up
                                          ↓
                                    Delivered
```

### Learning Outcomes
✅ Order state machine (Placed → Confirmed → Preparing → Picked → Delivered)  
✅ Location-based partner assignment  
✅ Real-time tracking  
✅ Multi-entity coordination

[View Full Documentation →](zomato-food-delivery/README.md)

---

## 🎵 Spotify Music Player

**Location:** `spotify-music-player/`

### Overview
A music streaming platform with playlist management, playback controls, and music library organization.

### Key Features
- Song, album, and artist management
- Playlist creation and management
- Playback controls (play, pause, skip, shuffle, repeat)
- Queue management
- User library (liked songs, saved playlists)

### Core Components
```
User → Library → Playlist → Song
         ↓          ↓
      Player → Queue
```

### Workflow
```
User Browses Music → Select Song → Add to Queue
                                        ↓
                                   Play Song
                                        ↓
                        Controls: ⏸ ⏭ ⏮ 🔀 🔁
                                        ↓
                              Save to Library
                                        ↓
                            Create/Update Playlist
```

### Learning Outcomes
✅ Queue data structure implementation  
✅ State management (playing, paused, stopped)  
✅ Playlist CRUD operations  
✅ Shuffle and repeat algorithms

[View Full Documentation →](spotify-music-player/README.md)

---

## 💳 Payment Gateway

**Location:** `payment-gateway/`

### Overview
A secure payment processing system supporting multiple payment methods with transaction management and refund handling.

### Key Features
- Multiple payment methods (Credit/Debit Card, UPI, Wallet)
- Transaction lifecycle management
- Payment validation and fraud checks
- Refund processing
- Integration with external payment providers

### Core Components
```
Customer → PaymentMethod → Transaction → Merchant
              ↓                ↓
      PaymentProcessor → PaymentProvider
                             ↓
                      RefundManager
```

### Workflow
```
Customer Initiates Payment → Select Payment Method
                                      ↓
                              Enter Payment Details
                                      ↓
                              Validate Payment
                                      ↓
                          Process via Provider
                                      ↓
                    Success → Credit Merchant
                                      ↓
                              Send Confirmation
```

### Learning Outcomes
✅ Strategy pattern for payment methods  
✅ Transaction state management  
✅ Idempotency handling  
✅ Security best practices  
✅ Refund workflow

[View Full Documentation →](payment-gateway/README.md)

---

## 🎟️ Discount Coupon Engine

**Location:** `discount-coupon-engine/`

### Overview
A flexible coupon management system with multiple discount types, validation rules, and usage tracking.

### Key Features
- Multiple coupon types (Percentage, Flat, BuyXGetY, FreeShipping)
- Coupon validation (expiry, usage limits, min order value)
- Discount calculation with max caps
- Per-user and global usage tracking
- Coupon stacking logic

### Core Components
```
Admin → CouponManager → Coupon Types
                            ↓
Customer → Order → CouponValidator
                       ↓
              DiscountCalculator
                       ↓
              UsageTracker
```

### Workflow
```
Admin Creates Coupon → Define Rules
                           ↓
                    Store as ACTIVE
                           ↓
Customer Applies Code → Validate Coupon
                           ↓
                    Calculate Discount
                           ↓
                    Apply to Order
                           ↓
                    Update Usage Count
```

### Learning Outcomes
✅ Strategy pattern for discount types  
✅ Complex validation logic  
✅ Usage limit tracking  
✅ Discount calculation algorithms

[View Full Documentation →](discount-coupon-engine/README.md)

---

## ⚡ Zepto Quick Commerce

**Location:** `zepto-quick-commerce/`

### Overview
A 10-minute delivery system using dark stores (micro-warehouses) with location-based routing and real-time inventory management.

### Key Features
- Dark store (micro-warehouse) management
- Location-based store selection
- Real-time inventory tracking
- 10-minute delivery promise
- Stock reservation system

### Core Components
```
Customer → DarkStore → Inventory → Product
              ↓           ↓
         OrderRouter  InventoryManager
              ↓
      DeliveryPartner
```

### Workflow
```
Customer Opens App → Detect Location
                          ↓
              Find Nearest Dark Store
                          ↓
              Browse Available Products
                          ↓
              Place Order (10-min promise)
                          ↓
              Route to Optimal Dark Store
                          ↓
              Reserve Stock
                          ↓
              Assign Partner
                          ↓
              Pick → Pack → Deliver
              (2min) (1min)  (7min)
```

### Learning Outcomes
✅ Location-based routing algorithms  
✅ Real-time inventory management  
✅ Stock reservation to prevent overselling  
✅ Time-bound delivery tracking  
✅ Dark store optimization

[View Full Documentation →](zepto-quick-commerce/README.md)

---

## 📂 Project Structure

```
low-level-design-systems/
├── tinder-dating-app/
│   ├── uml/
│   │   └── class-diagram.png
│   ├── code/
│   │   └── *.java
│   └── README.md
│
├── zomato-food-delivery/
│   ├── uml/
│   │   └── class-diagram.png
│   ├── code/
│   │   └── *.java
│   └── README.md
│
├── spotify-music-player/
│   ├── uml/
│   │   └── class-diagram.png
│   ├── code/
│   │   └── *.java
│   └── README.md
│
├── payment-gateway/
│   ├── uml/
│   │   └── class-diagram.png
│   ├── code/
│   │   └── *.java
│   └── README.md
│
├── discount-coupon-engine/
│   ├── uml/
│   │   └── class-diagram.png
│   ├── code/
│   │   └── *.java
│   └── README.md
│
├── zepto-quick-commerce/
│   ├── uml/
│   │   └── class-diagram.png
│   ├── code/
│   │   └── *.java
│   └── README.md
│
└── README.md (this file)
```

---

## 🎯 Design Patterns Used

| Pattern | Projects |
|---------|----------|
| **Strategy** | Payment Gateway, Coupon Engine |
| **Factory** | Payment Gateway, Coupon Engine |
| **Observer** | Tinder (notifications), Zomato (order updates) |
| **State** | Zomato (order states), Payment Gateway (transaction states) |
| **Singleton** | All projects (managers/controllers) |
| **Builder** | Tinder (profile), Zomato (order) |

---

## 🛠️ Tech Stack

- **Language:** Java
- **Paradigm:** Object-Oriented Programming (OOP)
- **Design:** SOLID Principles
- **Documentation:** UML Class Diagrams
- **Visualization:** ASCII Workflow Diagrams

---

## 💡 Key Concepts Covered

✅ **Object-Oriented Design** - Classes, inheritance, polymorphism  
✅ **Design Patterns** - Strategy, Factory, Observer, State, Singleton  
✅ **SOLID Principles** - Single responsibility, Open/closed, etc.  
✅ **State Management** - Order states, transaction states  
✅ **Algorithm Design** - Matching, routing, discount calculation  
✅ **Real-world Systems** - Production-ready architectures  

---

## 📖 How to Use This Repository

1. **For Interview Prep:**
   - Study each project's workflow
   - Understand the UML diagrams
   - Practice explaining the design decisions

2. **For Learning:**
   - Start with one project
   - Read the README thoroughly
   - Study the code implementation
   - Try to implement variations

3. **For Portfolio:**
   - Clone and customize
   - Add your own features
   - Deploy and showcase

---

## 🤝 Contributing

Feel free to:
- Add more features to existing projects
- Suggest improvements to designs
- Fix bugs or optimize code
- Add more LLD projects

## 👨‍💻 Author

Created with ❤️ for learning Low-Level Design and System Design concepts.

**Interview Ready** | **Production Quality** | **Beginner Friendly**

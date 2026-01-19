# 💕 Tinder Dating App - Low Level Design

## 📖 Overview
A dating application system that allows users to create profiles, swipe on other profiles, match with mutual likes, and chat with matches. This LLD focuses on the core matching algorithm and user interaction flow.

---

## 🧩 Core Entities/Components
- **User** - Profile with bio, photos, preferences (age, gender, location)
- **Profile** - User's dating profile information
- **Swipe** - User action (Like/Pass) on another profile
- **Match** - Created when two users like each other
- **Chat** - Messaging between matched users
- **MatchingEngine** - Handles swipe logic and match creation
- **ProfileFeed** - Generates potential matches for users

---

## 🔄 System Workflow

```
┌─────────────┐
│   User A    │
│  Opens App  │
└──────┬──────┘
       │
       ▼
┌─────────────────────┐
│  ProfileFeed        │
│  - Fetch profiles   │
│  - Apply filters    │
│  - Show User B      │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│   User A Swipes     │
│   ◄── Left (Pass)   │
│   ──► Right (Like)  │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  MatchingEngine     │
│  Check if User B    │
│  already liked A?   │
└──────┬──────────────┘
       │
       ├─── NO ──► Store swipe, continue
       │
       └─── YES ──┐
                  ▼
           ┌──────────────┐
           │ Create Match │
           │  A ↔ B       │
           └──────┬───────┘
                  │
                  ▼
           ┌──────────────┐
           │ Notify Both  │
           │   "It's a    │
           │    Match!"   │
           └──────┬───────┘
                  │
                  ▼
           ┌──────────────┐
           │  Open Chat   │
           │   A ↔ B      │
           └──────────────┘
```

---

## 🎨 UML Class Diagram

![Class Diagram](uml/class-diagram.png)

The UML diagram shows relationships between:
- User and Profile (1:1)
- User and Swipe (1:N)
- Match and Users (M:N)
- Match and Chat (1:1)

---

## 💻 Code Structure

The `code/` folder contains Java implementation with:

- **User.java** - User entity with profile data
- **Profile.java** - Profile details and preferences
- **Swipe.java** - Swipe action (Like/Pass) with timestamp
- **Match.java** - Match entity linking two users
- **Chat.java** - Chat session between matched users
- **MatchingEngine.java** - Core logic for match detection
- **ProfileFeed.java** - Algorithm to fetch and filter profiles
- **Main.java** - Demo/test scenarios

---

## 🎯 Design Goals & Learning Outcomes

✅ **Bidirectional matching logic** - Understand mutual like detection  
✅ **Efficient swipe storage** - Handle high-volume user actions  
✅ **Profile filtering** - Apply user preferences (age, distance, gender)  
✅ **Real-time notifications** - Match alerts to both users  
✅ **Scalability considerations** - Design for millions of users  

---

## 📂 Project Structure
```
tinder-dating-app/
├── uml/
│   └── class-diagram.png
├── code/
│   └── *.java
└── README.md
```

---

**Interview Ready** | **Clean Code** | **Beginner Friendly**

──t IZomato─────────┐
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

### 📝 is a food delivery platform hungry customers wtaurants and delivery partneromers browse menus, place ords, and track theiral-time. The stes between three actortomernts, and delivery partners, the entirfecycle from t to delivery.

#orld Problemlved
- **🎯 Real-World Problem Solveate muities (cestaurant, delr) and manage ore transitions whensuring timely deliy?
- **Solution:** Impw to eff state machtch users base, use locationterest without revealing gn the nearest until both parties partner, and provtime statu all parts.

### 🔑 K
- **Restaurant resment** - Menu items, png, avaity, opg hours
- **Order Placeagement- Add items to ca profiles wiupons, che bio, age, gender, and location
- **Payment In Filteion** - Multiple rangent methods (caius, and wallet, COferences
- **Smart Pachaer Assignment** ight t nearest availabpassr
- **Order St AlgMachine** - Track ordual likegh 7  creat
- **Real-time Notifications**ve loca uon updates of deliveen aartner
- **Raat Sys Reviews** -hed t-delivery feedbaceach oth

### 🏗️ System Aecture
```
```──────────────────────────────────────────────
┌──────         ────────MATO DELIVERY SYS───────────      ────┐   │
└────                    TINDE─────────────────               │──┘

┌─────   ┌────────────┐         ┌─────────────
┌─Customer │──────── ┌─────aurant │──         DeliveryP──┐r │
└──────────│───────  └─────ileFeed┘         └────────────│


## 🎵 Spotify Music Player

**Location:** `spotify-music-player/`  
**Complexity:** Low-Medium | **Design Patterns:** Singleton, Command, State

### 📝 What It Does
Spotify is a music streaming platform where users can play songs, create playlists, follow artists, and discover new music. The system manages a vast music library, handles playback controls, maintains user libraries, and provides features like shuffle, repeat, and queue management.

### 🎯 Real-World Problem Solved
- **Challenge:** How to manage music playback state, handle queue operations, and provide
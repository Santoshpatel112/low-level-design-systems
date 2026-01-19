# 🎵 Spotify Music Player - Low Level Design

## 📖 Overview
A music streaming platform that allows users to play songs, create playlists, follow artists, and discover music. This LLD focuses on playlist management, playback control, and music recommendation.

---

## 🧩 Core Entities/Components
- **User** - Listener with preferences and playlists
- **Song** - Music track with metadata
- **Artist** - Creator of songs/albums
- **Album** - Collection of songs
- **Playlist** - User-created song collection
- **Player** - Controls playback (play, pause, skip)
- **Queue** - Manages upcoming songs
- **Library** - User's saved songs and playlists

---

## 🔄 System Workflow

```
┌──────────────┐
│     User     │
│  Opens App   │
└──────┬───────┘
       │
       ▼
┌─────────────────────┐
│   Browse Music      │
│   - Songs           │
│   - Albums          │
│   - Playlists       │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│  Select Song        │
│  "Play Song"        │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│   Player            │
│   ▶ Play            │
│   Load song to      │
│   queue             │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│   Playback          │
│   🎵 Now Playing    │
│   ⏸ Pause           │
│   ⏭ Next            │
│   ⏮ Previous        │
│   🔀 Shuffle         │
│   🔁 Repeat          │
└──────┬──────────────┘
       │
       ├──► Add to Playlist
       │
       ├──► Add to Queue
       │
       └──► Like/Save Song
              │
              ▼
       ┌─────────────────┐
       │   Library       │
       │   Save to       │
       │   "Liked Songs" │
       └─────────────────┘

User Actions:
┌─────────────────────┐
│  Create Playlist    │
│  - Add songs        │
│  - Reorder songs    │
│  - Share playlist   │
└─────────────────────┘
```

---

## 🎨 UML Class Diagram

![Class Diagram](uml/class-diagram.png)

The UML diagram shows relationships between:
- User and Playlist (1:N)
- Playlist and Song (M:N)
- Artist and Album (1:N)
- Album and Song (1:N)
- Player and Queue (1:1)

---

## 💻 Code Structure

The `code/` folder contains Java implementation with:

- **User.java** - User entity with library
- **Song.java** - Song with metadata (title, duration, artist)
- **Artist.java** - Artist with albums
- **Album.java** - Album containing songs
- **Playlist.java** - User playlist with songs
- **Player.java** - Playback controls
- **Queue.java** - Song queue management
- **Library.java** - User's saved content
- **Main.java** - Demo scenarios

---

## 🎯 Design Goals & Learning Outcomes

✅ **Playlist management** - Create, update, delete playlists  
✅ **Queue handling** - Manage playback order  
✅ **Playback controls** - Play, pause, skip, shuffle, repeat  
✅ **Library organization** - Save and categorize music  
✅ **State management** - Track current song and playback state  

---

## 📂 Project Structure
```
spotify-music-player/
├── uml/
│   └── class-diagram.png
├── code/
│   └── *.java
└── README.md
```

---

**Interview Ready** | **Clean Code** | **Beginner Friendly**

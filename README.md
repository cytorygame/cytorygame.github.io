# Cytory (Android Play Store App)

An AI-powered Cyberpunk campaign manager for Android/iOS/Web. Uses a FastAPI backend + React Native frontend + OpenAI/Anthropic LLMs to run fully adaptive, narrative-driven adventures.

**Status**: ✅ Version 1.24 (Code 24) Production Ready | Android 15 (16 KB Page Size) Compliant ✅ | Google Play Games on PC Compatible ✅ | Validated Backend ✅ | Full Frontend ✅ | RAG Active ✅

---

## 🏗 Architecture: Local-First & Stateless Compute

This project follows a **Local-First** philosophy to ensure data ownership, offline capability, and low latency.

### 1. Data Ownership (Memory)
- **Source of Truth**: All character templates and campaign sessions are stored locally on the device (`expo-file-system`).
- **Cloud Sync**: Cross-device synchronization is handled via the user's personal **Google Drive** (App Data Folder, 5 slots).
- **Railway Role**: The Railway backend acts as a stateless "Neural Engine." It does not persist player characters permanently.

### 2. Neural Engine (Compute)
- **FastAPI Backend**: Acts as the "Brain." It receives the current game state, processes AI response/mechanics, and returns the updated state.
- **Statelessness**: Every API call (except Auth/Pulses) includes the full `state` object. If the backend restarts, no data is lost because the phone holds the master copy.

### 3. Neural Pulses & Local Rewards (The Bank)
- **Stateful Source**: The Railway database is the **Source of Truth** for **Neural Pulses** (currency) and **Authentication**.
- **Daily / Weekly Free Charges**: Free daily rerolls and free weekly revives are stored locally in `AsyncStorage` (`rewards.ts`), prioritized automatically before pulse deductions, and firewalled from the AI LLM stream.

---

## 🚀 Quick Start

### 1. Backend (FastAPI)
For environment variables and detailed setup, see [backend/README.md](./backend/README.md).
```bash
cd backend
pip install -r requirements.txt
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### 2. Frontend (React Native)
For build instructions and emulator setup, see [frontend/README.md](./frontend/README.md).
```bash
cd frontend
npm install
npx expo run:android
```

---

## 🎮 Core Features

### 🛡️ Safety & Moderation
- **Content Warning**: Mature content advisory and AI unpredictability warning upon entry.
- **Language Filter**: Vulgar language filter for monitoring and blocking (Backend-enforced).
- **Copyright Guard**: System-level protocols to prevent the use of proprietary names (e.g., Arasaka), replaced with imaginary equivalents (SENTIN-EX).

### 📈 Gameplay & Engagement
- **5-Tier Item Rarity System**: Visual gear classification across 5 distinct tiers (⚪ Basic, 🔵 Rare, 🟣 Exceptional, 🟡 Legendary, 🔴 Mythic) with custom badge styling in Fleshsmith Store & Inventory.
- **Quick Sell / Gear Recycling**: 1-tap item recycling in Neural Inventory recovering 10% credit value (5 CR minimum) to monetize scavenged loot.
- **Faceted 3D D20 Die**: Custom 3D polygon D20 renderer (`D20Die.tsx`) with 3D perspective tumbling roll animation and extensible dice skin architecture (`white`, `cyber`, `gold`, `obsidian`).
- **Contact & Feedback Uplink**: In-app `CONTACT_US` popup allowing runners to transmit Suggestions, Feedback, Bug Reports, and Inquiries directly to command database logs.
- **Daily / Weekly / Monthly Rewards**: Daily free tactical rerolls, weekly free nano-revives, and 20 monthly free pulses.
- **Automated Tactical Combat**: D20 dice checks, initiative tracking, damage resolution, and tactical HUD.
- **Google Docs Story Archive**: Export full campaign narration, choices, and combat logs directly into an editable Google Doc on Google Drive.

### 🎨 Website & Marketing Engine (V1.24)
- **Unified Cyberpunk Aesthetic**: Consistent dark-mode neon styling across Home, Player Handbook, and Privacy Policy.
- **Direct Play Store Integration**: High-converting "Get It On Google Play" buttons linked directly to Play Store listing.
- **SEO & Social Previews**: Open Graph, Twitter Cards, and Google Search Schema.org JSON-LD structured data for rich search engine snippets.
- **Quick Jump TOC**: Interactive Table of Contents in Player Handbook for instant section navigation.

---

## 🐞 Recent Fixes & Updates (Version 1.24)

- [x] **Version Code 24 Release**: Incremented version code to 24 (1.24) across `build.gradle`, `app.json`, and `package.json`.
- [x] **Google Play Games on PC Compatibility**: Added `android.hardware.touchscreen` and `telephony` as optional (`required="false"`) in `AndroidManifest.xml`.
- [x] **Squad-Wide Turn Tuning (+1 PTS / Turn)**: Every squad member receives +1 PTS per turn, with bonus points tracked separately in `bonus_points_earned`.
- [x] **0ms Instant Local Loadout & Tuning Actions**: Instant local state updates for equipping, unequipping, quick selling, and committing neural tuning points without blocking UI popups.
- [x] **Squad Roster Management & AI Backstory Swap Narration**: 1-Pulse roster swaps allowing up to 10 active operatives with ordered selection badges (`#1`, `#2`, `#3`...). The AI GM dynamically narrates joining backstories and departing movements.
- [x] **Universal Operative Identity Recalibration**: Editing profiles in Crew seamlessly syncs name changes (`[IDENTITY_BURN]`) and bio-signatures (`[SYSTEM_RECALIBRATION]`) into active campaigns without warning popups.
- [x] **Diegetic Friction Pacing Protocol**: AI GM uses in-universe lockdowns and handler comms to maintain narrative pacing without invisible walls.
- [x] **Single-LLM-Call Action Loop**: Optimized action loop to perform strictly 1 fast AI call per request, eliminating 504 proxy timeouts on history milestones.
- [x] **Quick Sell & Rarity Tiers**: Implemented `/character/inventory/sell/{session_id}` and 5-tier item rarity classification with 36px matched button heights.
- [x] **3D D20 Die Renderer**: Built `<D20Die />` component with 3D perspective rotation and skin theme support.

---

## 🔮 Future Roadmap

- [ ] **Daily Operations [OPS]**: Faction standing contracts, daily login streaks, and high-value bounty targets in the Sprawl.
- [ ] **Custom Dice Skins Shop**: Unlockable/buyable D20 cosmetics (`cyber`, `gold`, `obsidian`) in the Fleshsmith Marketplace.
- [ ] **Expanded Squad Tactics**: Multi-unit combat encounters, squad combo attacks, and vehicle-based road warfare.

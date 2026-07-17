# Saif and Khazama
> A gamified mobile app teaching **economic literacy** through an interactive 10-level journey across Saudi Arabia — from AlUla to NEOM.

---

## Overview

**Saif & Khazama** is a front-end prototype of a bilingual (Arabic/English) educational mobile app built with Expo. Players follow two characters, Saif and Khazama, through iconic Saudi landmarks, completing economic challenges, daily tasks, and investment activities along the way.

The app is fully RTL/LTR aware, richly animated, and runs on both **iOS/Android** (via Expo Go) and **web** (with a phone-frame bezel on desktop).

---

## Features

| Screen | Description |
|---|---|
| 🗺️ **Home / Map** | Interactive heritage-map journey with 10 level nodes, animated character pin, and pulsing current-level indicator |
| 📈 **Journey** | Level-by-level progress list with staggered entrance animations and animated progress bars |
| ✅ **Tasks** | Daily economic challenges grouped by category with completion tracking |
| 🏪 **Store** | Parchment-style marketplace with Build & Cosmetic sections, animated buy flow, and balance display |
| 💹 **Investments** | Portfolio overview with count-up stats, animated progress bars, and project cards |
| 🤝 **More** | Settings hub with language toggle, character profiles, and access to Granny Chat |
| 👵 **Granny Chat** | Bilingual AI-style chat with الجدة (Granny); keyword-matched responses, quick-question chips, and animated bubbles |
| 🏛️ **Level Detail** | Per-level activity list, animated progress fill, hero image, and status badge |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | [Expo](https://expo.dev) SDK 54 + Expo Router (file-based routing) |
| Language | TypeScript |
| UI | React Native core + `expo-linear-gradient`, `expo-blur` |
| Animations | `react-native-reanimated` v4 (`FadeInDown`, `ZoomIn`, spring, shared values) |
| Icons | `@expo/vector-icons` (Ionicons) |
| State | React `useState` / `useContext` — no backend |
| Monorepo | pnpm workspaces |

---

## Project Structure

```
artifacts/saif-khazama/
├── app/
│   ├── (tabs)/
│   │   ├── index.tsx          # Home / heritage map
│   │   ├── journey.tsx        # Level progress list
│   │   ├── tasks.tsx          # Daily tasks
│   │   ├── store.tsx          # Marketplace
│   │   ├── investments.tsx    # Portfolio / investments
│   │   └── more.tsx           # Settings & profiles
│   ├── level/
│   │   └── [id].tsx           # Dynamic level detail
│   ├── granny-chat.tsx        # Chat with الجدة
│   ├── _layout.tsx            # Root stack layout
│   └── +html.tsx              # Web shell (phone-frame bezel)
│
├── components/
│   ├── LevelNode.tsx          # Animated map node
│   ├── TaskCard.tsx           # Task item card
│   ├── MiniGameCard.tsx       # Mini-game card
│   ├── HeritageMeter.tsx      # Progress meter
│   ├── GrandmotherTip.tsx     # Tip overlay
│   ├── CharacterBanner.tsx    # Character display
│   ├── LanguageToggle.tsx     # AR / EN switcher
│   └── ErrorBoundary.tsx      # Error handling
│
├── constants/
│   ├── translations.ts        # All AR + EN strings
│   ├── levels.ts              # 10-level configuration + assets
│   ├── tasks.ts               # Task definitions
│   ├── grannyResponses.ts     # Chat keyword matching + fallback pool
│   ├── regions.ts             # Saudi landmark geographic data
│   └── colors.ts              # Theme palette
│
├── context/
│   └── LanguageContext.tsx    # isRTL + t() + lang toggle
│
├── hooks/
│   └── useColors.ts           # Theme-aware color hook
│
└── assets/
    └── images/                # Map bg, characters, level hero images
```

---

## Design System

| Token | Value |
|---|---|
| Primary purple | `#7C3AED` |
| Warm gold | `#D4A017` |
| Dark background | `#1E0A3C` |
| Parchment card | `#FDF6E3` |
| Card border | `#C8A46E` |

**Typography:** `Inter_400Regular` + `Inter_700Bold` via `expo-google-fonts`  
**Direction:** Per-component RTL via `isRTL` from `LanguageContext` — no forced `I18nManager` flip

---

## Animations

All animations use **`react-native-reanimated` v4**.

- `FadeInDown` — screen/card entrance with staggered delays
- `ZoomIn.springify()` — chat bubbles, badges
- `useSharedValue` loops — pulsing rings, floating character, breathing CTA
- `withSpring` — press feedback on buttons and nodes
- Count-up stats, animated progress bar fills on the Investments screen
- Typing-dot loader in Granny Chat uses the classic `Animated` API (loop compatibility)

---

## Bilingual Support

The app ships in **Arabic (AR)** and **English (EN)**, toggled at runtime.

- All strings live in `constants/translations.ts`
- `LanguageContext` exposes `t(key)`, `lang`, and `isRTL`
- Layout direction is applied per-component with `flexDirection: isRTL ? 'row-reverse' : 'row'`
- Granny Chat responses are bilingual — each response object has `ar` and `en` fields

---

## Getting Started

### Prerequisites

- Node.js 18+
- pnpm 9+
- Expo CLI (`npx expo`)

### Install & Run

```bash
# Install dependencies (from monorepo root)
pnpm install

# Start the Expo dev server
pnpm --filter @workspace/saif-khazama run dev
```

Then scan the QR code with **Expo Go** on your phone, or press `w` to open in the browser.

### Web Build

```bash
cd artifacts/saif-khazama
npx expo export --platform web --output-dir dist
node server/serve.js        # serves dist/ as a SPA
```

On screens ≥ 700 px wide, the app renders inside a centered phone-frame bezel with a purple glow (defined in `app/+html.tsx`).

---

## Prototype Scope

This is a **non-functional front-end prototype**:

- ✅ All data is hardcoded — no API calls, no database
- ✅ State lives in React `useState`; resets on refresh
- ✅ Granny Chat uses local keyword-matching, not a live LLM
- ✅ Purchases in the Store toggle a local `Set` — no payment processing

---

## Journey Map

| Level | Location | Theme |
|---|---|---|
| 1 | AlUla & Diriyah | السوق — The Market |
| 2 | AlUla & Diriyah | القوافل — Caravans |
| 3 | AlUla & Diriyah | المتجر — Trading |
| 4 | NEOM & AlQaadee | المقهى — Café Economics |
| 5 | NEOM | المصنع — Manufacturing |
| 6 | NEOM | رجور — Resources |
| 7 | NEOM & AlQaadee | الشركة — Company |
| 8 | NEOM Expansion | العقار — Real Estate |
| 9 | Future Vision | رجور — Advanced Trading |
| 10 | NEOM & Future | الاستثمار — Investment |

---

## License

This project is a prototype developed for educational purposes. All illustrated assets are AI-generated and intended for demonstration only.

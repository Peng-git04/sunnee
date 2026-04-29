# 🧴 Sunnee Kids — Bottle Configurator

An interactive configurator for customizing the thermal bottle included as a free gift with the first order of the **Sunnee Kids** line.  
Users can choose the color of the cap, body, and bottom from 10 predefined colors, with a real-time preview.

---

## ✨ Features

- **3 guided steps** — cap → body → bottom, with Next / Back navigation
- **10 predefined colors** — a vibrant palette designed for a kids audience
- **Live preview** — the SVG bottle updates in real time with every selection
- **Confirmation screen** — visual summary of the chosen colors upon submission
- **Restart** — users can reset and redo the configuration at any time

---

## 🛠️ Tech Stack

| Technology | Version |
|---|---|
| [Vue 3](https://vuejs.org/) | `^3.x` |
| [TypeScript](https://www.typescriptlang.org/) | `^5.x` |
| [Vite](https://vitejs.dev/) | `^5.x` |

No external UI dependencies — all design is custom scoped CSS.

---

## 📁 Project Structure

```
sunnee-kids-configurator/
├── index.html
├── package.json
├── vite.config.ts
├── tsconfig.json
├── tsconfig.app.json
├── tsconfig.node.json
└── src/
    ├── main.ts
    ├── App.vue
    ├── style.css
    ├── vite-env.d.ts
    ├── data/
    │   └── colors.ts          # Color palette and step definitions
    └── components/
        ├── BottleConfigurator.vue   # Root configurator component
        ├── BottlePreview.vue        # SVG bottle preview
        ├── ColorGrid.vue            # Color selection grid
        └── StepsBar.vue             # Step progress bar
```

---

## 🚀 Installation & Setup

### Prerequisites

- **Node.js** >= 18.x
- **npm** >= 9.x

### Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/your-username/sunnee-kids-configurator.git
cd sunnee-kids-configurator

# 2. Install dependencies
npm install

# 3. Start the development server
npm run dev
```

Open your browser at `http://localhost:5173`.

---

## 📦 Production Build

```bash
# Generate optimized files in the /dist folder
npm run build

# Preview the build locally
npm run preview
```

The `dist/` folder is ready to be deployed on any static hosting platform (Netlify, Vercel, GitHub Pages, etc.).

---

## 🎨 Color Palette

| # | Name | Hex |
|---|---|---|
| 1 | Coral Red | `#FF6B6B` |
| 2 | Sun Orange | `#FF9F43` |
| 3 | Lemon Yellow | `#FFD93D` |
| 4 | Mint Green | `#6BCB77` |
| 5 | Turquoise | `#4ECDC4` |
| 6 | Sky Blue | `#74B9FF` |
| 7 | Dream Lilac | `#A29BFE` |
| 8 | Bubble Pink | `#FD79A8` |
| 9 | Golden Peach | `#FDCB6E` |
| 10 | Pearl Gray | `#B2BEC3` |

---

## 🧩 Components

### `BottleConfigurator.vue`
Root component. Manages global state: current step, chosen colors, and transition to the confirmation screen. Orchestrates all other components.

### `BottlePreview.vue`
Renders the thermal bottle as an SVG. Receives the `[capIdx, bodyIdx, bottomIdx]` tuple as a prop and updates colors in real time via `computed`.

### `ColorGrid.vue`
A 5×2 grid of circular colored buttons. Emits the `select` event with the clicked color's id. Highlights the current selection with a border and checkmark.

### `StepsBar.vue`
A visual three-dot bar with connecting lines. Displays the status of each step: `idle`, `active`, or `done`.

### `data/colors.ts`
Single source of truth for data: exports the `Color` and `Step` interfaces, the `COLORS` array, and the `STEPS` array.

## 📄 License

This project was developed for internal use by the **Sunnee** brand. All rights reserved.

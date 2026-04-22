# 🧴 Sunnee Kids — Bottle Configurator

Configuratore interattivo per la personalizzazione della bottiglia termica in omaggio con il primo ordine della linea **Sunnee Kids**.  
L'utente può scegliere il colore di tappo, corpo e fondo tra 10 colori predefiniti, con anteprima in tempo reale.

---

## ✨ Funzionalità

- **3 step guidati** — tappo → corpo → fondo, con navigazione Avanti / Indietro
- **10 colori predefiniti** — palette vivace pensata per un pubblico kids
- **Anteprima live** — la bottiglia SVG si aggiorna in tempo reale ad ogni selezione
- **Schermata di conferma** — riepilogo visivo dei colori scelti al momento dell'invio
- **Ricomincia** — l'utente può resettare e ripetere la configurazione

---

## 🛠️ Tech Stack

| Tecnologia | Versione |
|---|---|
| [Vue 3](https://vuejs.org/) | `^3.x` |
| [TypeScript](https://www.typescriptlang.org/) | `^5.x` |
| [Vite](https://vitejs.dev/) | `^5.x` |

Nessuna dipendenza UI esterna — tutto il design è custom in CSS scoped.

---

## 📁 Struttura del progetto

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
    │   └── colors.ts          # Palette colori e definizione step
    └── components/
        ├── BottleConfigurator.vue   # Componente root del configuratore
        ├── BottlePreview.vue        # Anteprima SVG della bottiglia
        ├── ColorGrid.vue            # Griglia di selezione colori
        └── StepsBar.vue             # Barra di avanzamento step
```

---

## 🚀 Installazione e avvio

### Prerequisiti

- **Node.js** >= 18.x
- **npm** >= 9.x

### Setup

```bash
# 1. Clona il repository
git clone https://github.com/tuo-username/sunnee-kids-configurator.git
cd sunnee-kids-configurator

# 2. Installa le dipendenze
npm install

# 3. Avvia il server di sviluppo
npm run dev
```

Apri il browser su `http://localhost:5173`.

---

## 📦 Build per produzione

```bash
# Genera i file ottimizzati nella cartella /dist
npm run build

# Testa la build in locale
npm run preview
```

La cartella `dist/` è pronta per essere deployata su qualsiasi hosting statico (Netlify, Vercel, GitHub Pages, ecc.).

---

## 🎨 Palette colori

| # | Nome | Hex |
|---|---|---|
| 1 | Rosso Corallo | `#FF6B6B` |
| 2 | Arancio Sole | `#FF9F43` |
| 3 | Giallo Limone | `#FFD93D` |
| 4 | Verde Menta | `#6BCB77` |
| 5 | Turchese | `#4ECDC4` |
| 6 | Azzurro Cielo | `#74B9FF` |
| 7 | Lilla Sogno | `#A29BFE` |
| 8 | Rosa Bubble | `#FD79A8` |
| 9 | Pesca Dorata | `#FDCB6E` |
| 10 | Grigio Perla | `#B2BEC3` |

---

## 🧩 Componenti

### `BottleConfigurator.vue`
Componente principale. Gestisce lo stato globale: step corrente, colori scelti e transizione alla schermata di conferma. Orchestra gli altri componenti.

### `BottlePreview.vue`
Renderizza la bottiglia termica in SVG. Riceve come prop il tuple `[capIdx, bodyIdx, bottomIdx]` e aggiorna i colori in tempo reale tramite `computed`.

### `ColorGrid.vue`
Griglia 5×2 di bottoni circolari colorati. Emette l'evento `select` con l'id del colore cliccato. Evidenzia la selezione corrente con bordo e segno di spunta.

### `StepsBar.vue`
Barra visiva a tre dot con linee di connessione. Mostra lo stato di ogni step: `idle`, `active` o `done`.

### `data/colors.ts`
Sorgente unica dei dati: esporta le interfacce `Color` e `Step`, l'array `COLORS` e l'array `STEPS`.

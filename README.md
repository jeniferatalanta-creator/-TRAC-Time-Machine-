# ⏳ TRAC Time Machine

> *"What did my wallet look like 6 months ago?"* — Now you can find out.

A **TRAC Intercom** fork that delivers historical wallet analytics with cinematic visual design. Query any TRAC-ecosystem wallet across time and see exactly how your holdings have evolved.

---
<img width="1272" height="831" alt="image" src="https://github.com/user-attachments/assets/4999394a-9ee1-43dd-855a-bf702f9d0871" />

## 🚀 What It Does

TRAC Time Machine is an agent-powered app built on Intercom that lets you **travel back in time** and inspect your wallet's historical state:

- 📅 **Show my wallet 6 months ago** — instant temporal snapshot
- 📊 **Balance vs. Now** — side-by-side comparison with growth %
- 📈 **Analytics** — peak balance, lowest point, tx count, avg monthly change
- 🧾 **Transaction history** — labeled, color-coded entries for the selected period
- 🔗 **Shareable snapshot** — copy your growth summary to share anywhere

### Example Output

```
⏳ TRAC Time Machine

📅 6 months ago:  1,200 TNK
📅 Now:           2,050 TNK
📈 Growth:        +70.8%

Peak:     2,340 TNK
Low:      1,100 TNK
Txs:      31
Avg/Mo:   +141.6 TNK
```

---

## 🖥️ Live App

> **`index.html`** — open directly in any browser, no server needed.

![App Screenshot](./screenshots/screenshot.png)

---

## 🤖 Intercom Agent Integration

This app uses Intercom sidechannels for:
- Fetching wallet state at historical block heights
- Real-time balance diffing via replicated state layer
- Agent-to-agent coordination for multi-token analytics

See [`SKILL.md`](./SKILL.md) for full agent instructions.

---

## 📦 Tech Stack

| Layer | Tech |
|---|---|
| Frontend | Pure HTML/CSS/JS (zero dependencies) |
| Fonts | Orbitron + Space Mono (Google Fonts) |
| P2P Layer | TRAC Intercom sidechannels |
| Data | TRAC Network historical ledger |
| Design | Retro-futuristic terminal aesthetic |

---

## 🔧 Setup & Run

```bash
# 1. Clone this fork
git clone https://github.com/YOUR_USERNAME/intercom.git
cd intercom

# 2. Open the app
open index.html   # macOS
# or just double-click index.html in your file explorer

# 3. For Intercom agent backend (optional):
npm install
npm start
```

---

## 💰 TRAC Payout Address

> trac1tueh2ncs5mnclr3rxrt7maxqqgqpsd2dhz73wmxhwd4cl9ea2unqje0g9j`

*(Replace this with your real TRAC address before submitting to awesome-intercom)*

---

## 🌐 Fork Info

- **Upstream:** https://github.com/Trac-Systems/intercom  
- **Awesome Intercom:** https://github.com/Trac-Systems/awesome-intercom  
- **Project:** TRAC Time Machine — historical wallet analytics agent

---

## 📸 Screenshots

> Add screenshots of the app in `./screenshots/` folder and link them here as proof the app works.

---

## 📝 License

MIT — fork freely, build boldly.

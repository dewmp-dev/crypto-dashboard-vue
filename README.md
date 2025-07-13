# Crypto Dashboard - Vue.js + TypeScript + TailwindCSS

A simple and elegant dashboard for viewing real-time cryptocurrency data.  
Built using **Vue 3**, **TypeScript**, **Tailwind CSS**, and **Chart.js**.

---

## 📸 Screenshots

- Home Page: Search & List top 100 crypto currencies  
- Detail Page: View market data and interactive 7-day price chart

---

## 🚀 Features

- ✅ Top 100 crypto coins fetched from [CoinGecko API](https://www.coingecko.com/en/api)
- 🔍 Search by name or symbol
- 📄 Paginated list view
- 📊 Detail view with market data and price chart
- 🎨 Modern responsive UI with TailwindCSS
- 🧠 Written in TypeScript using Vue 3 Composition API

---

## ⚙️ Tech Stack

- Vue 3
- TypeScript
- Vue Router
- TailwindCSS
- Chart.js + vue-chartjs
- Axios
- Vite

---

## 📦 Project Install

```bash
npm install
npm run dev

📁 Folder Structure
src/
├── views/            → Home & Detail pages
├── components/       → (Optional UI components)
├── router/           → Vue Router setup
├── style.css         → TailwindCSS entry
├── App.vue           → Main layout
├── main.ts           → App entry point

📈 API Used
GET /coins/markets – List top 100 coins

GET /coins/:id – Detail of selected coin

GET /coins/:id/market_chart – Historical price data for chart


🙋‍♀️ Author
Created by Manusavee P. (Dew)

# 🚀 Ascent Wealth — Replit Agent Prompt
### Paste everything below this line directly into Replit Agent

---

Build a complete web app called **"Ascent Wealth"** — a personal investment tracker with a stunning adventure/motivational theme. This is a premium fintech app that feels like Wealthfront meets a video game achievement system. The user should feel like they are literally ascending toward financial freedom — climbing a mountain, gaining altitude, breaking through clouds — as their net worth grows.

---

## 🛠️ Tech Stack

- **React 18 + Vite**
- **Tailwind CSS** (with custom config for extended colors, fonts, animations)
- **Recharts** for all charts and data visualization
- **Framer Motion** for animations and transitions
- **LocalStorage** for full data persistence (no backend needed)
- **Google Fonts**: Import `"Clash Display"` or `"DM Serif Display"` for headings and `"DM Sans"` for body text — load via @import in index.css
- **Lucide React** for icons

---

## 🎨 Visual Design System

### Color Palette (define as Tailwind CSS variables + custom theme)
```
--ascent-void: #030712          /* deep space black background */
--ascent-summit: #0ea5e9        /* sky blue primary */
--ascent-aurora: #6366f1        /* indigo/purple accent */
--ascent-peak: #f59e0b          /* amber gold highlight */
--ascent-growth: #10b981        /* emerald green for gains */
--ascent-loss: #ef4444          /* red for losses */
--ascent-cloud: rgba(255,255,255,0.06)   /* glassmorphism card bg */
--ascent-glow: rgba(99,102,241,0.15)    /* aurora glow */
```

### Global Style Rules
- **Background**: Deep dark (`#030712`) with a full-screen SVG mountain silhouette scene fixed behind everything. The mountains should be layered: dark foreground peaks, mid-range purple/indigo mountains, and a sky gradient from deep navy at bottom to a subtle aurora of teal/indigo at top. The mountains get "taller" (SVG viewBox shifts upward) as total net worth increases — use a CSS custom property `--altitude` (0–100) driven by net worth progress.
- **Cards**: Glassmorphism — `backdrop-blur-xl`, semi-transparent white/indigo borders (`border border-white/10`), subtle inner glow on hover
- **Typography**: DM Serif Display for all large numbers and hero text; DM Sans for labels/body
- **Gradients**: Use multi-stop gradients heavily. Key gradient: `linear-gradient(135deg, #6366f1 0%, #0ea5e9 50%, #10b981 100%)`
- **Glow Effects**: Box shadows with color (e.g., `0 0 40px rgba(99,102,241,0.3)`) on key cards
- **Animations**: Smooth entrance animations (fade up + scale) on all cards using Framer Motion `initial/animate/transition`. Numbers should count up with a spring animation on load/update.

---

## 📁 File Structure

```
src/
  components/
    Layout/
      Sidebar.jsx         — Navigation sidebar
      TopBar.jsx          — Top bar with greeting, dark mode toggle, avatar
    Dashboard/
      NetWorthHero.jsx    — Giant net worth number with airplane/altitude metaphor
      AltitudeBar.jsx     — "Altitude meter" progress bar toward goal
      AssetAllocation.jsx — Donut/pie chart of portfolio breakdown
      PerformanceChart.jsx — Line chart of net worth over time
      QuoteCard.jsx       — Rotating investor quote carousel
    Portfolio/
      PortfolioTable.jsx  — List of all investments
      AddInvestmentModal.jsx — Modal form to add/edit investments
    Goals/
      GoalCard.jsx        — Individual goal with progress
      AddGoalModal.jsx    — Modal to create a new goal
    UI/
      GlassCard.jsx       — Reusable glassmorphism card wrapper
      AnimatedNumber.jsx  — Number that counts up smoothly
      Badge.jsx           — Status badge (gain/loss/neutral)
  hooks/
    usePortfolio.js       — All portfolio state + LocalStorage logic
    useGoals.js           — Goals state + LocalStorage logic
  data/
    quotes.js             — Investor quotes array
    sampleData.js         — Sample portfolio data for first-time users
  pages/
    Dashboard.jsx
    Portfolio.jsx
    Goals.jsx
  App.jsx
  main.jsx
  index.css
```

---

## 🏔️ Background Mountain Scene (SVG)

In `index.css` or a `MountainBackground.jsx` component, render a fixed full-screen SVG with:

1. **Sky gradient**: `#030712` → `#0c1445` → `#1e1b4b` (bottom to top)
2. **Stars**: ~80 tiny white circles randomly positioned in the upper 60%
3. **Back mountain range**: Gentle peaks, fill `#1e1b4b` (very dark indigo)
4. **Mid mountain range**: Sharper peaks, fill `#312e81`
5. **Front mountain range**: Bold peaks, fill `#0f0f1a` (near black)
6. **Clouds**: 3–5 wispy SVG cloud shapes at different heights, very subtle `rgba(255,255,255,0.03)` fill, animated to drift left slowly via CSS keyframes
7. **Altitude indicator**: A tiny glowing airplane icon (`✈`) that rises vertically along the right side of the screen as net worth approaches the goal — position controlled by `--altitude` CSS variable

---

## 🏠 Dashboard Page (`Dashboard.jsx`)

### Section 1 — Hero Net Worth Card (`NetWorthHero.jsx`)
- Full-width glassmorphism card with aurora glow border
- Giant animated number: **Total Net Worth** (e.g., `$124,500`) using `AnimatedNumber`
- Subtitle: **"ALTITUDE: 24,500 ft"** — where altitude in feet = net worth in dollars (playful metaphor)
- Below that: `+$3,200 (2.6%) this month` in emerald green with an up arrow
- A mini sparkline (Recharts `<Sparkline>`) of last 30 days performance
- Tagline rotating between: `"You're above the clouds."` / `"Keep climbing."` / `"The summit is closer than you think."`

### Section 2 — Stats Row (4 cards)
1. **Total Invested** — with a "fuel in tank" icon
2. **Total Gains/Losses** — colored emerald or red
3. **Best Performer** — asset name + % gain
4. **Days Investing** — counter from first investment date

### Section 3 — Charts Row (2 columns)
- **Left**: `PerformanceChart` — Area chart (Recharts `<AreaChart>`) of net worth over time. Gradient fill from indigo to transparent. X-axis = dates, Y-axis = value. Smooth curve. Tooltip with glassmorphism style.
- **Right**: `AssetAllocation` — Recharts `<PieChart>` (donut style) with custom colors per asset class. Legend below with colored dots.

### Section 4 — Altitude Bar (`AltitudeBar.jsx`)
- A wide horizontal progress bar styled like an airplane runway/altitude meter
- Left label: `"Ground Level $0"` → Right label: `"Summit Goal: $[goal amount]"`
- The fill uses the main gradient; a tiny airplane emoji moves along the bar
- Below: `"You are X% of the way to your summit."`

### Section 5 — Quote Card (`QuoteCard.jsx`)
- Glassmorphism card with a subtle mountain icon watermark
- Auto-rotates every 8 seconds (Framer Motion `AnimatePresence` fade transition)
- Large italic serif quote text, smaller attribution below with a mountain `⛰️` or `✈️` icon

---

## 💼 Portfolio Page (`Portfolio.jsx`)

- **Header**: "Your Holdings" with an `+ Add Investment` button (opens `AddInvestmentModal`)
- **Filter tabs**: All | Stocks | Crypto | Real Estate | Cash | Other
- **Portfolio Table** (`PortfolioTable.jsx`):
  - Columns: Asset Name | Type | Quantity | Purchase Price | Current Price | Total Value | Gain/Loss | Gain % | Actions (Edit/Delete)
  - Each row is a glassmorphism card with hover glow
  - Gain/loss column colored green/red with arrow icon
  - Smooth row entrance animations (staggered with Framer Motion)
- **Summary footer**: Total value, total cost basis, total gain/loss

### `AddInvestmentModal.jsx`
- Modal with glassmorphism backdrop blur
- Fields:
  - Asset Name (text)
  - Asset Type (select: Stock, Crypto, Real Estate, Cash, Bond, ETF, Other)
  - Ticker/Symbol (optional)
  - Quantity / Units
  - Purchase Price per unit
  - Current Price per unit
  - Purchase Date
  - Notes (optional)
- **"Add to Portfolio"** button with gradient background
- Validation: all required fields must be filled
- On submit: save to LocalStorage via `usePortfolio` hook, close modal, animate new row in

---

## 🎯 Goals Page (`Goals.jsx`)

- **Header**: "Your Financial Summits" with `+ Set New Goal` button
- Goals displayed as cards in a 2-col grid
- Each `GoalCard.jsx`:
  - Goal title (e.g., "Reach $500k by 2030")
  - Target amount + target date
  - Current progress (auto-calculated from portfolio net worth or manually input)
  - A vertical mountain progress visual: mountain SVG with a colored fill that rises as progress increases — from base to peak
  - Percentage complete
  - "X days remaining" or "ACHIEVED 🏔️" badge
  - Edit / Delete buttons

### `AddGoalModal.jsx`
- Fields: Goal Name, Target Amount ($), Target Date, Link to Portfolio (yes/no), Notes
- Save to LocalStorage via `useGoals` hook

---

## 💾 Data Hooks

### `usePortfolio.js`
```javascript
// Manages investments array in LocalStorage key: 'ascent_portfolio'
// Each investment: { id, name, type, ticker, quantity, purchasePrice, currentPrice, purchaseDate, notes }
// Computed values: totalValue, totalCost, totalGain, gainPercent, allocationByType
// Methods: addInvestment, updateInvestment, deleteInvestment, updateCurrentPrice
// Also stores daily snapshots for performance chart: { date, totalValue }
```

### `useGoals.js`
```javascript
// Manages goals array in LocalStorage key: 'ascent_goals'
// Each goal: { id, name, targetAmount, targetDate, linkedToPortfolio, currentAmount, notes }
// Methods: addGoal, updateGoal, deleteGoal
```

---

## 💬 Investor Quotes (`src/data/quotes.js`)

Include ALL of these quotes exactly:

```javascript
export const quotes = [
  { text: "The stock market is a device for transferring money from the impatient to the patient.", author: "Warren Buffett", icon: "⛰️" },
  { text: "Risk comes from not knowing what you're doing.", author: "Warren Buffett", icon: "✈️" },
  { text: "The investor's chief problem — and even his worst enemy — is likely to be himself.", author: "Benjamin Graham", icon: "⛰️" },
  { text: "In the short run, the market is a voting machine, but in the long run, it is a weighing machine.", author: "Benjamin Graham", icon: "🏔️" },
  { text: "It's far better to buy a wonderful company at a fair price than a fair company at a wonderful price.", author: "Charlie Munger", icon: "✈️" },
  { text: "Invert, always invert. Turn a situation or problem upside down.", author: "Charlie Munger", icon: "⛰️" },
  { text: "He who lives by the crystal ball will eat shattered glass.", author: "Ray Dalio", icon: "🏔️" },
  { text: "The biggest mistake investors make is to believe that what happened in the recent past is likely to persist.", author: "Ray Dalio", icon: "✈️" },
  { text: "Know what you own, and know why you own it.", author: "Peter Lynch", icon: "⛰️" },
  { text: "Behind every stock is a company. Find out what it's doing.", author: "Peter Lynch", icon: "✈️" },
  { text: "The person that turns over the most rocks wins the game.", author: "Peter Lynch", icon: "🏔️" },
  { text: "Time in the market beats timing the market.", author: "Kenneth Fisher", icon: "⛰️" },
];
```

---

## 🌙 Dark/Light Mode

- Default: **Dark mode** (dark is the primary brand)
- Light mode: background becomes `#f0f4ff` (very light blue), cards become white with subtle indigo borders, text goes dark
- Toggle button in `TopBar.jsx` — sun/moon icon, smooth transition
- Persist preference in LocalStorage key `ascent_theme`
- Use Tailwind `dark:` variants throughout

---

## 🎬 Sample Data (First Load Experience)

On first load (no LocalStorage data), populate with sample data to show the app fully:

```javascript
// src/data/sampleData.js
export const samplePortfolio = [
  { id: '1', name: 'Apple Inc.', type: 'Stock', ticker: 'AAPL', quantity: 10, purchasePrice: 150, currentPrice: 189, purchaseDate: '2023-01-15', notes: '' },
  { id: '2', name: 'Bitcoin', type: 'Crypto', ticker: 'BTC', quantity: 0.5, purchasePrice: 28000, currentPrice: 67000, purchaseDate: '2023-03-10', notes: '' },
  { id: '3', name: 'Vanguard S&P 500 ETF', type: 'ETF', ticker: 'VOO', quantity: 20, purchasePrice: 380, currentPrice: 450, purchaseDate: '2022-11-01', notes: '' },
  { id: '4', name: 'Ethereum', type: 'Crypto', ticker: 'ETH', quantity: 3, purchasePrice: 1600, currentPrice: 3500, purchaseDate: '2023-06-20', notes: '' },
  { id: '5', name: 'Cash Savings', type: 'Cash', ticker: '', quantity: 1, purchasePrice: 5000, currentPrice: 5000, purchaseDate: '2024-01-01', notes: 'Emergency fund' },
];

export const sampleGoals = [
  { id: '1', name: 'First $100K', targetAmount: 100000, targetDate: '2025-12-31', linkedToPortfolio: true, currentAmount: 0, notes: 'The hardest and most important milestone' },
  { id: '2', name: 'Financial Freedom Fund', targetAmount: 500000, targetDate: '2030-01-01', linkedToPortfolio: true, currentAmount: 0, notes: '' },
];
```

---

## 🧭 Navigation (Sidebar)

Sidebar items with Lucide icons:
- 🏠 Dashboard (`LayoutDashboard`)
- 💼 Portfolio (`Briefcase`)
- 🎯 Goals (`Target`)

Sidebar style:
- Fixed left, `w-64`, glassmorphism background
- App logo at top: stylized mountain peak `⛰️` + "ASCENT" in all-caps DM Serif Display
- Active nav item: gradient left border + subtle background glow
- Bottom of sidebar: tiny motivational phrase that rotates daily: "Every dollar is a soldier." / "Compound interest never sleeps." / "Your future self is watching."

---

## ✅ Final Quality Checklist

Make sure the app includes ALL of the following:

- [ ] All pages render without errors
- [ ] Adding an investment updates the dashboard net worth in real time
- [ ] Charts render with sample data on first load
- [ ] Goals show correct progress % linked to portfolio
- [ ] Quote carousel auto-rotates every 8 seconds
- [ ] Airplane icon on altitude bar moves proportionally
- [ ] Dark/light mode toggle works and persists
- [ ] All data persists on page refresh via LocalStorage
- [ ] Fully responsive: mobile (single column), tablet (2 col), desktop (full layout)
- [ ] No placeholder images — use SVG icons and emoji where visuals are needed
- [ ] Smooth animations on all major interactions (modal open/close, page transitions, number updates)
- [ ] App feels PREMIUM — not like a tutorial project. Every spacing, shadow, and color choice should feel intentional.

---

## 🚀 Final Instructions to Replit Agent

Build this app completely, file by file. Start with:
1. `vite.config.js` + `tailwind.config.js` + `index.css` (fonts, CSS variables, base styles)
2. Data hooks (`usePortfolio.js`, `useGoals.js`) and sample data
3. Shared UI components (`GlassCard`, `AnimatedNumber`, `Badge`)
4. Mountain background SVG component
5. Layout components (Sidebar, TopBar)
6. Dashboard page and all its sub-components
7. Portfolio page with modal
8. Goals page with modal
9. Wire everything together in `App.jsx` with React Router

Make every component production-grade. The app should look like it was built by a senior designer and developer at a top fintech company. **Do not cut corners on the visual design** — this is the most important requirement.

# PropIQ — EU Real Estate Investment Intelligence App

> **A decision-intelligence web app that transforms 5,000+ European property listings into a personalised investment strategy — no dashboard experience required.**

[![Made with HTML/CSS/JS](https://img.shields.io/badge/Built%20With-HTML%20%7C%20CSS%20%7C%20JavaScript-gold?style=flat-square)](#)
[![Dataset](https://img.shields.io/badge/Dataset-5%2C000%20EU%20Properties-blue?style=flat-square)](#dataset)
[![Cities](https://img.shields.io/badge/Cities-10%20Major%20EU%20Markets-green?style=flat-square)](#dataset)
[![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)](#license)

---

## Table of Contents

1. [The Problem I Was Solving](#the-problem-i-was-solving)
2. [The Solution — From Dashboard to Advisor](#the-solution)
3. [Live Demo](#live-demo)
4. [Features](#features)
5. [Dataset Overview](#dataset-overview)
6. [How the Scoring Engine Works](#how-the-scoring-engine-works)
7. [Project Structure](#project-structure)
8. [Data Analysis Code](#data-analysis-code)
9. [HTML App — Architecture & Key Code](#html-app--architecture--key-code)
10. [Power BI Version](#power-bi-version)
11. [Design System — Sovereign Ledger](#design-system--sovereign-ledger)
12. [Known Issues & Fixes Applied](#known-issues--fixes-applied)
13. [Roadmap](#roadmap)
14. [Getting Started](#getting-started)
15. [License](#license)

---

## The Problem I Was Solving

Most real estate data tools share the same flaw: **they give you data, but not decisions.**

You get a table of properties. You get a map. Maybe a chart. But you're left staring at 5,000 rows wondering:

- *Which city should I actually invest in?*
- *Is this property cheap or expensive relative to its market?*
- *How fast does this type of property actually sell?*
- *Does any of this match MY goal — rental income, flipping, or long-term growth?*

The conventional dashboard approach assumes the user already knows how to read the data, interpret the metrics, and draw their own conclusions. That's fine for analysts. It's useless for investors.

**The real problem isn't a lack of data. It's a lack of guided interpretation.**

I kept thinking about how a good private wealth advisor actually works. They don't hand you a spreadsheet. They ask you five questions — your goal, your budget, your risk appetite, your timeline — and then they tell you exactly what to do and why. The data is the background. The recommendation is the foreground.

That mental model is what I tried to build here.

### Why This Matters for EU Real Estate Specifically

European property markets are extraordinarily diverse within a relatively small geography. Warsaw properties average **€1,503/sqm**. Paris averages **€5,201/sqm**. The same €500,000 budget gets you a studio in Paris or a four-bedroom villa in Warsaw. Without context — without knowing which city you're in and what that city's average looks like — a price is just a number.

The goal was to build a tool that **contextualises every number** and translates it into a signal: *undervalued*, *fair*, or *overpriced* — relative to that specific city, not to Europe as a whole.

---

## The Solution

**PropIQ** is a single-file, zero-dependency web application that works like a personal investment advisor:

1. **Asks 6 guided questions** about your investment goal, budget, risk tolerance, horizon, location preference, and property type
2. **Runs a weighted composite scoring model** across all 10 cities, calibrated to your answers
3. **Surfaces a personalised narrative** — "here's your top city, here's why, here's what to buy"
4. **Backs it with evidence** — interactive map, property table filtered to your budget, comparative charts
5. **Lets you run scenarios** — change any input and watch the rankings update instantly

The result feels like a conversation with a data-driven advisor, not a session with a BI tool.

---

## Live Demo

Download `PropIQ_Real_Estate_Advisor.html` and open it directly in any browser. No server, no install, no API key. The entire dataset (5,000 properties) is embedded in the file.

```bash
# Just open the file
open PropIQ_Real_Estate_Advisor.html
# or double-click it in your file explorer
```

---

## Features

| Feature | Description |
|---|---|
| 🎯 **Guided Questionnaire** | 6-step wizard capturing goal, budget, risk, horizon, location, and property type |
| 🧠 **Investment Scoring Engine** | Composite score weighted by goal: undervaluation, demand, liquidity, and growth |
| 📍 **Interactive Europe Map** | Leaflet.js map with city circles sized by score, colour-coded by rank |
| 📋 **Filtered Property Table** | Real listings from the dataset, filtered to your budget and ranked by score |
| 📊 **Evidence Charts** | Side-by-side bar charts: price/sqm, days on market, growth signals, final scores |
| 🔁 **Scenario Planner** | Live re-ranking as you adjust goal, risk, horizon, and location preference |
| 💡 **Advisor Narrative** | Dynamic text card summarising your top city with score, growth, and match count |
| 🚨 **Risk Flags** | Highlights markets with slow sales cycles or weak growth signals |
| 🎨 **Sovereign Ledger Design** | Dark luxury aesthetic: Deep Onyx, Warm Bone, Rich Gold — no borders, glass morphism |

---

## Dataset Overview

The dataset covers **5,000 European property listings** across 10 major cities.

| Field | Type | Description |
|---|---|---|
| `property_id` | string | Unique identifier (PROP-XXXXX) |
| `listing_date` | date | When the property was listed |
| `property_type` | string | Apartment, Villa, Townhouse, Office, etc. |
| `listing_type` | string | Sale or Rental |
| `city` | string | One of 10 EU cities |
| `country` | string | Country of the city |
| `bedrooms` | int | Number of bedrooms |
| `bathrooms` | float | Number of bathrooms |
| `square_meters` | float | Total floor area |
| `year_built` | int | Construction year |
| `sale_price_eur` | float | Asking price in euros (Sale listings) |
| `monthly_rent_eur` | float | Monthly rent in euros (Rental listings) |
| `price_per_sqm` | float | Price divided by area |
| `days_on_market` | float | How long the listing has been active |
| `latitude` / `longitude` | float | Geolocation coordinates |
| `last_sold_price_eur` | float | Previous transaction price |
| `parking_spots` | int | Number of parking spaces |
| `gym` / `swimming_pool` / `elevator` | string | Amenity flags (Yes/No) |
| `furnishing_status` | string | Furnished, Semi-Furnished, Unfurnished |
| `energy_rating` | string | EU energy efficiency label (A–G) |
| `floor_number` | float | Floor level |

### City Summary (from analysis)

| City | Country | Avg €/sqm | Avg Days on Market | Listings | Avg Growth |
|---|---|---|---|---|---|
| Paris | France | €5,201 | 172 | 730 | +97% |
| Amsterdam | Netherlands | €4,754 | 183 | 592 | +99% |
| Berlin | Germany | €3,233 | 164 | 641 | +75% |
| Brussels | Belgium | €2,784 | 172 | 305 | +117% |
| Vienna | Austria | €2,774 | 170 | 532 | +93% |
| Rome | Italy | €2,760 | 173 | 536 | +82% |
| Prague | Czech Republic | €2,181 | 162 | 335 | +80% |
| Madrid | Spain | €2,171 | 175 | 551 | +96% |
| Lisbon | Portugal | €1,881 | 171 | 409 | +78% |
| Warsaw | Poland | €1,503 | 171 | 369 | +71% |

---

## How the Scoring Engine Works

The scoring engine runs entirely in JavaScript in the browser. It evaluates every city against four metrics, then combines them with weights that shift depending on the user's stated goal.

### The Four Component Scores

```
Undervaluation Score  =  max(0,  (global_avg_ppsqm - city_avg_ppsqm) / global_avg_ppsqm  × 100)
Demand Score          =  max(0,  (global_avg_dom - city_avg_dom) / global_avg_dom  × 100  +  50)
Growth Score          =  min(100, city_avg_growth × 50)
Liquidity Score       =  max(0,  100 - (city_avg_dom / 365 × 100))
```

Where:
- `global_avg_ppsqm` = mean price per sqm across all 10 cities (≈ €2,903)
- `global_avg_dom` = mean days on market across all 10 cities (≈ 172 days)
- `city_avg_growth` = mean of `(sale_price - last_sold_price) / last_sold_price` per city

### Goal-Based Weighting

| Goal | Undervaluation | Demand | Growth | Liquidity |
|---|---|---|---|---|
| **Flip** | 40% | 10% | 10% | 40% |
| **Rental Income** | 20% | 40% | 20% | 20% |
| **Long-Term Appreciation** | 20% | 10% | 50% | 20% |
| **Default** | 30% | 30% | 20% | 20% |

### Risk & Location Modifiers

After the base weighted score is calculated, multipliers are applied:

```javascript
// Risk modifiers
if (risk === 'low'  && city IN ['Paris','Amsterdam','Vienna'])  score *= 1.12
if (risk === 'high' && city IN ['Warsaw','Prague','Brussels'])  score *= 1.12
if (risk === 'low'  && city IN ['Warsaw','Prague','Brussels'])  score *= 0.85

// Horizon modifiers
if (horizon === 'short') score += (50 - days_on_market) * 0.2
if (horizon === 'long')  score += avg_growth * 5

// Final clamp
score = min(100, max(0, score))
```

### vs City Average (the table column)

For each individual property in the filtered table:

```javascript
vsAvg = (property.price_per_sqm - cityAverage.avg_ppsqm) / cityAverage.avg_ppsqm
```

- **Negative (green)** → property is cheaper than its city's average. Potential undervaluation.
- **Near zero (yellow)** → fairly priced relative to the local market.
- **Positive (red)** → property commands a premium above the city average.

---

## Project Structure

```
propiq/
├── PropIQ_Real_Estate_Advisor.html   # Self-contained app (dataset embedded)
├── EU_Real_Estate_Dataset.xlsx       # Source data (5,000 listings)
├── analysis/
│   └── analyse.py                    # Data exploration & JSON export script
└── README.md
```

> **Note:** The HTML file is fully self-contained. The dataset is embedded directly as a JavaScript constant inside the file. No external files, no server, no build step required.

---

## Data Analysis Code

This script was used to explore the dataset, compute city-level benchmarks, engineer the `growth` feature, and export a clean JSON file for embedding in the app.

```python
import pandas as pd
import json
import math

# ── 1. LOAD & INSPECT ──────────────────────────────────────────────────────
df = pd.read_excel('EU_Real_Estate_Dataset.xlsx')

print('Shape:', df.shape)
print('Columns:', list(df.columns))
print('\nCountries:', df['country'].unique())
print('Cities:', df['city'].unique())
print('Property types:', df['property_type'].unique())
print('Listing types:', df['listing_type'].unique())

print('\nNumeric stats:')
print(df[['sale_price_eur', 'monthly_rent_eur',
          'price_per_sqm', 'days_on_market', 'square_meters']].describe())


# ── 2. FEATURE ENGINEERING ──────────────────────────────────────────────────
# Price growth since last sale
df['growth'] = (
    (df['sale_price_eur'] - df['last_sold_price_eur'])
    / df['last_sold_price_eur']
).round(4)


# ── 3. CITY-LEVEL AGGREGATION ───────────────────────────────────────────────
city_stats = df.groupby('city').agg(
    avg_price_sqm = ('price_per_sqm',  'mean'),
    avg_days      = ('days_on_market', 'mean'),
    count         = ('property_id',    'count'),
    avg_price     = ('sale_price_eur', 'mean'),
    country       = ('country',        'first'),
    lat           = ('latitude',       'mean'),
    lon           = ('longitude',      'mean'),
).round(2).reset_index()

print(city_stats.to_string())


# ── 4. GROWTH BY CITY ───────────────────────────────────────────────────────
df_sale = df[df['listing_type'] == 'Sale'].copy()
growth_by_city = df_sale.groupby('city')['growth'].mean().round(3)
print('\nGrowth by city:')
print(growth_by_city)


# ── 5. DEMAND (DAYS ON MARKET) BY PROPERTY TYPE ─────────────────────────────
type_demand = df.groupby('property_type')['days_on_market'].mean().round(1)
print('\nDays on market by type:')
print(type_demand)


# ── 6. PRICE DISTRIBUTION (for budget slider defaults) ──────────────────────
sale_prices = df[df['listing_type'] == 'Sale']['sale_price_eur'].dropna()
prices_sorted = sorted(sale_prices)
n = len(prices_sorted)

print('\nSale price distribution:')
print(f"  Min:  €{prices_sorted[0]:,.0f}")
print(f"  p10:  €{prices_sorted[int(n*0.1)]:,.0f}")
print(f"  p25:  €{prices_sorted[int(n*0.25)]:,.0f}")
print(f"  p50:  €{prices_sorted[int(n*0.5)]:,.0f}")
print(f"  p75:  €{prices_sorted[int(n*0.75)]:,.0f}")
print(f"  p90:  €{prices_sorted[int(n*0.9)]:,.0f}")
print(f"  Max:  €{prices_sorted[-1]:,.0f}")
print(f"  Total sale listings: {n}")


# ── 7. EXPORT TO CLEAN JSON ──────────────────────────────────────────────────
cols = [
    'property_id', 'property_type', 'listing_type', 'city', 'country',
    'bedrooms', 'bathrooms', 'square_meters', 'sale_price_eur',
    'monthly_rent_eur', 'price_per_sqm', 'days_on_market',
    'latitude', 'longitude', 'last_sold_price_eur', 'parking_spots',
    'gym', 'swimming_pool', 'elevator', 'furnishing_status',
    'energy_rating', 'growth'
]

df_export = df[cols].copy().where(pd.notna(df[cols]), other=None)
records = df_export.to_dict(orient='records')

# Replace any residual float NaN / Inf — these are illegal in JSON
# and will cause JSON.parse() to throw silently in the browser
def clean_value(val):
    if val is None:
        return None
    if isinstance(val, float) and (math.isnan(val) or math.isinf(val)):
        return None
    return val

records = [{k: clean_value(v) for k, v in row.items()} for row in records]

# Verify before saving — browser JSON.parse rejects bare NaN
raw = json.dumps(records, separators=(',', ':'))
assert 'NaN' not in raw and 'Infinity' not in raw, "Invalid JSON values found!"

with open('data.json', 'w') as f:
    f.write(raw)

print(f"\nExported {len(records):,} records to data.json ({len(raw):,} bytes)")
```

### Output from Analysis

```
Shape: (5000, 25)

Sale price distribution:
  Min:   €50,000
  p10:   €221,132
  p25:   €367,347
  p50:   €646,363
  p75:   €1,229,698
  p90:   €2,236,793
  Max:   €13,287,305
  Total sale listings: 2,955

Days on market by property type:
  Villa        164.4
  Townhouse    169.0
  Office       169.8
  Mixed-Use    172.6
  Warehouse    172.0
  Apartment    173.7
  Retail       177.8
```

---

## HTML App — Architecture & Key Code

The app is a single HTML file with three logical screens managed entirely in vanilla JavaScript. No frameworks, no build tools, no dependencies beyond Leaflet.js for the map.

### Screen Architecture

```javascript
// Three screens, one active at a time
function showScreen(id) {
  document.querySelectorAll('.screen')
    .forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

// Flow: Landing → Quiz → Results
goToLanding()  →  showScreen('screen-landing')
startQuiz()    →  showScreen('screen-quiz')
buildResults() →  showScreen('screen-results')
```

### Quiz Step Renderer

Each of the 6 steps is defined as a configuration object. The renderer reads the config and builds the HTML dynamically, keeping the logic completely separate from the presentation:

```javascript
const STEPS = [
  {
    id: 'goal',
    title: 'What is your investment goal?',
    sub: 'This shapes everything — from which cities to target to what property type to buy.',
    type: 'choice',
    options: [
      { val:'flip',         icon:'🔄', title:'Quick Profit (Flip)',   desc:'Buy undervalued, sell fast' },
      { val:'rental',       icon:'🏠', title:'Rental Income',         desc:'Steady monthly cash flow'   },
      { val:'appreciation', icon:'📈', title:'Long-Term Growth',      desc:'Hold for appreciation'      }
    ],
    cols: 3
  },
  // ... 5 more steps
];

function renderStep() {
  const step = STEPS[currentStep];
  // progress bar, question title, option grid or budget sliders
  // nav buttons with disabled state until selection made
}
```

### Composite Scoring Engine

The heart of the app. Runs in the browser on every answer change:

```javascript
function scoreCity(city) {
  const { goal, location, risk, horizon } = answers;

  // Component scores (0–100 each)
  const undervalScore = Math.max(0,
    (globalAvgPpsqm - city.avg_ppsqm) / globalAvgPpsqm * 100
  );
  const demandScore = Math.max(0,
    (globalAvgDom - city.avg_dom) / globalAvgDom * 100 + 50
  );
  const growthScore   = Math.min(100, city.avg_growth * 50);
  const liquidScore   = Math.max(0, 100 - (city.avg_dom / 365 * 100));

  // Goal-based weights
  const weights = {
    flip:          { underval:0.4, demand:0.1, growth:0.1, liquid:0.4 },
    rental:        { underval:0.2, demand:0.4, growth:0.2, liquid:0.2 },
    appreciation:  { underval:0.2, demand:0.1, growth:0.5, liquid:0.2 },
    default:       { underval:0.3, demand:0.3, growth:0.2, liquid:0.2 },
  };
  const w = weights[goal] || weights.default;

  let base = undervalScore * w.underval
           + demandScore   * w.demand
           + growthScore   * w.growth
           + liquidScore   * w.liquid;

  // Risk multipliers
  const majorCities    = ['Paris','Amsterdam','Berlin','Vienna','Rome'];
  const emergingCities = ['Warsaw','Lisbon','Prague','Brussels','Madrid'];

  if (risk === 'low'  && majorCities.includes(city.city))    base *= 1.12;
  if (risk === 'high' && emergingCities.includes(city.city)) base *= 1.12;
  if (risk === 'low'  && emergingCities.includes(city.city)) base *= 0.85;

  // Location preference multipliers
  if (location === 'major'    && majorCities.includes(city.city))    base *= 1.15;
  if (location === 'emerging' && emergingCities.includes(city.city)) base *= 1.15;
  if (location === 'major'    && emergingCities.includes(city.city)) base *= 0.80;
  if (location === 'emerging' && majorCities.includes(city.city))    base *= 0.80;

  // Horizon adjustments
  if (horizon === 'short') base += (50 - city.avg_dom) * 0.2;
  if (horizon === 'long')  base += city.avg_growth * 5;

  return Math.min(100, Math.max(0, base));
}
```

### Property Table Filtering

Properties are filtered inline against the user's budget, location, and property type answers. The key lesson here: **all filtering must use column-level comparisons with variables, not nested measure calls** (relevant for both the JS and the Power BI DAX port):

```javascript
function renderPropertiesTable(top3) {
  const topCities = top3.map(c => c.city);
  const cityAvgMap = {};
  CITY_DATA.forEach(c => { cityAvgMap[c.city] = c.avg_ppsqm; });

  let filtered = allProperties.filter(p =>
    topCities.includes(p.city)
    && p.sale_price_eur >= answers.budgetMin
    && p.sale_price_eur <= answers.budgetMax
    && p.listing_type === 'Sale'
  );

  if (answers.propType !== 'any') {
    filtered = filtered.filter(p => p.property_type === answers.propType);
  }

  // Score proxy — sort by undervaluation + speed
  filtered.sort((a, b) => {
    const score = p => {
      const cityAvg = cityAvgMap[p.city] || 2500;
      return (cityAvg - p.price_per_sqm) / cityAvg * 50
           + (365 - p.days_on_market) * 0.1;
    };
    return score(b) - score(a);
  });

  // Render top 50 with conditional formatting
  const show = filtered.slice(0, 50);
  // ... table HTML generation
}
```

### Data Embedding Strategy

Instead of fetching an external `data.json` file (which fails on `file://` protocol), the dataset is embedded directly as a JavaScript constant. The Python script generates it, the HTML references it:

```python
# Python — generate the embedded data constant
raw = json.dumps(records, separators=(',', ':'))
# Inject into HTML
html = html.replace(
    '<script>',
    f'<script>\nconst EMBEDDED_DATA = {raw};\n',
    1  # only the first <script> tag
)
```

```javascript
// JavaScript — use it directly, no fetch needed
async function loadAndRenderProperties(top3) {
  if (allProperties.length === 0) {
    allProperties = EMBEDDED_DATA;
  }
  renderPropertiesTable(top3);
}
```

---

## Power BI Version

The full analytical logic has also been ported to Power BI using DAX measures and disconnected parameter tables. See the companion guide in this repository for the complete implementation including:

- M Query for data transformation and `price_growth_pct` feature engineering
- `CityAverages` reference table built from grouped aggregations
- What-If Parameters for `Budget Min` and `Budget Max` sliders
- DAX scoring measures that mirror the JavaScript engine exactly
- Disconnected answer tables (`GoalOptions`, `RiskOptions`, etc.) bridged to the `data` table through DAX context rather than relationships
- HTML Content visual with a DAX-generated rich HTML narrative card
- Chiclet Slicer configuration for the questionnaire UI

### Key DAX — Composite Investment Score

```dax
Investment Score =
VAR wUnderval  = [W Undervaluation]
VAR wDemand    = 0.3
VAR wGrowth    = [W Growth]
VAR wLiquidity = [W Liquidity]

VAR RawScore =
    [Undervaluation Score] * wUnderval +
    [Demand Score]         * wDemand  +
    [Growth Score]         * wGrowth  +
    [Liquidity Score]      * wLiquidity

VAR TotalWeight = wUnderval + wDemand + wGrowth + wLiquidity

RETURN DIVIDE(RawScore, TotalWeight)
```

### Key DAX — Qualifying Properties Count

```dax
Qualifying Properties Count =
VAR minB = [Budget Min]
VAR maxB = [Budget Max]
VAR selectedType     = [Selected PropType]
VAR selectedLocation = [Selected Location]
VAR majorCities      = {"Paris","Amsterdam","Berlin","Vienna","Rome"}
VAR emergingCities   = {"Warsaw","Lisbon","Prague","Brussels","Madrid"}

RETURN
COUNTROWS(
    FILTER(
        'data',
        'data'[listing_type] = "Sale"
        && 'data'[sale_price_eur] >= minB
        && 'data'[sale_price_eur] <= maxB
        && (
            selectedType = "Any"
            || 'data'[property_type] = selectedType
        )
        && (
            selectedLocation = "any"
            || ( selectedLocation = "major"    && 'data'[city] IN majorCities )
            || ( selectedLocation = "emerging" && 'data'[city] IN emergingCities )
        )
    )
)
```

> **Important:** Never nest measures that use `SELECTEDVALUE()` inside a `FILTER()` call on a table. Always inline the logic using column references and VAR declarations as shown above.

---

## Design System — Sovereign Ledger

The visual design follows a private wealth aesthetic called **Sovereign Ledger**. The guiding principle is that high-end interfaces are defined by *restraint and depth*, not decoration.

### Colour Palette

| Token | Hex | Usage |
|---|---|---|
| `--onyx` | `#0d0d0f` | Deepest layer: header, left panel |
| `--onyx-2` | `#141418` | Base canvas: right panel background |
| `--onyx-3` | `#1c1c22` | Raised cards, table wrappers |
| `--onyx-4` | `#242430` | Input fields, deepest inset surfaces |
| `--bone` | `#f2ede6` | Primary text on dark |
| `--bone-2` | `#e8e0d4` | Secondary text |
| `--gold` | `#c9a84c` | Primary accent, score highlights |
| `--gold-warm` | `#e2b95a` | Gradient end for gold elements |
| `--sage` | `#3d6b5e` | Secondary positive signal |
| `--ruby` | `#8b2e2e` | Caution / negative signals |
| `--smoke` | `#8a8a9a` | Labels, metadata, secondary info |

### Typography

| Role | Font | Weight |
|---|---|---|
| Display / Headlines | Cormorant Garamond (serif) | 300–600 |
| Italic brand moments | Cormorant Garamond Italic | 300 |
| Body / UI | Outfit (sans-serif) | 300–600 |

### The No-Line Rule

> *Boundaries must be defined solely through background colour shifts. The transition of tone is the divider.*

No `1px solid` borders are used anywhere for layout or section separation. The four-step onyx depth system (`--onyx` → `--onyx-4`) creates visual hierarchy entirely through surface contrast.

### Glass & Gradient

Floating elements use glassmorphism:

```css
.glass-element {
  background: rgba(255, 255, 255, 0.04);
  backdrop-filter: blur(16px);
  /* No border — glass surface is self-defining */
}
```

Gold elements always use a warm gradient rather than flat colour:

```css
background: linear-gradient(135deg, var(--gold) 0%, var(--gold-warm) 100%);
```

---

## Known Issues & Fixes Applied

### 1. `NaN` in exported JSON crashes browser silently

**Problem:** Python's `pandas` exports missing float values as `NaN`. This is valid Python but **illegal JSON**. The browser's `JSON.parse()` throws on the first `NaN` and silently returns `undefined`, leaving `allProperties` empty and every filter returning zero results.

**Fix:** After converting the DataFrame to a list of dicts, pass all values through a cleaner function before serialising:

```python
def clean_value(val):
    if val is None:
        return None
    if isinstance(val, float) and (math.isnan(val) or math.isinf(val)):
        return None
    return val

records = [{k: clean_value(v) for k, v in row.items()} for row in records]

# Assert before saving
raw = json.dumps(records, separators=(',', ':'))
assert 'NaN' not in raw, "Invalid JSON — browser will reject this"
```

### 2. `fetch('data.json')` fails on `file://` protocol

**Problem:** Browsers block all `fetch()` requests when a page is opened directly from the filesystem (`file://` URLs). An external `data.json` file will always fail with a CORS or network error.

**Fix:** Embed the dataset directly as a `const` inside the `<script>` block at build time. The HTML file becomes fully self-contained.

### 3. Power BI — `goal` is a reserved word in DAX

**Problem:** Naming a VAR `goal` inside a DAX measure throws a syntax error because `GOAL` is a reserved keyword.

**Fix:** Prefix all potentially reserved VAR names with an underscore:

```dax
VAR _goal    = [Selected Goal]
VAR _risk    = [Selected Risk]
VAR _horizon = [Selected Horizon]
```

### 4. Power BI — measures with `SELECTEDVALUE()` cannot be nested inside `FILTER()`

**Problem:** Calling a measure like `[In Budget]` (which internally uses `SELECTEDVALUE`) inside `COUNTROWS(FILTER('data', [In Budget] = 1))` throws a context error.

**Fix:** Inline all filter logic directly with column references and VARs inside the outer measure. Never call context-dependent measures from within `FILTER()`.

---

## Roadmap

- [ ] Add mortgage calculator tab (monthly payment at user-defined LTV and rate)
- [ ] Integrate real-time listing data via property API
- [ ] Add neighbourhood-level scoring (not just city-level)
- [ ] Export personalised PDF investment brief
- [ ] Add rental yield calculator for dual-use properties
- [ ] Multi-currency support (GBP, USD, PLN display)
- [ ] Add historical price trend chart per city using time-series data

---

## Getting Started

### Requirements

- Any modern browser (Chrome, Firefox, Safari, Edge)
- Python 3.8+ and `pandas` (only if re-running the analysis)

### Run the App

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/propiq.git
cd propiq

# Open the app — no server needed
open PropIQ_Real_Estate_Advisor.html
```

### Re-run the Analysis (Optional)

If you want to regenerate the embedded dataset from the source Excel file:

```bash
pip install pandas openpyxl
python analysis/analyse.py
```

Then embed the output `data.json` back into the HTML:

```python
with open('PropIQ_Real_Estate_Advisor.html', 'r') as f:
    html = f.read()

with open('data.json', 'r') as f:
    data = f.read()

html = html.replace(
    'const EMBEDDED_DATA = [];',
    f'const EMBEDDED_DATA = {data};'
)

with open('PropIQ_Real_Estate_Advisor.html', 'w') as f:
    f.write(html)
```

---

## License

MIT License — free to use, modify, and distribute. Attribution appreciated.

---

*Built with curiosity, pandas, and a strong opinion that data tools should feel like advisors, not spreadsheets.*

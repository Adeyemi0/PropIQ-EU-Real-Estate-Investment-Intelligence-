# PropIQ — The EU Real Estate Investment Advisor

[![Cities Covered](https://img.shields.io/badge/Cities-10%20Major%20EU%20Markets-gold?style=flat-square)](#the-10-markets)
[![Properties Analysed](https://img.shields.io/badge/Properties%20Analysed-5%2C000%2B-blue?style=flat-square)](#dataset)
[![No Login Required](https://img.shields.io/badge/No%20Login-Open%20In%20Browser-green?style=flat-square)](#getting-started)

---

## Table of Contents

1. [The Investor Problem I Was Solving](#the-investor-problem-i-was-solving)
2. [The Insight That Changed the Approach](#the-insight-that-changed-the-approach)
3. [What PropIQ Actually Does](#what-propiq-actually-does)
4. [The 10 Markets Covered](#the-10-markets-covered)
5. [How Your Answers Drive the Intelligence](#how-your-answers-drive-the-intelligence)
6. [Understanding the Scores & Signals](#understanding-the-scores--signals)
7. [What the Data Reveals About European Markets](#what-the-data-reveals-about-european-markets)
8. [The Scoring Engine — For the Curious](#the-scoring-engine--for-the-curious)
9. [Data Analysis Code](#data-analysis-code)
10. [Building the App](#building-the-app)
11. [The Design Philosophy](#the-design-philosophy)
12. [Known Issues & Fixes](#known-issues--fixes)
13. [Getting Started](#getting-started)
14. [What's Next](#whats-next)
15. [License](#license)

---

## The Investor Problem I Was Solving

Every serious investor I know has experienced the same frustration.

You're looking at European real estate. You open a property portal. You get 5,000 listings. Some are in Paris at €8,000/sqm. Some are in Warsaw at €1,200/sqm. There are villas, apartments, offices, townhouses. There are properties that have been sitting on the market for 300 days and properties that sold in 12. There is no shortage of data.

And yet — you still don't know what to do.

**Because the problem was never a lack of data. The problem is that raw data does not know your situation.**

It doesn't know that you have €500,000 to deploy and you need it working within 18 months. It doesn't know that you're comfortable with emerging market risk in exchange for upside. It doesn't know whether you want rental cash flow or capital appreciation. It doesn't know that you prefer apartments over villas because they're more liquid.

So you end up doing what most investors do: you spend hours filtering, comparing, and second-guessing yourself — and you still leave with a shortlist, not a conviction.

I built PropIQ to solve exactly that.

---

## The Insight That Changed the Approach

The turning point was realising that **most real estate tools are built for analysts, not investors.**

A dashboard gives you a chart of average prices by city. Fine. But that chart doesn't tell you whether *this specific property* in *this specific city* is cheap or expensive relative to its local market. It doesn't tell you whether that city fits your investment thesis. It doesn't rank anything. It just shows you data and leaves the decision to you.

I thought about how a genuinely good private wealth advisor operates. When a client comes in, they don't get a spreadsheet. They get a conversation. The advisor asks the right questions — *what's your goal, what's your timeline, how much risk can you stomach* — and then they deliver a recommendation. Not a report. A recommendation.

**That became the design brief: build an advisor, not a dashboard.**

The app had to earn the right to show data by first understanding the person looking at it. Every metric, every ranking, every highlighted property had to be filtered through the lens of that individual investor's profile. The same city that is a bad idea for a short-term flipper might be the best possible entry for a long-term appreciation play. The tool had to know the difference.

The second insight was about **how investors actually think about price**. An investor doesn't care that a property costs €3,500/sqm in isolation. They care whether €3,500/sqm is cheap or expensive for that city. Warsaw at €3,500/sqm would be a premium property. Paris at €3,500/sqm would be a bargain. Context is everything. So every price signal in PropIQ is shown relative to the local city average — not against a European average that flattens all nuance.

---

## What PropIQ Actually Does

PropIQ is built around a single user journey: **six questions in, a complete investment brief out.**

### Step 1 — It Asks Before It Tells

Before showing you a single property, PropIQ captures your investment profile:

- **Goal** — Are you flipping for quick profit, building rental income, or holding for long-term appreciation? This one answer shifts the entire scoring model.
- **Budget** — Your minimum and maximum spend. Every property shown will fit this range.
- **Location preference** — Major established capitals, undervalued emerging markets, or no preference.
- **Risk tolerance** — Conservative markets with proven liquidity, or emerging markets with higher upside potential.
- **Investment horizon** — 0–1 year, 1–3 years, or 3+ years. Short-horizon investors need fast-moving markets. Long-horizon investors can absorb slower cycles.
- **Property type** — Apartments, villas, or open to anything the data recommends.

### Step 2 — The Engine Scores Everything

Behind the scenes, PropIQ runs a weighted composite scoring model across all 10 cities using four investment signals: undervaluation relative to the EU average, demand velocity (how fast properties move), price growth since last sale, and market liquidity. The weights on those four signals shift based on your goal.

A flipper needs undervaluation and liquidity. A rental investor needs demand. An appreciation investor needs growth. The same city scores differently for each profile — which is exactly how a real investment decision should work.

### Step 3 — You Get a Brief, Not a Report

The output is not a table of numbers. It is a structured investment brief:

- Your **top 3 city recommendations**, ranked and explained in plain language
- A **narrative summary** — why each city fits your specific profile
- A **recommended property type** — based on what sells fastest and yields best in your target market
- A **filtered property table** — real listings from the dataset, sorted by investment score, showing only properties within your budget
- **Risk flags** — markets you should avoid given your profile, and why
- **Supporting evidence** — comparative charts showing price per sqm, days on market, and growth signals across all 10 cities

### Step 4 — You Can Challenge the Recommendation

The Scenario Planner lets you stress-test the output. Change your goal from rental to flip. Switch your risk tolerance from low to high. Move your horizon from long to short. The city rankings update instantly, showing you exactly how sensitive the recommendation is to your assumptions. This is how real investment analysis works — not a single answer, but a decision under different scenarios.

---

## The 10 Markets Covered

PropIQ analyses the following EU cities, representing a spectrum from mature premium markets to undervalued emerging capitals:

| City | Country | Market Type | Avg €/sqm | Avg Days Listed |
|---|---|---|---|---|
| Paris | France | Premium / Established | €5,201 | 172 days |
| Amsterdam | Netherlands | Premium / Established | €4,754 | 183 days |
| Berlin | Germany | Premium / Growing | €3,233 | 164 days |
| Brussels | Belgium | Mid-Market / High Growth | €2,784 | 172 days |
| Vienna | Austria | Mid-Market / Stable | €2,774 | 170 days |
| Rome | Italy | Mid-Market / Recovering | €2,760 | 173 days |
| Prague | Czech Republic | Emerging / Appreciating | €2,181 | 162 days |
| Madrid | Spain | Emerging / Liquid | €2,171 | 175 days |
| Lisbon | Portugal | Emerging / High Demand | €1,881 | 171 days |
| Warsaw | Poland | Undervalued / High Potential | €1,503 | 171 days |

The spread between the cheapest and most expensive market is **3.5x**. That gap is where investment opportunities live.

---

## How Your Answers Drive the Intelligence

This is the core of what makes PropIQ different from a filtered property search. Your answers don't just filter the data — they **reweight the entire scoring model**.

### If Your Goal Is Flipping for Quick Profit

The model prioritises **undervaluation** (40%) and **liquidity** (40%). The question it answers is: *where can I buy below market and exit quickly?* Cities with fast days-on-market and low price-per-sqm relative to the EU average rise to the top. A slow, overpriced market — even a prestigious one — drops down the ranking regardless of its prestige.

### If Your Goal Is Rental Income

The model shifts weight toward **demand** (40%). The question becomes: *where are properties absorbed fastest, signalling strong tenant demand?* Cities where listings move quickly indicate a landlord's market with reliable occupancy. Undervaluation still matters for entry cost, but the velocity of the market is the primary signal.

### If Your Goal Is Long-Term Appreciation

The model heavily weights **growth** (50%) — the historical price appreciation from last sold price to current listing price. The question becomes: *where has capital grown fastest, and where is that momentum likely to continue?* A city that has already doubled prices is telling you something about demand fundamentals that no chart of current listings can show you.

### Risk Tolerance Refinement

On top of the goal-based weights, risk tolerance applies city-specific multipliers:

- **Low risk** investors get bonus scores for Paris, Amsterdam, and Vienna — deep, liquid markets with institutional buyer depth that protects values in downturns
- **High risk** investors get bonus scores for Warsaw, Prague, and Brussels — markets where the price-to-income gap still offers asymmetric upside
- **Low risk** investors see emerging markets scored down, because the data shows they have higher days-on-market variance and thinner buyer pools

### Horizon Calibration

Short-horizon investors (0–1 year) get a velocity premium — cities where properties move faster score higher, because you need an exit, not just an entry. Long-horizon investors get a growth premium, because compounding appreciation over years outweighs short-term friction.

---

## Understanding the Scores & Signals

### The Investment Score (0–100)

This is the composite score for each city given your specific profile. It is not a universal ranking — Brussels scores higher than Paris for a high-risk appreciation investor but lower for a low-risk rental investor. The score is personal to you.

### vs City Average (the table column)

This is the most actionable signal in the property table. It answers the question: *is this specific property cheap or expensive for its local market?*

```
vs City Avg = (property price/sqm − city average price/sqm) / city average price/sqm
```

| Colour | Signal | What It Means |
|---|---|---|
| 🟢 Green (negative %) | Below city average | Potential undervaluation — entry advantage |
| 🟡 Yellow (near 0%) | Fairly priced | At market — justified if other signals are strong |
| 🔴 Red (positive %) | Above city average | Premium priced — needs justification from amenities or location |

A property that is 20% below the city average in Warsaw represents a fundamentally different opportunity than one that is 20% below average in Paris — but both are signals worth investigating.

### Days on Market

Low days on market means the market is absorbing supply quickly. It signals real demand, not just listing activity. For flippers, it means your exit window is shorter. For rental investors, it means tenants are competing for units. For appreciation investors, it means the demand foundation is real.

### Growth Signal

This is the percentage change from last sold price to current asking price across the dataset. It is a proxy for capital appreciation — what the market is pricing in based on real transaction history in that city.

---

## What the Data Reveals About European Markets

Running this analysis surfaced several patterns that directly inform the PropIQ scoring logic:

**Brussels is the hidden opportunity city.** It has the highest average growth signal in the dataset (+117%) while sitting in the mid-market price band. It is neither as expensive as Paris nor as distant as Warsaw — a combination that makes it interesting for multiple investor profiles.

**Berlin moves fastest.** Despite premium pricing, Berlin has the lowest average days on market (164 days) of all 10 cities. Properties there are absorbed quickly, which matters enormously for exit-focused investors.

**The premium cities are not necessarily the best investments.** Paris and Amsterdam are the most expensive by a significant margin, but their growth signals are not proportionally higher. An investor chasing appreciation gets more from Brussels or Madrid at a fraction of the entry cost.

**Warsaw has the most room to run.** At €1,503/sqm it is the most undervalued city in the dataset relative to the EU average. For an investor with a long horizon and high risk tolerance, the price gap to the EU average represents structural upside — if that convergence thesis plays out.

**Villa vs Apartment dynamics are clear in the data.** Villas average 164 days on market. Apartments average 174 days. That 10-day difference sounds small, but in a fast-moving market it is the difference between a clean exit and a price negotiation. For liquidity-sensitive investors, apartments win.

---

## The Scoring Engine — For the Curious

The full mathematical model behind PropIQ's city rankings:

### Four Component Scores

```
Undervaluation  =  max(0,  (EU_avg_ppsqm − city_avg_ppsqm) / EU_avg_ppsqm  × 100)
Demand          =  max(0,  (EU_avg_dom − city_avg_dom) / EU_avg_dom  × 100  +  50)
Growth          =  min(100, city_avg_growth × 50)
Liquidity       =  max(0,  100 − (city_avg_dom / 365 × 100))
```

### Goal-Based Weight Table

| Goal | Undervaluation | Demand | Growth | Liquidity |
|---|---|---|---|---|
| Flip | 40% | 10% | 10% | 40% |
| Rental | 20% | 40% | 20% | 20% |
| Appreciation | 20% | 10% | 50% | 20% |

### Risk & Location Multipliers Applied After Base Score

```
Low risk  + [Paris / Amsterdam / Vienna]   → score × 1.12
High risk + [Warsaw / Prague / Brussels]   → score × 1.12
Low risk  + [Warsaw / Prague / Brussels]   → score × 0.85

Major cities preference + major city       → score × 1.15
Emerging preference + emerging city        → score × 1.15

Short horizon bonus  →  score + (50 − city_avg_dom) × 0.2
Long horizon bonus   →  score + city_avg_growth × 5

Final score clamped to range [0, 100]
```

---

## Data Analysis Code

The Python analysis that built the city benchmarks and prepared the clean dataset:

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

print('\nKey numeric stats:')
print(df[['sale_price_eur', 'monthly_rent_eur',
          'price_per_sqm', 'days_on_market', 'square_meters']].describe())


# ── 2. FEATURE ENGINEERING ──────────────────────────────────────────────────
# Historical price growth: how much has each property appreciated
# since its last transaction? This is our appreciation signal.
df['growth'] = (
    (df['sale_price_eur'] - df['last_sold_price_eur'])
    / df['last_sold_price_eur']
).round(4)


# ── 3. CITY-LEVEL BENCHMARKS ────────────────────────────────────────────────
# These become the reference points for every individual property score.
# A property's value is meaningless without knowing what's normal in its city.
city_stats = df.groupby('city').agg(
    avg_price_sqm = ('price_per_sqm',  'mean'),
    avg_days      = ('days_on_market', 'mean'),
    count         = ('property_id',    'count'),
    avg_price     = ('sale_price_eur', 'mean'),
    country       = ('country',        'first'),
    lat           = ('latitude',       'mean'),
    lon           = ('longitude',      'mean'),
).round(2).reset_index()

print('\nCity benchmarks:')
print(city_stats.to_string())


# ── 4. GROWTH SIGNAL BY CITY ─────────────────────────────────────────────────
# Only look at Sale listings — rental records don't have meaningful sale price
# growth data and would distort the appreciation signal.
df_sale = df[df['listing_type'] == 'Sale'].copy()
growth_by_city = df_sale.groupby('city')['growth'].mean().round(3)

print('\nAverage price growth since last sale, by city:')
print(growth_by_city)


# ── 5. LIQUIDITY BY PROPERTY TYPE ────────────────────────────────────────────
# Days on market by property type reveals which asset classes
# are absorbed fastest — critical for exit-planning investors.
type_demand = df.groupby('property_type')['days_on_market'].mean().round(1)
print('\nAverage days on market by property type:')
print(type_demand)


# ── 6. BUDGET DISTRIBUTION ───────────────────────────────────────────────────
# Understanding the price distribution shapes the slider defaults.
# Setting defaults at p10–p90 ensures most users see real results
# without having to adjust anything.
sale_prices = df[df['listing_type'] == 'Sale']['sale_price_eur'].dropna()
prices_sorted = sorted(sale_prices)
n = len(prices_sorted)

print('\nSale price distribution:')
for label, pct in [('Min','0'),('p10','10'),('p25','25'),
                   ('p50','50'),('p75','75'),('p90','90'),('Max','100')]:
    idx = 0 if pct == '0' else (-1 if pct == '100' else int(n * int(pct) / 100))
    print(f"  {label}:  €{prices_sorted[idx]:,.0f}")
print(f"  Total sale listings: {n:,}")


# ── 7. EXPORT CLEAN JSON FOR THE APP ─────────────────────────────────────────
# Critical: pandas exports NaN for missing floats. NaN is valid Python
# but ILLEGAL in JSON. The browser's JSON.parse() throws silently on NaN,
# leaving allProperties empty and every budget filter returning zero results.
# Replace all NaN/Inf with null before serialising.

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

def clean_value(val):
    if val is None:
        return None
    if isinstance(val, float) and (math.isnan(val) or math.isinf(val)):
        return None
    return val

records = [{k: clean_value(v) for k, v in row.items()} for row in records]

# Assert before saving — do not skip this check
raw = json.dumps(records, separators=(',', ':'))
assert 'NaN' not in raw and 'Infinity' not in raw, "Invalid JSON — browser will reject this"

with open('data.json', 'w') as f:
    f.write(raw)

print(f"\nExported {len(records):,} records ({len(raw):,} bytes)")
print("Zero NaN values confirmed — safe for browser JSON.parse()")
```

---

## Building the App

The complete Python script that takes the clean JSON and injects it into the self-contained HTML file:

```python
import json, math, pandas as pd

# ── STEP 1: Build clean dataset ──────────────────────────────────────────────
df = pd.read_excel('EU_Real_Estate_Dataset.xlsx')
df['growth'] = (
    (df['sale_price_eur'] - df['last_sold_price_eur'])
    / df['last_sold_price_eur']
).round(4)

cols = [
    'property_id','property_type','listing_type','city','country',
    'bedrooms','bathrooms','square_meters','sale_price_eur','monthly_rent_eur',
    'price_per_sqm','days_on_market','latitude','longitude',
    'last_sold_price_eur','parking_spots','gym','swimming_pool',
    'elevator','furnishing_status','energy_rating','growth'
]

df_export = df[cols].copy().where(pd.notna(df[cols]), other=None)
records = df_export.to_dict(orient='records')

def clean_value(val):
    if val is None: return None
    if isinstance(val, float) and (math.isnan(val) or math.isinf(val)): return None
    return val

records = [{k: clean_value(v) for k, v in row.items()} for row in records]
data_json = json.dumps(records, separators=(',', ':'))

assert 'NaN' not in data_json


# ── STEP 2: Embed dataset inside the HTML ────────────────────────────────────
# Why embed instead of fetch()?
# Browsers block fetch() requests on file:// protocol (local files).
# Embedding makes the app completely self-contained — open it anywhere,
# no server, no network, no dependencies.
with open('app_template.html', 'r') as f:
    html = f.read()

html = html.replace(
    '<script>',
    f'<script>\nconst EMBEDDED_DATA = {data_json};\n',
    1  # Only replace the first <script> tag
)

with open('PropIQ_Real_Estate_Advisor.html', 'w') as f:
    f.write(html)

print(f"Built PropIQ_Real_Estate_Advisor.html")
print(f"Total size: {len(html) / 1_000_000:.1f} MB")
print(f"Properties embedded: {len(records):,}")
```

### How the App Uses the Embedded Data

```javascript
// On results screen load — no fetch, no async, no failure modes
async function loadAndRenderProperties(top3) {
  if (allProperties.length === 0) {
    allProperties = EMBEDDED_DATA; // The 5,000 properties, right here in memory
  }
  renderPropertiesTable(top3);
}

// Property filtering — budget, city, and type all applied at once
function renderPropertiesTable(top3) {
  const topCities = top3.map(c => c.city);

  let filtered = allProperties.filter(p =>
    topCities.includes(p.city)
    && p.sale_price_eur >= answers.budgetMin
    && p.sale_price_eur <= answers.budgetMax
    && p.listing_type === 'Sale'
  );

  if (answers.propType !== 'any') {
    filtered = filtered.filter(p => p.property_type === answers.propType);
  }

  // Sort by investment signal — undervaluation + speed composite
  filtered.sort((a, b) => {
    const cityAvgMap = {};
    CITY_DATA.forEach(c => { cityAvgMap[c.city] = c.avg_ppsqm; });
    const score = p => {
      const cityAvg = cityAvgMap[p.city] || 2500;
      return (cityAvg - p.price_per_sqm) / cityAvg * 50
           + (365 - p.days_on_market) * 0.1;
    };
    return score(b) - score(a);
  });

  const show = filtered.slice(0, 50);
  // Render with conditional formatting on vs City Avg column
}
```

---

## The Design Philosophy

PropIQ uses a design system called **Sovereign Ledger** — a private wealth aesthetic built on three principles:

### 1. Surfaces, Not Borders

High-end financial interfaces do not use lines to separate sections. They use depth. PropIQ has four layers of darkness that create hierarchy purely through background contrast — no `1px solid` borders anywhere in the layout. The transition of tone is the divider.

```
Layer 1 — Onyx #0d0d0f     →  Header, left advisor panel
Layer 2 — Onyx #141418     →  Main canvas, right panel
Layer 3 — Onyx #1c1c22     →  Cards, table wrappers, elevated elements
Layer 4 — Onyx #242430     →  Input fields, deepest insets
```

### 2. Glass for Floating Elements

Anything that floats above the canvas — the tab bar, the landing stats, the option buttons on hover — uses glassmorphism: a semi-transparent background with `backdrop-filter: blur`, giving the impression of frosted glass over the dark surface.

### 3. Editorial Typography

Headlines use **Cormorant Garamond**, a classical serif that carries the weight of financial authority. Body text uses **Outfit**, a geometric sans-serif that is clean and readable at small sizes. The combination signals that this is not a consumer app — it is a professional instrument.

The gold (`#c9a84c`) is never flat. It always appears as a warm gradient (`#c9a84c → #e2b95a`), which gives it the depth of real metal rather than a flat accent colour.

---

## Known Issues & Fixes

### Properties table showing empty despite valid budget range

**Root cause:** Python's `pandas` exports missing float values as `NaN`. JavaScript's `JSON.parse()` throws a `SyntaxError` on `NaN` (which is not valid JSON) and fails silently — `allProperties` stays as an empty array, and every filter returns zero results.

**Fix:** Pass all values through a cleaner before serialising, then assert the output contains no `NaN` before writing:

```python
def clean_value(val):
    if val is None: return None
    if isinstance(val, float) and (math.isnan(val) or math.isinf(val)): return None
    return val

records = [{k: clean_value(v) for k, v in row.items()} for row in records]
raw = json.dumps(records, separators=(',', ':'))
assert 'NaN' not in raw  # Never skip this
```

### App works in browser but shows no data when opened as a local file

**Root cause:** Browsers block `fetch()` requests on `file://` protocol for security. An external `data.json` file is unreachable when the HTML is opened from a local folder.

**Fix:** Embed the dataset as a `const` directly inside the HTML at build time. One file. No dependencies.

### Power BI — `goal` throws a syntax error in DAX

**Root cause:** `GOAL` is a reserved keyword in DAX.

**Fix:** Prefix all VAR names that might conflict with reserved words with an underscore: `VAR _goal`, `VAR _risk`, `VAR _horizon`.

### Power BI — `COUNTROWS(FILTER('data', [In Budget] = 1))` throws a context error

**Root cause:** Measures that use `SELECTEDVALUE()` internally cannot be called from inside a `FILTER()` on a table. DAX does not have a row context to resolve them.

**Fix:** Inline all filter logic directly inside the outer measure using column references and VAR declarations — never nest a context-dependent measure inside `FILTER()`.

---

## Getting Started

Download the HTML file and open it in any browser. That is the entire installation process.

```bash
git clone https://github.com/YOUR_USERNAME/propiq.git
cd propiq

# Open directly — no server needed
open PropIQ_Real_Estate_Advisor.html
```

To rebuild from the source Excel file after modifying the data:

```bash
pip install pandas openpyxl
python analysis/analyse.py
```

---

## What's Next

- **Mortgage calculator** — monthly payment projections at user-defined LTV and interest rate, turning the investment score into a cash flow forecast
- **Rental yield view** — for properties with both sale price and rental data, surface the gross yield as a primary metric for income investors
- **Neighbourhood scoring** — move from city-level to postcode-level benchmarks as richer data becomes available
- **One-click investment brief** — export a PDF summary of your personalised recommendations to share with a co-investor or financial advisor
- **Live data integration** — connect to a real-time property API so the intelligence updates with the market
- **Portfolio mode** — track multiple properties across cities and monitor how the investment score evolves over time

---

## License

MIT — use it, build on it, make money with it.

---

*Most data tools show you everything and help you decide nothing. PropIQ shows you what matters for your situation and tells you exactly what to do about it.*

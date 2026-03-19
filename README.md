# PropIQ — EU Real Estate Market Analysis

> **A data analysis of 5,000+ European property listings, presented not as a report or a dashboard — but as a personalised investment experience built directly in the browser.**

[![Dataset](https://img.shields.io/badge/Dataset-5%2C000%20EU%20Properties-gold?style=flat-square)](#the-dataset)
[![Markets](https://img.shields.io/badge/Markets-10%20EU%20Cities-blue?style=flat-square)](#market-findings)
[![Tool](https://img.shields.io/badge/Presented%20In-HTML%20%2F%20CSS%20%2F%20JS-green?style=flat-square)](#why-not-power-bi-or-excel)

---

## Table of Contents

1. [What This Analysis Is About](#what-this-analysis-is-about)
2. [The Thought Process — Why I Built It This Way](#the-thought-process--why-i-built-it-this-way)
3. [Why Not Power BI or Excel?](#why-not-power-bi-or-excel)
4. [The Dataset](#the-dataset)
5. [Analytical Framework](#analytical-framework)
6. [Key Market Findings](#key-market-findings)
7. [How the Scoring Model Works](#how-the-scoring-model-works)
8. [Analysis Code — Python](#analysis-code--python)
9. [Delivering the Analysis — HTML App Code](#delivering-the-analysis--html-app-code)
10. [Design Decisions](#design-decisions)
11. [Bugs Encountered & Fixed](#bugs-encountered--fixed)
12. [Getting Started](#getting-started)
13. [What I Would Do With More Data](#what-i-would-do-with-more-data)
14. [License](#license)

---

## What This Analysis Is About

This project analyses a dataset of **5,000 European property listings** across 10 major cities to answer a question every real estate investor actually asks:

> *Given my budget, my goal, and my risk appetite — where in Europe should I invest, what should I buy, and what should I avoid?*

The analysis covers:

- **Undervaluation signals** — which cities and individual properties are priced below their local market average
- **Demand velocity** — how fast properties are being absorbed in each market (days on market as a demand proxy)
- **Price growth** — appreciation from last sold price to current asking price, used as a historical momentum signal
- **Liquidity** — how quickly an investor can exit a position in each market
- **Composite investment scoring** — combining all four signals into a single ranked output, weighted by the investor's stated goal

The output is not a static report. The findings are delivered as an **interactive experience** where an investor inputs their profile and receives a personalised version of the analysis — their cities, their properties, their risk context.

---

## The Thought Process — Why I Built It This Way

Most data analysis projects end the same way: a PDF report, a Power BI dashboard, or an Excel workbook. The analyst does the hard work, produces the findings, and then hands the output to whoever commissioned it. That person reads it, nods, and then still asks — *"but what does this mean for me specifically?"*

That gap bothered me with this dataset in particular.

Real estate investment data is deeply personal. The same dataset means completely different things to different investors. A €500,000 budget in Paris buys you a small apartment. The same budget in Warsaw buys a portfolio. A short-term flipper needs to know which markets move fast. A long-term appreciation investor needs to know where prices have historically grown. A rental income investor needs to know where demand is structurally strong. These are not the same analysis — they are four different analyses of the same data.

**The conventional approach would have been to build one dashboard and let the user filter.** Filters are fine. But a filter doesn't explain *why* something is a good fit for you. It doesn't reweight the scoring model based on your goal. It doesn't tell you what to avoid. It doesn't give you a recommendation — it gives you a narrower version of the full dataset and leaves the interpretation entirely to you.

I wanted the analysis to do the interpretation. I wanted the output to speak directly to the person receiving it, in their context, with their constraints. That meant the analysis needed to capture the investor's profile first — and then deliver findings that were filtered, scored, and narrated specifically for that profile.

That decision — **analysis that personalises itself to the reader** — is what drove every other choice in the project.

---

## Why Not Power BI or Excel?

This is the honest answer to what most analysts would have reached for.

**Power BI** would have been the natural choice. The dataset is clean, the relationships are simple, and Power BI handles interactive filtering well. I actually built a full Power BI version of this analysis using DAX measures, disconnected parameter tables, What-If sliders, and the HTML Content visual for a styled narrative card. It works.

But Power BI has a ceiling when it comes to delivering a *guided* experience. You can build slicers. You can build bookmarks. You can approximate a questionnaire with buttons. But you cannot build a step-by-step flow where the analysis literally walks the investor through six questions before showing them anything — where the experience itself signals that the output has been built around their answers. That guided flow is not a cosmetic feature. It is a core part of how the findings land. An investor who has just told the analysis their goal and risk profile is primed to trust the recommendation in a way that someone who just clicked a slicer is not.

**Excel** would have been even more limiting. Excel is a calculation engine. It is excellent for financial modelling, scenario analysis, and structured data manipulation. For communicating findings to a non-analyst audience — let alone personalising those findings — it is the wrong tool.

**HTML, CSS, and JavaScript** gave me complete control over the experience of receiving the analysis. The same scoring model that could have lived in a DAX measure lives in a JavaScript function. The same city benchmarks that could have been a Power Query aggregation are a pre-computed object in the browser. The result is a self-contained file that opens in any browser, requires no software, no login, no license — and delivers a richer, more personalised experience than either BI tool would have produced.

The tool choice is not about preference. It is about what the analysis needed to do and what each tool is actually capable of.

---

## The Dataset

**5,000 European property listings** across 10 cities, covering both Sale and Rental listing types.

| Field | Description |
|---|---|
| `property_id` | Unique identifier |
| `listing_date` | Date listed |
| `property_type` | Apartment, Villa, Townhouse, Office, Retail, Warehouse, Mixed-Use |
| `listing_type` | Sale or Rental |
| `city` / `country` | Location |
| `bedrooms` / `bathrooms` | Unit configuration |
| `square_meters` | Floor area |
| `year_built` | Construction year |
| `sale_price_eur` | Asking price (Sale listings) |
| `monthly_rent_eur` | Monthly rent (Rental listings) |
| `price_per_sqm` | Derived price density |
| `days_on_market` | Listing age — used as demand proxy |
| `latitude` / `longitude` | Geolocation |
| `last_sold_price_eur` | Previous transaction — used to compute growth |
| `parking_spots` / `gym` / `swimming_pool` / `elevator` | Amenity flags |
| `furnishing_status` | Furnished / Semi / Unfurnished |
| `energy_rating` | EU efficiency label A–G |
| `floor_number` | Floor level |

### Split by Listing Type

| Type | Count | Notes |
|---|---|---|
| Sale | 2,955 | Used for investment scoring and property table |
| Rental | 2,045 | Used for demand context and rental yield signals |

### Price Distribution (Sale Listings)

| Percentile | Price |
|---|---|
| Minimum | €50,000 |
| 10th | €221,132 |
| 25th | €367,347 |
| Median | €646,363 |
| 75th | €1,229,698 |
| 90th | €2,236,793 |
| Maximum | €13,287,305 |

---

## Analytical Framework

The analysis is structured around four investment signals, each derived directly from fields in the dataset:

### Signal 1 — Undervaluation

Measures how cheap a city's average price per sqm is relative to the EU-wide average across all 10 cities. A city priced below the EU average has room for mean reversion — the core of a value investing thesis applied to real estate.

At the property level, the same logic applies: each listing is compared against its own city's average, not the EU average. A property 20% below its city average is the actionable entry signal.

### Signal 2 — Demand Velocity

`days_on_market` is used as a proxy for demand. A low days-on-market figure means supply is being absorbed quickly — buyers (or tenants) are competing for stock. This matters differently by investment goal: for a flipper it determines exit speed, for a rental investor it signals occupancy reliability, for a long-term holder it signals underlying demand fundamentals.

### Signal 3 — Price Growth

Calculated as:
```
growth = (sale_price_eur − last_sold_price_eur) / last_sold_price_eur
```

This is the only backward-looking signal in the model. It does not predict future growth — it reveals where capital has already been moving, which is the closest proxy the dataset provides for momentum.

### Signal 4 — Liquidity

Derived from days on market but framed as an exit measure rather than a demand measure. A market where properties sell in 90 days is materially more liquid than one where they sit for 300 days. For investors with shorter horizons or leverage, liquidity is not optional.

### Composite Score

The four signals are combined into a single Investment Score using weighted addition. The weights are not fixed — they shift based on the investor's stated goal:

| Goal | Undervaluation | Demand | Growth | Liquidity |
|---|---|---|---|---|
| Flip | 40% | 10% | 10% | 40% |
| Rental | 20% | 40% | 20% | 20% |
| Appreciation | 20% | 10% | 50% | 20% |

After the base score is computed, city-specific multipliers are applied based on risk tolerance and location preference, then the score is clamped to [0, 100].

---

## Key Market Findings

### City Benchmarks

| City | Country | Avg €/sqm | Avg Days Listed | Avg Growth | Listings |
|---|---|---|---|---|---|
| Paris | France | €5,201 | 172 days | +97% | 730 |
| Amsterdam | Netherlands | €4,754 | 183 days | +99% | 592 |
| Berlin | Germany | €3,233 | 164 days | +75% | 641 |
| Brussels | Belgium | €2,784 | 172 days | +117% | 305 |
| Vienna | Austria | €2,774 | 170 days | +93% | 532 |
| Rome | Italy | €2,760 | 173 days | +82% | 536 |
| Prague | Czech Republic | €2,181 | 162 days | +80% | 335 |
| Madrid | Spain | €2,171 | 175 days | +96% | 551 |
| Lisbon | Portugal | €1,881 | 171 days | +78% | 409 |
| Warsaw | Poland | €1,503 | 171 days | +71% | 369 |

### What the Data Reveals

**Brussels is the most interesting anomaly in the dataset.** It has the highest growth signal (+117%) while sitting in the mid-market price band. It is neither as expensive as Paris nor as geographically peripheral as Warsaw. For an appreciation investor, it is the clearest signal in the data.

**Berlin is the fastest market.** At 164 average days on market, it absorbs listings faster than any other city in the dataset. For investors who need liquidity — whether because of leverage, short horizons, or exit flexibility — Berlin's market depth is meaningful.

**The premium cities are not the best growth plays.** Paris and Amsterdam command the highest prices but their growth signals (+97% and +99%) are not proportionally higher than mid-market cities like Brussels (+117%) or Madrid (+96%). Price leadership does not imply growth leadership.

**Warsaw has the largest undervaluation gap.** At €1,503/sqm it sits 48% below the EU average in this dataset. For an investor with a long horizon and appetite for emerging market risk, that gap represents the widest structural upside of any city in the analysis.

**Apartments are more liquid than villas by a measurable margin.** Average days on market: Villas 164 days, Apartments 174 days. The direction is counterintuitive — villas move faster on average — but the gap is narrow enough that property-specific factors (location, condition, pricing) dominate. The more useful signal is within-city variation, which the property table surfaces through the vs City Average column.

---

## How the Scoring Model Works

### City-Level Components

```
Undervaluation  =  max(0,  (EU_avg_ppsqm − city_avg_ppsqm) / EU_avg_ppsqm  × 100)
Demand          =  max(0,  (EU_avg_dom − city_avg_dom) / EU_avg_dom  × 100  + 50)
Growth          =  min(100, city_avg_growth × 50)
Liquidity       =  max(0,  100 − (city_avg_dom / 365 × 100))
```

Where:
- `EU_avg_ppsqm` = €2,903 (mean across all 10 cities)
- `EU_avg_dom` = 172 days (mean across all 10 cities)
- `city_avg_growth` = mean of individual property growth values per city

### Risk & Location Multipliers

```
Low risk  + [Paris / Amsterdam / Vienna]    → base score × 1.12
High risk + [Warsaw / Prague / Brussels]    → base score × 1.12
Low risk  + [Warsaw / Prague / Brussels]    → base score × 0.85

Major cities preference + major city        → base score × 1.15
Emerging preference    + emerging city      → base score × 1.15
Major cities preference + emerging city     → base score × 0.80

Short horizon → score + (50 − city_avg_dom) × 0.2
Long horizon  → score + city_avg_growth × 5

Final: clamp to [0, 100]
```

### Property-Level Signal (vs City Average)

For each individual listing in the filtered results table:

```
vs_city_avg = (property.price_per_sqm − city.avg_ppsqm) / city.avg_ppsqm
```

Negative = below city average (potential value entry)
Positive = above city average (premium pricing)

This is the most actionable signal for an investor who has already decided on a city — it tells them whether a specific property is cheap or expensive within that local market context.

---

## Analysis Code — Python

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
# Price growth: how much has each property appreciated since last transaction?
# This is the only backward-looking signal — a historical momentum indicator.
df['growth'] = (
    (df['sale_price_eur'] - df['last_sold_price_eur'])
    / df['last_sold_price_eur']
).round(4)


# ── 3. CITY-LEVEL BENCHMARKS ────────────────────────────────────────────────
# Every individual property signal is meaningless without a local reference.
# These city averages become the denominator for undervaluation calculations.
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
# Rental listings do not carry meaningful sale price growth data.
# Isolate Sale listings for the appreciation analysis.
df_sale = df[df['listing_type'] == 'Sale'].copy()
growth_by_city = df_sale.groupby('city')['growth'].mean().round(3)

print('\nAverage price growth since last sale, by city:')
print(growth_by_city)


# ── 5. DEMAND VELOCITY BY PROPERTY TYPE ─────────────────────────────────────
# Days on market by property type — which asset classes
# are absorbed fastest? Informs property type recommendations.
type_demand = df.groupby('property_type')['days_on_market'].mean().round(1)
print('\nAverage days on market by property type:')
print(type_demand)


# ── 6. PRICE DISTRIBUTION ────────────────────────────────────────────────────
# Understanding the full price range shapes the budget slider defaults
# in the interactive output. Setting wide defaults ensures the analysis
# surfaces results without requiring the user to adjust anything first.
sale_prices = df[df['listing_type'] == 'Sale']['sale_price_eur'].dropna()
prices_sorted = sorted(sale_prices)
n = len(prices_sorted)

print('\nSale price distribution:')
for label, pct in [('Min','0'), ('p10','10'), ('p25','25'), ('p50','50'),
                   ('p75','75'), ('p90','90'), ('Max','100')]:
    idx = 0 if pct == '0' else (-1 if pct == '100' else int(n * int(pct) / 100))
    print(f"  {label}:  €{prices_sorted[idx]:,.0f}")
print(f"  Total sale listings: {n:,}")


# ── 7. EXPORT CLEAN JSON ──────────────────────────────────────────────────────
# pandas exports missing floats as NaN — valid Python, illegal JSON.
# JSON.parse() in the browser throws silently on NaN, returning undefined
# and leaving the entire property array empty. Clean before serialising.

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

# Verify before writing — do not skip this
raw = json.dumps(records, separators=(',', ':'))
assert 'NaN' not in raw and 'Infinity' not in raw, "Invalid JSON values remain"

with open('data.json', 'w') as f:
    f.write(raw)

print(f"\nExported {len(records):,} records ({len(raw):,} bytes)")
print("Zero NaN confirmed — safe for browser JSON.parse()")
```

### Analysis Output

```
Shape: (5000, 25)

City benchmarks:
        city  avg_price_sqm  avg_days  count    avg_price         country
   Amsterdam        4754.25    183.39    592  1652546.52     Netherlands
      Berlin        3232.56    164.34    641   974956.85         Germany
    Brussels        2783.67    172.47    305   956922.21         Belgium
      Lisbon        1880.98    170.50    409   694433.16        Portugal
      Madrid        2171.06    175.18    551   790773.06           Spain
       Paris        5200.85    172.22    730  1708074.72          France
      Prague        2181.47    162.30    335   747992.46  Czech Republic
        Rome        2760.13    173.04    536   958883.25           Italy
      Vienna        2774.07    170.10    532   875516.36         Austria
      Warsaw        1503.03    170.57    369   465858.66          Poland

Average growth since last sale:
Brussels    1.169  (+117%)
Amsterdam   0.992  (+99%)
Paris       0.971  (+97%)
Madrid      0.963  (+96%)
Vienna      0.932  (+93%)
Rome        0.822  (+82%)
Prague      0.800  (+80%)
Lisbon      0.776  (+78%)
Berlin      0.750  (+75%)
Warsaw      0.705  (+71%)

Days on market by property type:
Villa        164.4
Townhouse    169.0
Office       169.8
Warehouse    172.0
Mixed-Use    172.6
Apartment    173.7
Retail       177.8

Sale price distribution:
  Min:   €50,000
  p10:   €221,132
  p25:   €367,347
  p50:   €646,363
  p75:   €1,229,698
  p90:   €2,236,793
  Max:   €13,287,305
  Total sale listings: 2,955
```

---

## Delivering the Analysis — HTML App Code

Once the analysis was complete, the question became: **how do I deliver these findings in a way that is personalised to the reader?**

The answer was to build the output in HTML/CSS/JavaScript — a medium that lets the scoring model run live in the browser, responding to the investor's inputs in real time, without requiring any software, login, or connection.

### Embedding the Dataset

The biggest technical decision was how to get 5,000 records into the browser. A `fetch()` call to an external file fails silently when the HTML is opened directly from a local folder (`file://` protocol blocks network requests). The solution was to embed the entire cleaned dataset as a JavaScript constant at build time:

```python
# Inject dataset into the HTML at build time
with open('app_template.html', 'r') as f:
    html = f.read()

with open('data.json', 'r') as f:
    data = f.read()

# Replace the first <script> tag to inject the data constant
html = html.replace(
    '<script>',
    f'<script>\nconst EMBEDDED_DATA = {data};\n',
    1
)

with open('PropIQ_Real_Estate_Advisor.html', 'w') as f:
    f.write(html)
```

The HTML file becomes entirely self-contained — one file, open in any browser, no dependencies.

### The Scoring Model in JavaScript

The same analytical logic from Python runs live in the browser, recalculating on every input change:

```javascript
// City-level scoring — runs once per city per answer change
function scoreCity(city) {
  const { goal, location, risk, horizon } = answers;

  // Four component scores (0–100 each)
  const undervalScore = Math.max(0,
    (globalAvgPpsqm - city.avg_ppsqm) / globalAvgPpsqm * 100
  );
  const demandScore = Math.max(0,
    (globalAvgDom - city.avg_dom) / globalAvgDom * 100 + 50
  );
  const growthScore   = Math.min(100, city.avg_growth * 50);
  const liquidScore   = Math.max(0, 100 - (city.avg_dom / 365 * 100));

  // Goal-based weights — same logic as the Python analysis
  const weights = {
    flip:         { underval:0.4, demand:0.1, growth:0.1, liquid:0.4 },
    rental:       { underval:0.2, demand:0.4, growth:0.2, liquid:0.2 },
    appreciation: { underval:0.2, demand:0.1, growth:0.5, liquid:0.2 },
  };
  const w = weights[goal] || { underval:0.3, demand:0.3, growth:0.2, liquid:0.2 };

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

### Property Filtering

Listings are filtered against the investor's budget, top-ranked cities, and property type preference — then sorted by the same investment signal used for city scoring:

```javascript
function renderPropertiesTable(top3) {
  const topCities  = top3.map(c => c.city);
  const cityAvgMap = Object.fromEntries(CITY_DATA.map(c => [c.city, c.avg_ppsqm]));

  // Filter to budget, top cities, listing type, and property type
  let filtered = allProperties.filter(p =>
    topCities.includes(p.city)
    && p.sale_price_eur >= answers.budgetMin
    && p.sale_price_eur <= answers.budgetMax
    && p.listing_type === 'Sale'
  );

  if (answers.propType !== 'any') {
    filtered = filtered.filter(p => p.property_type === answers.propType);
  }

  // Sort by undervaluation + speed composite
  filtered.sort((a, b) => {
    const score = p => {
      const cityAvg = cityAvgMap[p.city] || 2500;
      return (cityAvg - p.price_per_sqm) / cityAvg * 50
           + (365 - p.days_on_market) * 0.1;
    };
    return score(b) - score(a);
  });

  // Display top 50 with vs City Average conditional formatting
  const show = filtered.slice(0, 50);
  // ... render table rows
}
```

---

## Design Decisions

The visual presentation follows a **private wealth aesthetic** — the design is intended to match the seriousness of the analysis and the profile of the investor receiving it.

**No borders for layout.** Sections are separated by background colour shifts across a four-step darkness scale (Onyx `#0d0d0f` through `#242430`), not lines. This is a deliberate choice — borders make interfaces feel like forms. Background shifts make them feel like surfaces.

**Typography is editorial.** Headlines use Cormorant Garamond (serif), a typeface associated with financial publishing. Body text uses Outfit (sans-serif), clean and readable at small sizes. The pairing signals that this is a professional instrument, not a consumer product.

**Gold as the accent is intentional.** The warm gold gradient (`#c9a84c → #e2b95a`) connects the visual language to real estate, wealth, and investment — without being decorative. Every gold element carries a meaning: a score, a recommendation, a selected state.

**Glassmorphism for floating elements.** The tab bar, landing stats panel, and option buttons on hover use `backdrop-filter: blur` with semi-transparent backgrounds. This creates depth without adding visual noise.

---

## Bugs Encountered & Fixed

### Properties table returned zero results despite valid budget

**Cause:** `pandas` exports missing float values as `NaN`. This is legal Python but illegal JSON. The browser's `JSON.parse()` fails silently on `NaN` — it does not throw a visible error, it just returns `undefined` for the entire parse. `allProperties` stays empty. Every filter returns zero results.

**Fix:** Clean all values through a function that converts `NaN` and `Infinity` to `None` before serialising. Assert the output contains neither before writing to disk.

### App showed no data when opened as a local file

**Cause:** Browsers block `fetch()` on `file://` protocol. An external `data.json` will always fail when the HTML is opened from the filesystem without a local server.

**Fix:** Embed the dataset directly inside the HTML file at build time as a JavaScript constant. No fetch required.

### Power BI port — `goal` threw a DAX syntax error

**Cause:** `GOAL` is a reserved keyword in DAX.

**Fix:** Prefix reserved-word VAR names with underscore: `VAR _goal`, `VAR _risk`, `VAR _horizon`.

### Power BI port — `COUNTROWS(FILTER('data', [In Budget] = 1))` threw a context error

**Cause:** Measures that use `SELECTEDVALUE()` cannot be called from inside a `FILTER()` on a table. DAX has no row context to resolve them at that point.

**Fix:** Inline all filter conditions directly inside the outer measure using column references and VAR declarations. Never nest a context-dependent measure inside `FILTER()`.

---

## Getting Started

```bash
git clone https://github.com/YOUR_USERNAME/propiq.git
cd propiq

# Open the analysis output — no install, no server, no login
open PropIQ_Real_Estate_Advisor.html
```

To rerun the Python analysis from source:

```bash
pip install pandas openpyxl
python analysis/analyse.py
```

---

## What I Would Do With More Data

- **Neighbourhood-level pricing** — city averages flatten a lot of within-city variation. A postcode-level benchmark would make the vs City Average signal significantly sharper.
- **Time series** — with listing date history, the days-on-market trend (getting faster or slower) would be more valuable than the current snapshot figure.
- **Rental yield** — with both sale price and monthly rent on the same properties, a gross yield calculation would add a direct income return signal alongside the capital appreciation signal.
- **Transaction volume** — the number of completed sales, not just listings, would make the demand signal more reliable. Days on market is a proxy; actual transaction velocity is the real measure.
- **Macroeconomic overlay** — linking city-level data to GDP growth, population flow, and interest rate environment would contextualise why some markets are growing faster than others.

---

## License

MIT — use it, build on it, extend it.

---

*The analysis was done in Python. The findings were delivered in HTML. The tool choice was deliberate — because how you present an analysis is part of the analysis.*

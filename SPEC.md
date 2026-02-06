# PocketWise — Financial Calculator Suite
# Build Specification

## Overview
Build 15 financial calculators as a static site deployed to Vercel. Each tool is a standalone HTML page linking to a shared CSS design system. Modern fintech aesthetic (Stripe/NerdWallet quality).

## Tech Stack
- **Static HTML/CSS/JS** — no frameworks
- **Shared CSS**: `/css/style.css` (comprehensive design system already written)
- **JS**: Inline in each page (vanilla, no dependencies)
- **Hosting**: Vercel (static deployment)
- **Fonts**: Plus Jakarta Sans (headings), Inter (body), JetBrains Mono (numbers) — loaded via CSS

## File Structure
Each tool goes in: `/home/henry/.openclaw/workspace/pocketwise/[slug]/index.html`
Shared CSS at: `/home/henry/.openclaw/workspace/pocketwise/css/style.css`

## Page Template
Every tool page MUST follow this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Tool Name] — Free Online Calculator | PocketWise</title>
  <meta name="description" content="[SEO meta description, 150-160 chars]">
  <link rel="canonical" href="https://pocketwise.io/[slug]/">
  <link rel="stylesheet" href="/css/style.css">
  <style>
    /* Tool-specific CSS only — design system is in /css/style.css */
  </style>
</head>
<body>
  <!-- NAVIGATION -->
  <nav class="lw-nav">
    <div class="lw-nav-inner">
      <a href="/" class="lw-logo">
        <div class="lw-logo-icon">L</div>
        PocketWise
      </a>
      <ul class="lw-nav-links">
        <li><a href="/mortgage-calculator/">Mortgage</a></li>
        <li><a href="/auto-loan-calculator/">Auto</a></li>
        <li><a href="/compound-interest-calculator/">Investing</a></li>
        <li><a href="/debt-payoff-calculator/">Debt</a></li>
        <li><a href="/">All Tools</a></li>
      </ul>
      <button class="lw-hamburger" onclick="document.querySelector('.lw-mobile-menu').classList.toggle('open')" aria-label="Menu">☰</button>
    </div>
    <div class="lw-mobile-menu">
      <a href="/">All Tools</a>
      <a href="/mortgage-calculator/">Mortgage Calculator</a>
      <a href="/auto-loan-calculator/">Auto Loan Calculator</a>
      <a href="/personal-loan-calculator/">Personal Loan Calculator</a>
      <a href="/compound-interest-calculator/">Compound Interest Calculator</a>
      <a href="/debt-payoff-calculator/">Debt Payoff Calculator</a>
      <a href="/credit-card-payoff-calculator/">Credit Card Payoff</a>
      <a href="/home-affordability-calculator/">Home Affordability</a>
      <a href="/refinance-calculator/">Refinance Calculator</a>
      <a href="/loan-comparison-tool/">Loan Comparison</a>
      <a href="/amortization-schedule/">Amortization Schedule</a>
      <a href="/debt-to-income-calculator/">Debt-to-Income</a>
      <a href="/apr-calculator/">APR Calculator</a>
      <a href="/savings-goal-calculator/">Savings Goal Calculator</a>
      <a href="/investment-return-calculator/">Investment Returns</a>
      <a href="/emergency-fund-calculator/">Emergency Fund</a>
    </div>
  </nav>

  <main class="lw-main">
    <!-- HERO -->
    <div class="lw-hero">
      <span class="lw-badge">[Badge Text]</span>
      <h1>[Tool Name with <span class="accent">gradient word</span>]</h1>
      <p class="subtitle">[Compelling subtitle]</p>
    </div>

    <!-- TOOL INTERFACE (input card) -->
    <div class="lw-card">
      <!-- Inputs here using .lw-form-group, .lw-label, .lw-input, .lw-range, .lw-select -->
    </div>

    <!-- RESULTS -->
    <div class="lw-result-hero">
      <!-- Big number result -->
    </div>
    <div class="lw-result-grid">
      <!-- Breakdown items -->
    </div>

    <!-- VISUAL (chart, table, etc.) -->
    <div class="lw-card">
      <!-- Chart or data visualization -->
    </div>

    <!-- SEO CONTENT -->
    <div class="lw-content">
      <h2>...</h2>
      <p>...</p>
      <!-- 500+ words of educational content -->
      <!-- FAQ section with lw-faq accordion -->
    </div>

    <!-- RELATED TOOLS -->
    <div class="lw-related">
      <h2>Related Calculators</h2>
      <div class="lw-related-grid">
        <a href="/[slug]/" class="lw-related-link"><span class="dot"></span> [Tool Name]</a>
        <!-- 3-6 related tool links -->
      </div>
    </div>

    <!-- DISCLAIMER -->
    <p class="lw-disclaimer">
      <em>This calculator is for educational purposes only. Results are estimates and should not be considered financial advice. Consult a qualified financial advisor for personalized guidance.</em>
    </p>
  </main>

  <!-- FOOTER -->
  <footer class="lw-footer">
    <p>© 2026 PocketWise. Free financial calculators for everyone.</p>
  </footer>

  <script>
  (function() {
    'use strict';
    // Tool logic
    // Use real-time calculation (update on every input change)
    // Format numbers with Intl.NumberFormat or toLocaleString
    // Animate number changes smoothly
  })();
  </script>

  <!-- FAQ Schema -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "FAQPage",
    "mainEntity": [...]
  }
  </script>
</body>
</html>
```

## Design Principles
1. **Real-time calculation** — NO submit buttons. Update results on every input change.
2. **Number formatting** — Always format currency ($1,234.56), percentages (6.5%), and large numbers
3. **JetBrains Mono** for all numeric outputs — use class `lw-mono`
4. **Visual data** — Every tool needs charts, bars, or visual breakdowns, not just numbers
5. **Smooth animations** — Animate bar fills, number transitions, result reveals
6. **Mobile-first** — Touch-friendly inputs (44px+ targets), single column on mobile
7. **Trustworthy feel** — Clean, precise, no flashy gimmicks. Think fintech.
8. **SEO**: 500+ words of educational content, 5 FAQs, proper H2/H3, FAQ schema

## Common JS Utilities
Include these in each tool's script (copy into each file):

```javascript
function fmt(n) { return new Intl.NumberFormat('en-US', {style:'currency', currency:'USD', minimumFractionDigits:0, maximumFractionDigits:0}).format(n); }
function fmtFull(n) { return new Intl.NumberFormat('en-US', {style:'currency', currency:'USD', minimumFractionDigits:2, maximumFractionDigits:2}).format(n); }
function fmtNum(n) { return new Intl.NumberFormat('en-US').format(Math.round(n)); }
function fmtPct(n) { return n.toFixed(1) + '%'; }
function pmt(rate, nper, pv) { if (rate === 0) return pv / nper; return pv * (rate * Math.pow(1+rate,nper)) / (Math.pow(1+rate,nper)-1); }
```

---

## TOOL SPECIFICATIONS

### 1. Mortgage Calculator
**Slug:** `mortgage-calculator`
**Keywords:** "mortgage calculator", "home loan calculator", "monthly mortgage payment"

**Inputs:**
- Home price ($50K-$2M, default $350,000)
- Down payment ($ amount or %, default 20%)
- Loan term (15/20/30 years, toggle buttons)
- Interest rate (1-12%, default 6.5%)
- Property tax rate (%/year, default 1.2%)
- Home insurance ($/year, default $1,500)
- PMI rate (auto-calculated if down payment <20%, typically 0.5-1%)

**Calculations:**
- Monthly P&I = PMT formula
- Monthly taxes = (home price × tax rate) / 12
- Monthly insurance = annual / 12
- Monthly PMI = (loan amount × PMI rate) / 12 (if applicable)
- Total monthly = P&I + taxes + insurance + PMI

**Output:**
- Big number: Monthly payment
- Donut chart: Payment breakdown (P&I, taxes, insurance, PMI)
- Result grid: Total interest, total cost, loan amount
- Mini amortization preview (first 5 years)

**Related:** Home Affordability, Refinance, Amortization Schedule, APR Calculator

---

### 2. Auto Loan Calculator
**Slug:** `auto-loan-calculator`
**Keywords:** "auto loan calculator", "car payment calculator", "car loan calculator"

**Inputs:**
- Vehicle price ($5K-$150K, default $35,000)
- Down payment ($, default $5,000)
- Trade-in value ($, default $0)
- Sales tax rate (%, default 7%)
- Loan term (24/36/48/60/72/84 months, toggle or select)
- Interest rate (0-25%, default 5.9%)

**Calculations:**
- Amount financed = (price - down - trade) × (1 + tax rate)
- Monthly payment = PMT formula
- Total interest, total cost

**Output:**
- Big number: Monthly payment
- Result grid: Amount financed, total interest, total cost
- Bar chart: Principal vs Interest vs Tax breakdown
- "What if" section: Show payment at different terms (table)

**Related:** Personal Loan, Loan Comparison, APR Calculator

---

### 3. Personal Loan Calculator
**Slug:** `personal-loan-calculator`
**Keywords:** "personal loan calculator", "loan payment calculator", "loan calculator"

**Inputs:**
- Loan amount ($1K-$100K, default $15,000)
- Loan term (12-84 months, default 36)
- Interest rate (2-36%, default 9.5%)
- Origination fee (0-8%, default 0%)

**Calculations:**
- Monthly payment = PMT formula
- True cost with fees
- APR (accounting for origination fee)
- Payoff date

**Output:**
- Big number: Monthly payment
- Result grid: Total interest, total cost, payoff date, APR
- Payment timeline chart (bars showing principal vs interest per year)

**Related:** Loan Comparison, Auto Loan, APR Calculator, DTI Calculator

---

### 4. Compound Interest Calculator
**Slug:** `compound-interest-calculator`
**Keywords:** "compound interest calculator", "investment calculator", "compound growth calculator"

**Inputs:**
- Initial investment ($0-$1M, default $10,000)
- Monthly contribution ($0-$10K, default $500)
- Annual return rate (0-30%, default 8%)
- Time period (1-50 years, default 20)
- Compound frequency (Monthly/Quarterly/Annually, default Monthly)

**Calculations:**
- Future value with compound interest + regular contributions
- Total contributions = initial + (monthly × 12 × years)
- Total interest earned = future value - total contributions

**Output:**
- Big number: Future value
- Result grid: Total contributions, interest earned, growth multiple
- AREA CHART: Stacked area showing contributions (blue) vs earnings (green) over time
  - Use CSS or SVG to draw this — horizontal bars per year stacked
- Year-by-year table (collapsible)

**Related:** Investment Return, Savings Goal, Emergency Fund

---

### 5. Debt Payoff Calculator (Snowball vs Avalanche)
**Slug:** `debt-payoff-calculator`
**Keywords:** "debt payoff calculator", "debt snowball calculator", "debt avalanche calculator"

**Inputs:**
- Add multiple debts (dynamic form, up to 10):
  - Debt name (text input)
  - Balance ($)
  - Minimum payment ($)
  - APR (%)
  - "Add Debt" button
- Extra monthly payment ($0-$2000, default $200)

**Calculations:**
- Snowball method: Pay minimums on all, extra goes to smallest balance
- Avalanche method: Pay minimums on all, extra goes to highest APR
- For each: total months, total interest paid, payoff timeline

**Output:**
- Side-by-side comparison cards: Snowball vs Avalanche
- For each: months to payoff, total interest, total paid
- Winner highlight (which saves more)
- Visual timeline: Stacked horizontal bars showing when each debt gets paid off
- Savings difference prominently displayed

**Related:** Credit Card Payoff, DTI Calculator, Personal Loan, Emergency Fund

---

### 6. Credit Card Payoff Calculator
**Slug:** `credit-card-payoff-calculator`
**Keywords:** "credit card payoff calculator", "credit card payment calculator", "how long to pay off credit card"

**Inputs:**
- Current balance ($100-$100K, default $5,000)
- APR (5-30%, default 22.99%)
- Mode toggle: "I'll pay fixed monthly" / "I want to pay off in X months"
  - Fixed: Monthly payment ($, must be > monthly interest)
  - Timeline: Number of months (1-120)

**Calculations:**
- If fixed payment: months to payoff, total interest
- If target months: required monthly payment, total interest
- Minimum payment scenario (for comparison): 2% of balance or $25

**Output:**
- Big number: Months to payoff OR Required payment
- Result grid: Total interest, total paid
- Scary comparison: "Minimum payment" scenario (showing years and total interest)
- Bar chart: Interest vs principal over time by year
- "What if I add $X more?" quick scenarios (+$50, +$100, +$200)

**Related:** Debt Payoff, DTI Calculator, Personal Loan

---

### 7. Loan Comparison Tool
**Slug:** `loan-comparison-tool`
**Keywords:** "loan comparison calculator", "compare loans", "loan comparison tool"

**Inputs:**
- Loan A: Amount, Rate, Term (months), Origination Fee (%)
- Loan B: Amount, Rate, Term (months), Origination Fee (%)
- (Pre-filled with example values)

**Calculations:**
- For each: Monthly payment, total interest, total cost, APR
- Difference in each category

**Output:**
- Side-by-side comparison with green highlight on winner per row
- Metrics: Monthly payment, total interest, total cost, APR
- Savings summary: "Loan [A/B] saves you $X over the life of the loan"
- Visual bars comparing each metric

**Related:** Personal Loan, Auto Loan, Mortgage, APR Calculator

---

### 8. Home Affordability Calculator
**Slug:** `home-affordability-calculator`
**Keywords:** "home affordability calculator", "how much house can I afford", "home buying calculator"

**Inputs:**
- Annual gross income ($20K-$500K, default $85,000)
- Monthly debt payments ($0-$5K, default $400)
- Down payment amount ($0-$500K, default $50,000)
- Interest rate (1-12%, default 6.5%)
- Loan term (15/20/30, default 30)
- Property tax rate (%, default 1.2%)
- Insurance ($/year, default $1,500)
- DTI limit (%, default 36% — with note about 28% housing-only rule)

**Calculations:**
- Max monthly housing payment = (Income/12 × DTI%) - existing debts
- Work backwards from PMT formula to find max loan amount
- Max home price = max loan + down payment
- Monthly breakdown at max price

**Output:**
- Big number: "You can afford up to $XXX,XXX"
- Gauge showing comfort zone (Conservative/Moderate/Aggressive)
  - Conservative: 28% housing DTI
  - Moderate: 33% housing DTI
  - Aggressive: 36%+ housing DTI
- Monthly payment breakdown at max price
- Result grid: Max loan, monthly payment, DTI ratio

**Related:** Mortgage, DTI Calculator, Refinance

---

### 9. Refinance Calculator
**Slug:** `refinance-calculator`
**Keywords:** "refinance calculator", "mortgage refinance calculator", "should I refinance"

**Inputs:**
- Current loan: Remaining balance, current rate, remaining term (months)
- New loan: New rate, new term (months), closing costs ($)

**Calculations:**
- Current monthly payment, new monthly payment
- Monthly savings = old - new
- Break-even months = closing costs / monthly savings
- Total savings over remaining life (accounting for different term lengths)

**Output:**
- Big number: Monthly savings
- Break-even: "You'll break even in X months"
- Visual timeline: Break-even point marked on a timeline
- Result grid: Current vs New payment, total savings, break-even
- Verdict: "Worth it if you stay X+ months"

**Related:** Mortgage, Amortization, Home Affordability

---

### 10. Amortization Schedule Generator
**Slug:** `amortization-schedule`
**Keywords:** "amortization schedule", "amortization calculator", "loan amortization table"

**Inputs:**
- Loan amount ($1K-$2M, default $250,000)
- Interest rate (0.5-15%, default 6.5%)
- Loan term (years: 5/10/15/20/25/30, default 30)
- Extra monthly payment ($0-$5K, default $0)

**Calculations:**
- Full month-by-month schedule: payment #, payment, principal, interest, extra, remaining balance
- Summary stats with/without extra payments

**Output:**
- Summary card: Monthly payment, total interest (with/without extra), payoff date, time saved
- VISUAL: Area chart showing principal vs interest portions over time
  - Two stacked areas that cross over (interest starts high, principal ends high)
- Full amortization table (paginated or scrollable, show yearly summary with expand to monthly)
- If extra payments: highlight savings in green

**Related:** Mortgage, Refinance, Personal Loan, Loan Comparison

---

### 11. Debt-to-Income Calculator
**Slug:** `debt-to-income-calculator`
**Keywords:** "debt to income ratio calculator", "DTI calculator", "what is my DTI"

**Inputs:**
- Monthly gross income ($)
- Monthly debts (individual fields):
  - Rent/Mortgage ($)
  - Car payment ($)
  - Student loans ($)
  - Credit card minimums ($)
  - Other debts ($)

**Calculations:**
- Front-end DTI (housing only / income)
- Back-end DTI (all debts / income)
- Categories: Excellent (<28%), Good (28-35%), Fair (36-43%), Poor (43-50%), Very Poor (>50%)

**Output:**
- Big number: DTI ratio with category badge
- Gauge visualization: colored zones (green → yellow → red)
- What lenders think: side labels on gauge
- Breakdown: pie/donut showing income allocation (housing, debts, remaining)
- Tips to improve DTI

**Related:** Home Affordability, Mortgage, Personal Loan, Credit Card Payoff

---

### 12. APR Calculator
**Slug:** `apr-calculator`
**Keywords:** "APR calculator", "annual percentage rate calculator", "loan APR calculator"

**Inputs:**
- Loan amount ($)
- Interest rate (%)
- Loan term (months)
- Fees: Origination fee ($), Points ($), Other fees ($)

**Calculations:**
- APR using Newton's method or iterative approach
- Monthly payment (at stated rate vs at APR)
- Total cost difference

**Output:**
- Side-by-side: Stated Rate vs APR (big numbers)
- "The fees add X% to your effective rate"
- Result grid: Monthly payment, total interest, total fees, total cost
- Visual: Rate vs APR bar comparison

**Related:** Mortgage, Personal Loan, Auto Loan, Loan Comparison

---

### 13. Savings Goal Calculator
**Slug:** `savings-goal-calculator`
**Keywords:** "savings goal calculator", "savings calculator", "how long to save for"

**Inputs:**
- Goal amount ($1K-$5M, default $25,000)
- Current savings ($, default $2,000)
- Monthly contribution ($, default $500)
- Expected annual return (0-15%, default 4%)

**Calculations:**
- Months to reach goal (with and without returns)
- If monthly amount given: when you'll reach goal
- Alternative: "How much do I need to save monthly to reach goal in X months?"

**Output:**
- Big number: Time to goal (X years, Y months)
- Without returns comparison (how much longer)
- Progress bar: Current savings → Goal
- Growth chart: Savings line over time approaching goal line
- Result grid: Total contributed, interest earned, goal date

**Related:** Emergency Fund, Compound Interest, Investment Return

---

### 14. Investment Return Calculator
**Slug:** `investment-return-calculator`
**Keywords:** "investment return calculator", "investment calculator", "investment growth calculator"

**Inputs:**
- Initial investment ($, default $10,000)
- Monthly additions ($, default $300)
- Annual return rate (%, default 8%)
- Investment period (years, default 25)
- Inflation rate (%, default 3%, optional toggle)

**Calculations:**
- Nominal future value
- Inflation-adjusted (real) future value
- Total contributions, total earnings
- Average annual return in dollars

**Output:**
- Big number: Future value (nominal)
- Secondary: Inflation-adjusted value (with note)
- Result grid: Total contributed, total earnings, real value
- Chart: Growth curve with inflation-adjusted overlay (lighter/dashed)
- Year-by-year table (collapsible)

**Related:** Compound Interest, Savings Goal, Emergency Fund

---

### 15. Emergency Fund Calculator
**Slug:** `emergency-fund-calculator`
**Keywords:** "emergency fund calculator", "how much emergency fund", "emergency savings calculator"

**Inputs:**
- Monthly expenses (itemized):
  - Housing/Rent ($)
  - Utilities ($)
  - Food/Groceries ($)
  - Transportation ($)
  - Insurance ($)
  - Other essentials ($)
- Months of coverage: 3/6/9/12 (toggle buttons, default 6)
- Current emergency savings ($, default $0)
- Monthly amount you can save ($, default $300)

**Calculations:**
- Target fund = total monthly expenses × months
- Gap = target - current savings
- Months to fully funded = gap / monthly savings

**Output:**
- Big number: Target emergency fund amount
- Progress bar: Current → Target (with percentage)
- "You'll be fully funded in X months" (or "You're already there! 🎉")
- Donut chart: Expense breakdown
- Result grid: Monthly expenses, target, gap, months to goal
- Tips: Where to keep your emergency fund (HYSA recommendations)

**Related:** Savings Goal, Compound Interest, DTI Calculator, Debt Payoff

---

## Cross-Linking Map

Every tool should link to 3-5 related tools. Use the Related section specified for each tool.

## Quality Checklist

Before saving each file, verify:
- [ ] Valid HTML5 document structure
- [ ] Links to /css/style.css
- [ ] Includes full navigation (header + mobile menu)
- [ ] Real-time calculation (no submit button)
- [ ] Numbers formatted with $ commas etc.
- [ ] JetBrains Mono for numeric outputs
- [ ] Mobile responsive (uses lw- classes that handle breakpoints)
- [ ] 500+ words of SEO content
- [ ] 5 FAQ items with accordion
- [ ] FAQ schema JSON-LD
- [ ] Related tools section with 3-5 links
- [ ] Financial disclaimer
- [ ] Footer
- [ ] NO external JS dependencies
- [ ] Smooth transitions/animations on results

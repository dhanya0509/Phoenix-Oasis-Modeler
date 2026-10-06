# 🌵 Phoenix Oasis Modeler & Scenario Comparator

An interactive, zero-dependency financial simulation engine designed to model Sonoran desert cost-of-living, accelerated debt paydown velocity, pre-tax payroll deductions, and liquidity reserve floors.

## 🔗 Live Interactive Demo

**Experience the live application:** [https://.github.io//](https://dhanya0509.github.io/Phoenix-Oasis-Modeler/)

## 📖 Overview & Motivation

Standard monthly budgets and static spreadsheets are retrospective: they describe where your money has already gone. When relocating to a new city or aggressively managing debt on an entry-to-mid career salary, you need a forward-looking cash flow simulator to stress-test financial commitments *before* signing a 12-month lease.

The **Phoenix Oasis Modeler** models real-world trade-offs across Phoenix, Arizona:

* **Rent is intertwined with climate:** In the Sonoran desert, summer electricity and air-conditioning bills can swing monthly utility costs from $\$50$ to $\$350+$.

* **Debt repayment is an active speed lever:** Committing $\$1,000$ to $\$2,000$ per month toward loan principal directly caps your daily living flexibility.

* **Pre-tax benefits change your take-home pay:** Choosing health plans and 401(k) contributions reduces your taxable base through IRS Section 125 and retirement deferrals.

## ✨ Key Features

* **Real-Time Client-Side Reactivity:** Instant recalculation across all key metrics and Chart.js visualizations upon slider movement with zero network latency.

* **Dynamic Pre-Tax and Tax Waterfall:** Simulates Section 125 pre-tax healthcare deductions, Traditional 401(k) contributions, single standard deductions ($\$14,600$), marginal federal income tax brackets, FICA ($7.65\%$), and Arizona's statutory flat tax ($2.5\%$).

* **Non-Negotiable Reserve Floor (**$\$200/\text{mo}$**):** Automatically audits cash flow against a minimum liquidity cushion before certifying any lifestyle plan as financially sound.

* **12-Month Sinking Fund Trajectory:** Models month-over-month reserve accumulation alongside discrete capital shocks, such as a mid-year travel deduction.

* **Side-by-Side Scenario Battleboard:** Employs an automated 100-point multi-factor scoring algorithm to benchmark custom user inputs against four Phoenix living archetypes.

* **Showcase Presets:** One-click presets (**⚡ Debt Crusher**, **⚖️ Valley Balanced**, **🌱 Max Saver**, **🏙️ Downtown Solo**) for immediate walkthroughs.

* **West Coast / Sonoran Design Language:** Custom aesthetic inspired by Sedona red rocks, desert gold, saguaro green, and warm linen tones, with complete dark-mode persistence.

## 🧮 Mathematical & Tax Logic

### 1. Paycheck Waterfall

Net take-home pay is determined through a sequential deduction and withholding waterfall:

$$
\text{Total Pre-Tax Deductions} = \text{Section 125 (Medical + Dental/Vision)} + \text{401(k)}
$$

1. **FICA Tax (**$7.65\%$**):** Per IRS statutes, Section 125 cafeteria plans reduce the FICA taxable base, whereas 401(k) contributions remain subject to FICA:
   

   $$
   \text{Taxable Base}_{\text{FICA}} = \max(0, \text{Gross Monthly} - \text{Section 125})
   $$

   $$
   \text{Monthly FICA} = \text{Taxable Base}_{\text{FICA}} \times 0.0765
   $$

2. **Federal Income Tax:** Evaluated using the 2024 single filer standard deduction ($\$14,600$) and statutory marginal brackets ($10\%$, $12\%$, $22\%$):
   

   $$
   \text{Taxable Base}_{\text{Fed}} = \max(0, [(\text{Gross Monthly} - \text{Total Pre-Tax}) \times 12] - \$14,600)
   $$

3. **Arizona State Income Tax:** Calculated using Arizona's statutory flat rate of $2.5\%$:
   

   $$
   \text{Monthly AZ Tax} = \frac{\text{Taxable Base}_{\text{Fed}} \times 0.025}{12}
   $$

4. **Net Take-Home Pay:**
   

   $$
   \text{Net Income} = \text{Gross Monthly} - \text{Total Pre-Tax} - (\text{FICA} + \text{Federal Tax} + \text{AZ State Tax})
   $$

### 2. Downstream Cash Flow & Outflows

Given the net monthly paycheck, downstream cash flow is partitioned into three commitments:

$$
\text{Housing Commitment} = \text{Room Rent} + \text{Utilities \& Summer A/C}
$$

$$
\text{Lifestyle Baseline} = \text{Groceries} + \text{Commute/Transit} + \text{Personal/Subscriptions}
$$

$$
\text{Total Outflows} = \text{Accelerated Loan Payment} + \text{Housing Commitment} + \text{Lifestyle Baseline}
$$

$$
\text{Monthly Net Surplus} = \text{Net Income} - \text{Total Outflows}
$$

* **Solvency Constraint:** $\text{Monthly Net Surplus} \ge \$200.00 / \text{month}$.

* **Daily Discretionary Flexibility:** $\text{Daily Allowance} = \frac{\text{Groceries} + \text{Personal}}{30}$.

### 3. Sinking Fund & 12-Month Sinking Trajectory

For each month $m \in \{1, 2, \dots, 12\}$ with a planned vacation expenditure of $C_{\text{trip}}$ at month $m_{\text{trip}}$:

$$
S_m = \sum_{k=1}^{m} \text{Monthly Surplus}_k -  \begin{cases}  C_{\text{trip}} & \text{if } m \ge m_{\text{trip}} \\ 0 & \text{if } m < m_{\text{trip}} \end{cases}
$$

Year-end accumulated bank reserve is defined as $S_{12}$.

## 🏛️ Valley Scenario Archetypes

The application continuously evaluates custom slider parameters alongside four pre-configured profiles:

| **Archetype** | **Location** | **Monthly Rent** | **Commute Strategy** | **Primary Focus** | 
| **🌵 West Valley Commuter** | Glendale / Peoria | $\$750$ | $\$220$ (I-10 gas & tolls) | Maximum bank accumulation | 
| **🚆 Tempe Transit Hub** | Near Valley Metro Rail | $\$1,050$ | $\$64$ (Light Rail pass) | Walkable, balanced debt & life | 
| **⚡ Aggressive Debt Squeeze** | Central Shared Room | $\$850$ | $\$80$ (Hybrid/short drive) | Rapid debt payoff pace | 
| **🏙️ Downtown Solo Studio** | Roosevelt Row / Downtown | $\$1,550$ | $\$40$ (Walk/Scooter) | Premium private urban lifestyle | 

## 🛠️ Tech Stack & Architecture

* **Markup & UI:** Semantic HTML5 structured for single-file deployment.

* **Styling:** [Tailwind CSS](https://tailwindcss.com/) loaded via CDN with customized desert design tokens, glassmorphism filters, and dark-mode toggles.

* **Scripting Engine:** Vanilla JavaScript (ES6+), object-oriented reactive state management, zero npm/node runtime dependencies.

* **Visual Analytics:** [Chart.js](https://www.chartjs.org/) (Doughnut breakdown, cumulative sinking fund trajectory, and scenario comparison bar charts).

* **Typography:** `Plus Jakarta Sans` for body copy, `Space Grotesk` for monospace tabular accounting.

## 🚀 Getting Started & Local Setup

Because the application is built on a zero-dependency single-file architecture, running it locally requires no build steps or package managers.

### Prerequisites

* Any modern web browser (Google Chrome, Mozilla Firefox, Safari, Microsoft Edge).

### Installation

1. **Clone the repository:**

   ```
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   
   ```

2. **Launch the application:**

   * Double-click `index.html` to open directly in your browser.

   * Or run a local HTTP server:

     ```
     # Using Python 3
     python3 -m http.server 8000
     
     ```

   * Open `http://localhost:8000` in your web browser.

## 🌐 Deploying to GitHub Pages

Deploying takes under two minutes:

1. Push `index.html` to the root of your GitHub repository.

2. Go to **Settings** → **Pages** in your repository.

3. Under **Build and deployment**:

   * **Source**: `Deploy from a branch`

   * **Branch**: `main` (or `master`), Folder: `/ (root)`

4. Click **Save**. Your site will be published at `https://<your-username>.github.io/<repo-name>/`.

## ⚖️ Legal Disclaimer

This application is created for educational, illustrative, and scenario-planning purposes only. It does not constitute certified financial, tax, or legal advice. Individual tax withholdings, Section 125 benefit eligibility, employer 401(k) matches, and payroll deductions vary based on filing status, local ordinances, and corporate benefit plans.

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

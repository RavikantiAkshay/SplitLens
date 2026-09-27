# SplitLens — Advanced Financial Visualizer & Expense Analyzer

A high-performance, privacy-first, 100% client-side web application for analyzing group expense exports (compatible with `.csv` exports from Splitwise). SplitLens transforms raw transaction logs into deep behavioral insights through interactive, mathematically rigorous, and non-redundant visualizations.

---

## Key Features & Custom Metrics Defined

### 1. Financial Persona & Behavioral Radar (5-Axis Spider Chart)
Standard expense apps only show a single number: how much someone owes or is owed. SplitLens introduces a multi-dimensional behavioral profiling engine that quantifies each member's role across 5 custom normalized dimensions (0–100% percentiles):

* **Funder Index (`Upfront Fronted vs. Consumed`)**
  * **What it is**: Measures whether a person primarily acts as the group's upfront banker/cash sponsor or relies on peers to front funds.
  * **Calculation**: $\frac{\text{Cash Fronted}}{\text{Cash Fronted} + \text{Value Consumed}} \times 100\%$
  * **Interpretation**: A score above 50% indicates a net capital sponsor (funding others upfront); a score below 50% indicates a member who primarily consumes on credit fronted by others.
* **Participation Breadth (`Outing Attendance`)**
  * **What it is**: Measures overall group social attendance and presence across activities.
  * **Calculation**: $\frac{\text{Outings Joined by Member}}{\text{Total Shared Group Outings}} \times 100\%$ (strictly excluding peer-to-peer debt settlements).
  * **Interpretation**: Identifies core regulars who attend almost every gathering versus selective or occasional guests.
* **Average Ticket Size (`Expense Magnitude`)**
  * **What it is**: Measures spending preference—whether a person shows up for high-cost milestone events or routine micro-transactions.
  * **Calculation**: Average rupee cost per outing joined ($\frac{\text{Total Cost of Attended Bills}}{\text{Bills Joined}}$), normalized as a percentile against the group's highest and lowest average spenders.
  * **Interpretation**: High scores indicate attendance concentrated in expensive dining, travel, or lodging; low scores indicate routine daily coffees, snacks, or groceries.
* **Equilibrium Score (`Debt Symmetry`)**
  * **What it is**: Measures how closely a person's payments match their consumption.
  * **Calculation**: $\left(1 - \frac{|\text{Net Balance}|}{\text{Total Cash Flow Volume}}\right) \times 100\%$
  * **Interpretation**: Near 100% indicates near-perfect symmetry (the member pays almost exactly what they consume with minimal outstanding debt). Lower scores indicate large debt or credit imbalances.
* **Network Connectivity (`Social Spread`)**
  * **What it is**: Measures integration across the entire social circle versus isolation in a sub-clique.
  * **Calculation**: $\frac{\text{Connected Peers with Active Debt Link}}{\text{Total Other Group Members}} \times 100\%$
  * **Interpretation**: High scores indicate central group connectors who share financial ties with everyone; lower scores indicate members who only interact within a narrow pair or subgroup.

#### Dynamic Archetype Classification
Based on these 5 dimensions, members are classified into clean behavioral archetypes:
* **Primary Funder**: Fronts upfront cash far in excess of consumption (>55% funder ratio).
* **Core Participant**: Attends the vast majority of group outings (>60% participation).
* **High-Ticket Participant**: High average ticket size (>70%) paired with selective attendance (≤15%).
* **Frequent Micro-Spender**: High attendance (≥35%) on small daily transactions (≤25% ticket size).
* **Balanced Payer**: Exceptional symmetry (≥88% equilibrium) with minimal debt overhang.
* **Selective Circle**: Debt and activity concentrated within a small subset of peers (≤45% connectivity).
* **Net Receiver**: Low upfront funding (≤25%) with outstanding settlement balances.
* **Standard Contributor**: Balanced attendance and spending aligned with group averages.

---

### 2. Social Dynamics & Co-Occurrence Matrix (Affinity Heatmap)
Measures real-world social interaction and sub-community patterns among members:
* **Shared Outings Count ($|A \cap B|$)**: Total number of expense transactions in which both person $A$ and person $B$ participated.
* **Joint Spend Volume**: Total cumulative rupee cost of all activities attended together.
* **Jaccard Affinity Score**: Normalized percentage overlap calculated as $\frac{|A \cap B|}{|A \cup B|} \times 100\%$. Identifies true companions who hang out together regardless of group size.
* **Greedy Affinity Clustering**: Automatically rearranges matrix rows and columns so tight-knit companion circles appear as glowing blocks along the diagonal.
* **Interactive Pair Inspector**: Drill into any pair to see their affinity tier, ranking, top shared spending categories, and largest joint receipts, with a direct shortcut to mutual debts.

---

### 3. Multi-Stage Cash Flow (Sankey / Alluvial Diagram)
Traces the end-to-end journey of group funds:
* **Stage 1 (Payers)**: Upfront cash capital deployed by each member.
* **Stage 2 (Categories)**: Expense categories funded by that capital (e.g., Dining, Groceries, Travel).
* **Stage 3 (Consumers)**: Final consumption value distributed to each member based on itemized splits.
* **Compound Dual Filtering**: Select any combination of *Person &times; Category* (e.g. *Akshay + Dining out*) to isolate exact cross-flows while dimming unrelated ribbons.
* **Category Net Balance**: Displays whether a specific member was a net funder or net consumer in that category.

---

### 4. Cumulative Cash-Flow Waves (Temporal Streamgraph)
Visualizes the chronological handoff of upfront financial responsibility:
* **Fritsch-Carlson Monotonic Splines**: Smooth organic cubic Hermite curves guaranteed with zero mathematical overshoots or gaps.
* **Triple View Mode**:
  1. *Cumulative Cash (₹)*: Running upfront funds contributed by each member across history.
  2. *Spending Pulse (Wave)*: Symmetrical streamgraph highlighting group spending surges and quiet lulls.
  3. *Funding Share (%)*: 100% normalized area chart demonstrating shifting sponsorship proportions over time.
* **Multi-Resolution & Scrubber**: Toggle between *Monthly* and *Weekly* intervals; hover to inspect period totals, largest single receipts, and payer breakdowns.

---

### 5. Outing Calendar Matrix (Chronological Activity Heatmap)
Chronological multi-year 53-week matrix (GitHub-style) uncovering temporal spending habits:
* **Dual Intensity Scales**: Toggle cell shading between *Spend Volume (₹)* and *Outing Count (Bills)* across a 5-tier emerald-to-amber ramp.
* **Day-of-Week Distribution**: 7-day breakdown (Sun–Sat) identifying recurring habits (e.g. Saturday outing concentration).
* **Streak & Density Analytics**: Measures active day density, longest consecutive spending streaks, longest quiet droughts, and weekend vs. weekday expenditure splits.
* **Day Selection**: Click any date cell to inspect the day's total spend, upfront payers, and itemized receipt breakdown.

---

### 6. Core Accounting & Ledger
* **Mutual Debts Ledger**: Bilateral debt calculation showing exactly who owes whom, for what, and on which dates.
* **Simplified Settlements Graph**: Greedy min-transaction settlement algorithm reducing multi-person debts to the minimum possible number of wire transfers.
* **Unified Accounting**: Gross cash-flow accounting reconciles across all tabs without discrepancies.

---

## 100% Privacy-First Architecture

* **Zero Server Infrastructure**: SplitLens has no backend server, database, or analytics trackers.
* **100% Local Execution**: All CSV parsing and calculations run in your browser's local memory via JavaScript and `FileReader`.
* **Zero Telemetry**: No cookies, no trackers, no external analytics, no third-party APIs. Your financial data never leaves your device.

---

## How to Run Locally

Since SplitLens is a self-contained web app, you can run it with any static web server:

```bash
# Using Node.js npx
npx http-server -p 8080 -c-1

# Using Python 3
python -m http.server 8080
```

Then open `http://localhost:8080` in any modern web browser.

---

## Deployment

SplitLens is ready for single-click deployment to:
* **GitHub Pages**: Simply push `index.html` to a GitHub repository and enable GitHub Pages under repository settings.
* **Vercel / Netlify / Cloudflare Pages**: Deploy the folder directly as a static site with zero build commands required.

---

## Legal Disclaimer & Trademark Notice

**SplitLens is an independent open-source project and is NOT affiliated with, endorsed by, sponsored by, or associated with Splitwise, Inc.**

* **"Splitwise"** is a registered trademark of Splitwise, Inc. Any references to "Splitwise" in this documentation or within the application are strictly for nominative purposes to identify file compatibility with exported `.csv` files.
* All trademarks, product names, and company names mentioned herein are the property of their respective owners.

---

## License

MIT License. See [LICENSE](LICENSE) for details.

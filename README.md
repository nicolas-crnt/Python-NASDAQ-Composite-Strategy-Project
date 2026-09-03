Automated Financial Strategy System on NASDAQCOM

Asset: NASDAQ Composite Index (NASDAQCOM)

This notebook implements a complete financial analysis pipeline: data ingestion and cleaning, visual regime identification, object-oriented portfolio analytics, statistical (OLS) analysis, an AI-generated code critique, and automated report generation.

**What it does**
Data ingestion, cleaning & merging - loads and prepares the NASDAQ Composite price history.
Visual analysis and period selection - splits the data into a bear-market period (2022) and a bull-market period (2023–2026) based on chart inspection.
Object-oriented portfolio analytics - an AdaptiveStrategy class that switches allocation posture (conservative vs. aggressive) depending on the detected regime.
Statistical analysis - OLS regression against the S&P 500 (alpha, beta, R², t-stats), plus Sharpe ratio, volatility, and max drawdown.
AI code critique - evaluates an AI-generated Sharpe ratio function and documents its flaws.
Automated report generation - outputs the full analysis as Excel and HTML reports.

**File	Description**
NASDAQCOM.csv
  Historical dates and prices for the NASDAQ Composite Index (and benchmark data used for the regression).
market_data_context.json
  Contextual metadata used by the pipeline (e.g. period labels, benchmark info). Read as input - see note below.
NASDAQCOMP_notebook.ipynb
  The pipeline described above.

**Outputs**
Running the full pipeline generates:
  NASDAQCOMP_report.xlsx - Excel report with the quantitative breakdown
  NASDAQCOMP_report.html - HTML report (executive summary, KPIs, regression table, AI critique)
  A chart image of the NASDAQ Composite price history with the two periods annotated
  Supporting .txt files documenting the period justification, benchmark justification, and AI code critique in full

**Setup**
pip install numpy pandas scipy xlsxwriter jinja2 matplotlib

**Configuration**
Key parameters set at the top of the notebook:
python
RISK_FREE_RATE = 0.0525   # US 3-month T-Bill, annualised
TRADING_DAYS   = 252      # Standard annualisation factor for US equities
PERIOD_1 = ('2022-01-01', '2022-12-31')   # Bear market (rate-hike crash)
PERIOD_2 = ('2023-01-01', '2026-01-28')   # Bull market (recovery & rally)

**Usage**
Run the notebook/script top to bottom. It will read NASDAQCOM.csv and market_data_context.json from the working directory and produce the Excel/HTML reports and supporting files listed above.

**Methodology summary**
Regime split: the NASDAQ Composite's 2021–2026 history is split into a 2022 bear market and a 2023–2026 bull market, since a single-period analysis would mask the very different risk/return profiles of each.
Benchmark: S&P 500, chosen for geographic alignment (US equities), market completeness (~80% of US equity cap), and consistency with the USD risk-free rate.
AI critique: an AI-generated Sharpe ratio function was audited and found to (1) omit the risk-free rate, (2) use a biased (population) standard deviation and (3) lack a zero-division guard - all fixed in this implementation.

**Author**
Nicolas Crichton

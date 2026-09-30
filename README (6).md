# Charity Impact and Multi Source Reporting Dashboard

I built this project to show the skills needed for a Business Intelligence Analyst role at a charity: SQL, data cleaning, data checks, dashboards, and helping non technical colleagues use data.

**Note:** All data in this project is made up (synthetic). No real people or real charity data is used.

## The problem

Charities keep their information in many places. Donations sit in one file, event attendance in another, and grant money in a finance sheet. These files are messy. The same donor can appear twice, some gifts have no amount, and some money is in dollars or euros instead of pounds.

Because of this, the leadership team cannot easily answer simple questions like:
* Are donations going up or down?
* Which campaign works best?
* Are donors coming back the next year?
* How much of our grant money have we spent?

## What I built

I made two versions of the same idea.

**Project 1: Power BI version.** The notebook cleans the data with SQL and saves tidy files. You load these into Power BI and build the dashboard. Step by step instructions are in POWERBI_GUIDE.md.

**Project 2: No Power BI version.** The same clean data feeds a web dashboard made with Python and simple web tools. It is in the docs folder and can go live on GitHub Pages for free. It has filters and click to drill down.

## The data (all synthetic)

1. Donor list from a CRM (1,240 rows)
2. Donations export (9,015 rows, from 2023 to 2025)
3. Event attendance (60 events)
4. Grants and finance sheet (25 grants)

I added realistic problems on purpose so the cleaning work is real.

## How I did it (method)

1. **Made the messy data** in Python with a fixed random seed so anyone gets the same result.
2. **Loaded it into a SQL database** (SQLite).
3. **Wrote SQL views** that clean and join the sources. The views are saved in sql/views.sql.
4. **Added data quality rules** and counted how many rows broke each rule.
5. **Checked the numbers add up** by comparing raw rows to clean rows.
6. **Built the dashboard** with donation trends, campaign performance and donor retention.
7. **Wrote a guide** so colleagues who do not know SQL can use the dashboard themselves.

## Data quality rules and what I found

* Duplicate donor IDs: 40 rows found. Kept the first row.
* Duplicate donation IDs: 15 rows found. Kept the first row.
* Missing gift amount: 84 rows found. Removed from totals.
* Missing campaign name: 152 rows found. Labelled as Unknown.
* Gifts not in pounds: 922 rows found. Converted to GBP.
* Gifts from unknown donor ID: 93 rows found. Removed from totals.
* Grants with missing spend: 3 rows found. Flagged as missing.

Of 9,015 raw gifts, 8,824 were clean and used in the dashboard. The 191 removed rows are fully explained by the rules above, so nothing disappears without a reason.

## Results

* **Total raised:** £323,539 from 8,824 gifts. The average gift was £36.67.
* **By year:** £110,689 in 2023, £103,502 in 2024 and £109,348 in 2025. Giving dipped in 2024 and recovered in 2025.
* **Best month:** December 2023 (£20,326). Giving is strongest in November and December.
* **Best campaign:** Winter Appeal raised £83,544, the most of any campaign. Gift Aid Drive was second at £63,305.
* **Weakest campaign:** Marathon Challenge raised £33,848 while its events cost £52,309, so it did not pay for itself in the first year.
* **Retention:** 41.8% of 2023 donors gave again in 2024, and 45.2% of 2024 donors gave again in 2025. More than half of donors are lost each year, so keeping donors is the biggest chance to grow.
* **Regions:** London gave the most (£105,960). Wales gave the least (£30,197).
* **Grants:** About 81% of awarded grant money has been spent where spend was recorded.
* **Data quality:** 1 in 10 gifts was in a foreign currency. Without conversion, totals would have been wrong.

Because the data is synthetic, these numbers show how the process works. They are not real charity findings.

## What I would suggest (as if this were real)

1. Focus on donor retention with thank you messages and a follow up in the first 90 days.
2. Review the cost of events for campaigns that raise less than they cost.
3. Fix data entry so campaign names and amounts are never left blank.

## How to run it

1. Open Google Colab and upload Charity_BI_Project.ipynb.
2. Click Runtime, then Run all.
3. The notebook creates the data, cleans it and builds the dashboard. It will also download a zip file of the results.


## Tools used

Python, pandas, SQL (SQLite), Power BI, Chart.js, Google Colab, GitHub Pages

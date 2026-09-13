# Insights behind the dashboard

Quick rundown of the numbers I pulled the summary from, in case anyone wants to check the math or rebuild the report.

## The basics

3,835 transactions, 19,150 units sold, total revenue of ₹76,92,04,987.97, spanning Oct 9, 2021 to Oct 8, 2024. No missing values, no duplicate transaction IDs — the source file was pretty clean going in.

## Brands

Apple edges out the field at ₹16.16 Cr, but it's close: Samsung's at ₹16.00 Cr, OnePlus at ₹15.37 Cr, Vivo at ₹15.01 Cr, and Xiaomi trails a bit at ₹14.38 Cr. Unit counts follow roughly the same order. Less than 12% separates the top and bottom brand, so there's no dominant player here — it reads more like an even five-way split.

## Cities

Delhi (₹20.39 Cr) and Mumbai (₹12.72 Cr) are well ahead of everything else. After those two it drops off fast — Ranchi, Chennai, and Rajkot are all clustered around ₹2.7–3.1 Cr, and the rest of the 29 cities trail further behind that.

## Models

Top five by revenue: iPhone SE (₹5.96 Cr), OnePlus Nord (₹5.79 Cr), Galaxy Note 20 (₹5.60 Cr), Vivo Y51 (₹5.48 Cr), Galaxy S21 (₹5.33 Cr). None of these are the newest release in their line, which is part of what made this worth calling out in the README.

## Ratings

Average comes out to 3.69/5. Breakdown: 5-star at 38.8% (1,488 transactions), 4-star at 22.0%, 3-star at 17.0%, 2-star at 14.2%, and 1-star at 8.1%. Skews positive but not lopsided.

## Payment methods

UPI leads slightly at 26.4% of transactions, then Debit Card and Credit Card essentially tied at 24.7% each, and Cash at 24.2%. Basically an even four-way split — nothing here suggests customers strongly favor one method over another.

## Day of week

Saturday and Monday bring in the most revenue; Wednesday is consistently the weakest. Worth noting: a small subset of rows in the raw `Day Name` column use abbreviations (`Mon`, `Tue`, etc.) instead of the full weekday name. It didn't affect the dashboard build since Power Query grouped on the values as given, but anyone doing a fresh groupby on the source Excel file should normalize this first (a simple `Replace Values` step in Power Query, or a mapping dict in Python).

## Demographics

Average customer age across all transactions: 38.1 years.

## How the Power BI side is put together

Revenue is a straightforward measure: `SUM(Units Sold × Price Per Unit)`. The city map uses Power BI's built-in Bing Maps geocoding on the `City` column directly — no manual lat/long needed. All four slicers (Brand, Mobile Model, City, Day Name) are synced across every visual on the page, so filtering one updates everything at once.

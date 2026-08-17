# Bhavani-A_week4_minorproject
BingePlay — Advanced SQL Analytics Project


A SQL analytics project exploring user behavior, subscription revenue, retention, and churn signals for a simulated streaming platform ("BingePlay"), using MySQL and Python (SQLAlchemy + pandas).

Overview

This project analyzes a relational dataset of ~113,000 records across 5 tables to answer 12 business questions covering revenue, engagement, retention, and churn. The focus is on writing SQL that handles real-world data issues correctly — NULLs, ties, many-to-many joins, and window function edge cases — rather than just producing a number that "looks right."



Dataset
Table	Rows	Description
users	3,000	User signups, demographics, referral source
subscriptions	4,497	Subscription plans, status, pricing, active/inactive periods
shows	100	Show metadata — category, language, rating, release year
watch_sessions	100,351	Individual viewing sessions — device, minutes watched, completion
ratings	5,000	User ratings (stars) per show
Tech Stack


MySQL — relational database
Python — SQLAlchemy + pymysql for the DB connection, pandas for result handling
Jupyter Notebook — analysis and documentation
Questions Answered
Active subscription revenue (as of a snapshot date)
Monthly signup momentum (Jan–Jun 2024)
Device-level session analytics (completion rate, avg watch time)
Rating vs. completion correlation by show category
Referral source conversion to paid subscriptions
Multi-device user identification
Q1 signups with zero watch activity
Subscription plan comparison (subscribers & watch time)
Top users ranked by total watch time (RANK())
Monthly signup running total (SUM() OVER)
Longest consecutive-day watch streaks (gaps-and-islands technique)
Churn signal detection — users with a ≥50% month-over-month drop in watch time
Key Technical Challenges
NULL handling in NOT IN — a subquery returning even one NULL silently breaks a NOT IN filter for every row; the fix is explicitly excluding NULLs in the subquery.
Window functions can't be filtered in the same WHERE clause — they're evaluated after WHERE runs, so filtering on a window function's output requires wrapping it in a CTE first.
Gaps and islands — detecting streaks of consecutive days by subtracting a ROW_NUMBER() from each date; constant results mark a single unbroken run.
Many-to-many join inflation — joining multiple one-to-many relationships back to the same table can silently multiply row counts if not handled carefully.
Repository Structure
├── bingeplay_<yourname>.ipynb   # Main analysis notebook
├── Advanced SQL Data set for MP 4.sql   # Database dump (schema + data)
└── README.md
How to Run
Set up a local MySQL instance (or use Google Colab with an in-session MySQL server).
Load the dataset:
bash



   mysql -u root -p < "Advanced SQL Data set for MP 4.sql"
Install Python dependencies:
bash


   pip install pymysql sqlalchemy pandas
Open bingeplay_<yourname>.ipynb and run all cells top to bottom.

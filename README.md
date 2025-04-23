# AtliQ Hospitality Dashboard

## Problem Statement

AtliQ Grands, a major player in the Indian hospitality industry for 20 years, is facing challenges with declining market share and revenue in the luxury/business hotel segment. This is attributed to increased competition and ineffective management decisions. To address this, the managing director aims to leverage Business and Data Intelligence to drive strategic decision-making and regain their competitive edge.

This Power BI dashboard is designed to provide the revenue management team with actionable insights from historical booking data. It helps visualize key performance indicators (KPIs), track trends, and understand performance drivers across different properties, dates, and booking platforms, ultimately enabling data-driven strategies to improve revenue and market share.

## Steps followed

-   **Step 1: Data Loading & Understanding:** Loaded the five provided CSV files (`dim_date`, `dim_hotels`, `dim_rooms`, `fact_aggregated_bookings`, `fact_bookings`) into Power BI Desktop. Reviewed the metadata to understand the structure and content of each table.
-   **Step 2: Data Cleaning & Transformation (Power Query):**
    *   Opened Power Query Editor. Used features like 'Column Distribution', 'Column Quality', and 'Column Profile' (based on the entire dataset) to inspect the data.
    *   Performed necessary cleaning steps, such as handling potential errors or inconsistencies (though specifics depend on initial data quality checks). Ensured data types were correctly assigned for calculations and relationships.
-   **Step 3: Data Modeling:**
    *   Established relationships between the tables in the Model View to create a Star Schema.
    *   `fact_bookings` and `fact_aggregated_bookings` were treated as fact tables.
    *   Dimension tables (`dim_date`, `dim_hotels`, `dim_rooms`) were linked to the fact tables using appropriate keys (e.g., `property_id`, `room_id`, `date`). This model optimizes query performance and simplifies analysis.
    *   *(See Data Model Snapshot below)*
-   **Step 4: DAX Calculations:**
    *   Created essential measures to calculate Key Performance Indicators (KPIs) crucial for hospitality revenue management:
        *   Total Revenue (`SUM(fact_bookings[revenue_realized])`)
        *   Average Daily Rate (ADR) (`[Total Revenue] / [Total Booked Room Nights]`) - *Note: Requires calculating Total Booked Room Nights first.*
        *   Occupancy % (`[Total Booked Room Nights] / [Total Capacity] * 100`) - *Note: Requires calculating Total Booked Room Nights and Total Capacity first.*
        *   Revenue Per Available Room (RevPAR) (`[Total Revenue] / [Total Capacity]`) or (`[ADR] * [Occupancy %] / 100`)
        *   Realisation % (`SUM(fact_bookings[revenue_realized]) / SUM(fact_bookings[revenue_generated]) * 100`)
        *   Daily Sellable Room Nights (DSRN) (`SUM(fact_aggregated_bookings[capacity])`)
        *   Other supporting measures as needed for specific visuals.
-   **Step 5: Report Design & Visualization:**
    *   Selected a suitable theme from the View tab for consistent branding and aesthetics.
    *   Added slicers for interactive filtering by `City`, `Room class`, `Property`, and `Date` (using `mmm yy` or `week no`).
    *   Created KPI Cards for key metrics: Revenue, RevPAR, DSRN, Occupancy %, ADR, Realisation %. Included trend indicators (Week on week change %) for context.
    *   Implemented informative Tooltips for KPI cards. For example, hovering over the 'Revenue' card shows a 'Revenue Trend by Week' line chart, differentiating between Weekday and Weekend revenue *(See Tooltip Snapshot below)*. Similar tooltips were likely created for other KPIs.
    *   Added a Donut Chart to show the 'Revenue % by category' (Luxury vs. Business).
    *   Included a Line Chart ('Trend by Key Metrics') to visualize weekly trends for RevPAR, ADR, and Occupancy %.
    *   Created a Matrix/Table ('Property by Key Metrics') to display detailed performance data for each hotel property.
    *   Added a Bar Chart to analyze 'Realisation % & ADR by Platform', showing how different booking platforms perform.
    *   Arranged visuals logically on the canvas, adding titles and formatting for clarity. Used shapes and text boxes for titles (e.g., "AtliQ Hospitality Dashboard") and sectioning if needed.

# Data Model Snapshot (Star Schema)

![Data Model View](https://github.com/user-attachments/assets/11276b28-98e8-4024-b52c-d9d8c224ca4a) 



# Snapshot of Dashboard Tooltip

![Dashboard Tooltip](https://github.com/user-attachments/assets/9fe6b824-59f7-4a3d-adaf-93c81c76e834)

# Report Snapshot (Power BI Desktop/Service)

![Dashboard](https://github.com/user-attachments/assets/be49fce5-b0f7-4f46-badf-ae936afba3f8)

# Insights

This dashboard provides several key insights for AtliQ Grands' revenue management team:

1.  **Overall Performance:** Displays total revenue generated (1.69bn), average RevPAR (7,337), Occupancy (57.8%), ADR (12.70K), and Realisation (70.1%) over the selected period (May-July 22). Trend indicators show performance relative to the previous week (e.g., +0.2% for RevPAR).

2.  **Revenue Contribution:** The donut chart highlights that 'Luxury' hotels contribute significantly more revenue (61.62%) compared to 'Business' hotels (38.38%).

3.  **Performance Trends:** The 'Trend by Key Metrics' chart shows weekly fluctuations in RevPAR, ADR, and Occupancy. This helps identify peak weeks (like Wk 27-29 showing higher ADR/RevPAR) and potential low periods requiring intervention. The 'RevPAr Trend by Week' tooltip further breaks this down, showing higher revenue generally generated on Weekends compared to Weekdays.

4.  **Property Level Insights:** The 'Property by Key Metrics' table allows for direct comparison between hotels. For instance, 'AtliQ Exotica Mumbai' generated the highest revenue (117M) and had a high RevPAR (10,629) and ADR (16,141), while 'AtliQ Seasons Delhi' had lower metrics. This helps pinpoint high and low-performing properties.

5.  **Booking Platform Analysis:** The 'Realisation % & ADR by Platform' chart reveals which booking channels yield the highest ADR and Realisation rates. For example, 'logitrip' and 'journey' show high Realisation % and ADR, while 'tripster' has lower Realisation %. This informs decisions about channel management and partnerships.

6.  **Occupancy vs. Rate Strategy:** By analyzing Occupancy % alongside ADR and RevPAR trends (weekly and by property), management can assess the effectiveness of their pricing strategies. For example, are high occupancy rates coming at the cost of lower ADR, or are they successfully maximizing RevPAR?

7.  **Cancellation Impact:** The Realisation % metric (70.1% overall) quantifies the impact of cancellations and no-shows on potential revenue. Analyzing this by property or booking platform can highlight areas needing better booking policies or follow-up.

By utilizing these insights, AtliQ Grands can make informed decisions regarding pricing, promotions, property management, and channel partnerships to improve overall revenue performance and regain market share.

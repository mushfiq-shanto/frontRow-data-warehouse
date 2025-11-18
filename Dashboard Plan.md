# **Season Pass Impact Assessment Dashboard Plan**

## **Project Context and Management Objective**

### **Background**

FrontRow is a sports ticketing solution provider partnering with **The Rebound**, a local basketball league featuring **8 teams**. These teams compete in a **round-robin format** resulting in **28 regular games**, with the top 4 progressing to a playoff round consisting of up to **3 additional games**, totalling **31 games per season**.

The standard pricing is **$5 for regular game tickets** and **$10 for playoff game tickets**. Currently, The Rebound is mid-way through its 5th season, with 9 of the 28 games completed.

Historical data from the previous 4 completed seasons show that, on average **20% to 30% of seats are empty for regular games**, while playoff tickets consistently sell out. Further analysis revealed that the audience includes a set of **dedicated fans** who typically purchase tickets for on average **4 of their favourite team's 7 regular games**.

To address this persistent capacity gap and better monetize these loyal customers, management theorized that offering a **Team-level Season Pass for $28** (a unit cost of $\mathbf{\$4}$ per game, providing a **$1 discount**) would incentivize dedicated fans to purchase the full bundle. This move is hypothesized to increase each dedicated customer's seasonal **GMV by $8** by effectively recovering a portion of the previously unsold 20% to 30% occupancy gap in regular games.

### **Management Objective**

The goal is to create a data-driven tool to assess the operational and financial impact of the Season Pass initiative for the current season, enabling management to make an informed decision to **Continue, Modify, or Discontinue** the product next season.

---

## **Dashboard Specification and Metrics**

### **Q1: Did introducing the season pass lead to extra revenue as theorized? If so, by how much?**

#### **Metrics and Logic: Measuring the Financial Gain**

Success is determined by comparing the **Current Season Total Regular GMV** against the historical baseline (Past 4 Season Average). If successful, the current GMV will be higher. We also assess the source of this gain by analyzing revenue at two levels: **GMV per Match** and **GMV per Customer**.

The hypothesis is that the Season Pass targets the **existing dedicated audience**. If this holds true, the **GMV per Customer** increase should be **higher** than the **GMV per Match** increase. If the difference is low, it suggests the Season Pass is attracting new, less-engaged audiences, which may require a strategy revision.

**Key Metrics Required:** Total Regular Season GMV, Average GMV per Match, Average GMV per Unique Customer, and Season Pass Return on Investment (ROI).

#### **Ideal Visualizations**

##### Regular Season GMV Summary (Comparison Table)
* **Purpose:** Provides a high-level comparison of financial performance against history.
* **Content:** Compares **Current Season** vs. **Past 4 Season Average** for:
    * Total Regular Season GMV
    * Average GMV per Match
    * Average GMV per Unique Customer

##### Match-by-Match GMV Performance (Line Chart)
* **Purpose:** Tracks revenue generation over time and identifies the timing of the financial surplus.
* **Content:** Two lines plotted against the chronological match sequence:
    * Current Season Match GMV (Actual value)
    * Past 4 Season Average Match GMV (Baseline)

##### Season Pass ROI (Card Visual)
* **Purpose:** A single figure summarizing the financial efficiency of the initiative.
* **Content:** Displays the ROI percentage.
    * *Calculation: Net GMV Gain (Current GMV minus Historical Average GMV) divided by the Total Estimated Lost Margin (from Q4).*

#### **Required Aggregated Tables**

##### T1. Season-Level Financials
* **Purpose:** Base data for deriving total and average GMV metrics.
* **Key Columns:**
    * `Season_ID`
    * `Total_Regular_GMV`
    * `Total_Regular_Tickets_Sold`
    * `Total_Season_Passes_Sold`
    * `Unique_Regular_Audience_Count`

##### T2. Match-Level GMV
* **Purpose:** Source data for the match-by-match trend visualization.
* **Key Columns:**
    * `Match_ID`
    * `Season_ID`
    * `Match_Date`
    * `Match_Regular_GMV`
    * `Average_GMV_Past_4_Seasons`

---

### **Q2: What portion of the previously unsold seats have been recovered?**

This measures the operational success of the Season Pass in closing the $20\%-30\%$ capacity gap.

#### Metrics and Logic: Measuring Attendance Recovery

The core measurement is the change in the **Average Occupancy Percentage** for regular games compared to historical averages. The most insightful metric is the **Recovery Percentage**, which quantifies the percentage of the historical empty seat inventory that has now been filled (Surplus Attendance divided by the Historical Gap).

* **Key Metrics Required:** Average Occupancy Percentage (Current vs. Past), and Empty Seat Recovery Percentage.

#### **Ideal Visualizations**

##### Average Regular Game Occupancy (Bar Chart / Gauge)
* **Purpose:** Provides a clear comparison of attendance efficiency.
* **Content:** A visual comparing:
    * Current Season Average Occupancy Percentage
    * Past 4 Season Average Occupancy Percentage

##### Empty Seat Recovery (Card Visual)
* **Purpose:** Highlights the operational impact in a single, quantifiable figure.
* **Content:** Displays the calculated Empty Seat Recovery Percentage.
    * *Calculation: (Current Avg Occupancy - Past Avg Occupancy) divided by (100% - Past Avg Occupancy).*

##### Match-by-Match Occupancy Trend (Line Chart)
* **Purpose:** Shows the consistency of attendance improvement across the season.
* **Content:** Plots the Occupancy Percentage for every match played in the current season.

#### **Required Aggregated Tables**

##### T3. Match-Level Attendance & Occupancy
* **Purpose:** To calculate and track occupancy rates for all regular games across all seasons.
* **Key Columns:**
    * `Match_ID`
    * `Season_ID`
    * `Total_Capacity`
    * `Tickets_Sold_Incl_Passes`
    * `Occupancy_Percent`

---

### **Q3: What is the season pass penetration rate among dedicated fans and overall audience?**

This assesses the success of the Season Pass in reaching its target market (dedicated fans).

#### **Metrics and Logic: Measuring Customer Adoption**

**Dedicated Fans** are defined as those purchasing $\ge 4$ regular tickets historically. The primary metric is the **Dedicated Fan Penetration Rate**: the proportion of this core audience that purchased a Season Pass. We also measure the **Overall Audience Penetration Rate** for context on general market acceptance.

* **Key Metrics Required:** Dedicated Fan Penetration Rate, Overall Audience Penetration Rate.

#### **Ideal Visualizations**

##### Dedicated Fan Penetration Rate (Donut Chart)
* **Purpose:** Shows the adoption success within the core target segment.
* **Content:** Distribution of:
    * Percentage of Dedicated Fans who bought the Pass
    * Percentage of Dedicated Fans who did not

##### Overall Audience Adoption (Donut Chart)
* **Purpose:** Shows the overall market penetration of the product.
* **Content:** Distribution of the Total Unique Audience:
    * Percentage who bought the Pass
    * Percentage who bought Single Tickets Only

#### **Required Aggregated Tables**

##### T4. Customer-Level Season Pass Adoption
* **Purpose:** To identify dedicated fans and track their current Season Pass purchase behavior.
* **Key Columns:**
    * `Customer_ID`
    * `Total_Regular_Tickets_Purchased_Last_Season`
    * `Is_Dedicated_Fan` (Boolean Flag for $\ge 4$ tickets)
    * `Has_Season_Pass_Current_Season` (Boolean Flag)

---

### **Q4: How much has the Season Pass sales cannibalized on regular ticket sales?**

This assesses the financial risk of margin sacrifice caused by discounting the tickets (full price $\$5$ vs. pass unit price $\$4$).

#### **Metrics and Logic: Measuring Lost Margin**

Cannibalization is the maximum potential margin lost on customers who would have bought single tickets at full price but chose the discounted pass instead. We quantify this by estimating the **Total Lost Margin** on Season Pass sales. We also track the **Cannibalization Quantity** (tickets) by comparing the current year's *single ticket sales only* against the historical total average.

* **Key Metrics Required:** Estimated Lost Margin (Monetary Value) and Cannibalization Quantity (Tickets).

#### **Ideal Visualizations**

##### Estimated Lost Margin (Cannibalization) (Card Visual)
* **Purpose:** Quantifies the maximum financial cost of the discount strategy.
* **Content:** Displays the total monetary value of the lost margin.
    * *Calculation: Total Season Passes Sold multiplied by 7 Games multiplied by the $\$1$ discount.*

##### Single Ticket Sales Volume (Comparison Table)
* **Purpose:** Contextualizes the lost margin by showing the ticket volume displacement.
* **Content:** Compares:
    * Current Season Single Tickets Sold (excluding pass units)
    * Past 4 Season Average Total Tickets Sold

#### **Required Aggregated Tables**

##### T1. Season-Level Financials
* **Purpose:** Reused from Q1 to extract total Season Pass sales for margin calculation.
* **Key Columns:** (See Section 2.1.3.1)
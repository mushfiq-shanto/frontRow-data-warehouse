# **Season Pass Impact Assessment Dashboard Plan**

## **Project Context and Management Objective**

### **Background**

FrontRow is a sports ticketing solution provider partnering with **The Rebound**, a local basketball league featuring **8 teams**. These teams compete in a **round-robin format** resulting in **28 regular games**, with the top 4 progressing to a playoff round consisting of up to **3 additional games**, totalling **31 games per season**.

The standard pricing is **$5 for regular game tickets** and **$10 for playoff game tickets**. Currently, The Rebound is mid-way through its 5th season, with 9 of the 28 games completed.

Historical data from the previous 4 completed seasons show that, on average **20% to 30% of seats are empty for regular games**, while playoff tickets consistently sell out. Further analysis revealed that the audience includes a set of **dedicated fans** who typically purchase tickets for on average **4 of their favourite team's 7 regular games**.

To address this persistent capacity gap and better monetize these loyal customers, management theorized that offering a **Team-level Season Pass for $28** (a unit cost of $4 per game, providing a **$1 discount**) would incentivize dedicated fans to purchase the full bundle. This move is hypothesized to increase each dedicated customer's seasonal **GMV by $8** by effectively recovering a portion of the previously unsold 20% to 30% occupancy gap in regular games.

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

##### Average Regular Game Occupancy
* **Purpose:** Provides a clear comparison of attendance efficiency.
* **Content:** A visual comparing:
    * Current Season Average Occupancy Percentage
    * Past 4 Season Average Occupancy Percentage

##### Empty Seat Recovery
* **Purpose:** Highlights the operational impact in a single, quantifiable figure.
* **Content:** Displays the calculated Empty Seat Recovery Percentage.
    * *Calculation: (Current Avg Occupancy - Past Avg Occupancy) divided by (100% - Past Avg Occupancy).*

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

##### Dedicated Fan Penetration Rate
* **Purpose:** Shows the adoption success within the core target segment.
* **Content:** Distribution of:
    * Percentage of Dedicated Fans who bought the Pass
    * Percentage of Dedicated Fans who did not

##### Overall Audience Adoption
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
    * `Is_Dedicated_Fan`
    * `Has_Season_Pass_Current_Season`

---

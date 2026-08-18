#  FedEx Logistics Supply Chain Analysis

### Exploratory Data Analysis | Supply Chain Analytics | Logistics Performance

> An end-to-end exploratory data analysis project focused on understanding shipment performance, delivery efficiency, transportation costs, vendor dependency, processing times, and operational bottlenecks across a global pharmaceutical supply chain.

---

##  Project Overview

Supply chain operations involve multiple interconnected factors such as transportation modes, suppliers, manufacturing locations, shipment values, delivery schedules, processing times, and destination countries.

In this project, I analyzed the **FedEx Supply Chain Management (SCMS) Delivery History dataset** to understand how these factors influence logistics performance and operational efficiency.

The analysis focuses on answering practical business questions such as:

* Which transportation modes are used most frequently?
* How well does each shipment mode perform in terms of delivery delays?
* Which transportation methods have the highest freight costs?
* Which countries receive the highest shipment value?
* Which countries experience the longest processing times?
* Which vendors contribute the highest shipment value?
* Is the supply chain dependent on a small number of vendors or manufacturing sites?
* How does freight cost relate to shipment value?
* Are delivery delays primarily related to shipment size and cost?
* Are there seasonal patterns in shipment volumes?
* Where are the major operational bottlenecks and cost-optimization opportunities?

The goal was not only to explore the dataset but also to translate the analysis into **actionable business insights and supply-chain recommendations**.

---

##  Business Objective

The primary objective of this project is to analyze global pharmaceutical shipment operations and identify patterns affecting:

*  Transportation efficiency
*  Delivery performance
*  Freight and shipment costs
*  Manufacturing and supplier dependency
*  Country-level logistics performance
*  Shipment volume and demand patterns
*  Order processing efficiency

The analysis ultimately aims to identify operational bottlenecks and areas where logistics planning, supplier management, and transportation decisions can be improved.

---

##  Dataset

The dataset contains historical shipment and delivery information from the Supply Chain Management System (SCMS).

### Dataset Size

* **Rows:** 10,324
* **Columns:** 33
* **Project Type:** Exploratory Data Analysis (EDA)

The dataset contains information related to:

* Shipment identification
* Countries
* Vendors
* Manufacturing sites
* Shipment modes
* Delivery dates
* Product groups
* Shipment quantities
* Shipment values
* Pack and unit prices
* Weight
* Freight costs
* Insurance costs
* Vendor agreements

Some important variables include:

`Country`, `Shipment Mode`, `Vendor`, `Product Group`, `Manufacturing Site`, `Line Item Quantity`, `Line Item Value`, `Freight Cost (USD)`, `Weight (Kilograms)`, `Scheduled Delivery Date`, and `Delivered to Client Date`.

---

##  Tools & Technologies

### Programming & Data Analysis

* **Python**
* **Pandas**
* **NumPy**

### Data Visualization

* **Matplotlib**
* **Seaborn**
* **Plotly**

### Development Environment

* **Google Colab**
* **Jupyter Notebook**

---

##  Project Workflow

```text
Raw Dataset
     ↓
Data Understanding
     ↓
Data Cleaning
     ↓
Missing Value Analysis
     ↓
Data Type Conversion
     ↓
Feature Engineering
     ↓
Exploratory Data Analysis
     ↓
Business Analysis
     ↓
Key Insights
     ↓
Business Recommendations
```

---

#  Data Loading & Initial Exploration

I started by loading the raw SCMS delivery history dataset using Pandas and performed an initial assessment of the dataset structure.

The first step was to understand:

* Dataset dimensions
* Column names
* Data types
* Missing values
* Duplicate records
* Numerical distributions
* Categorical variables

The dataset contains **10,324 records across 33 columns**.

I also used descriptive statistics to understand the distribution of numerical variables such as:

* Line Item Quantity
* Line Item Value
* Pack Price
* Unit Price
* Unit of Measure

---

# 2️ Data Quality & Cleaning

Before performing the analysis, I examined the dataset for common data-quality issues.

### Duplicate Records

I checked for duplicate rows and found:

```text
Duplicate Rows = 0
```

This meant that no duplicate records needed to be removed.

### Missing Values

Missing-value analysis was performed using:

```python
df.isnull().sum()
```

and missing-value percentages were calculated to understand the extent of missing information across columns.

Several variables contained missing values, particularly operational fields such as:

* Shipment Mode
* Dosage
* Weight
* Freight Cost
* Insurance

---

##  Data Type Conversion

The date columns were originally stored as objects, so I converted them into proper datetime format.

The following columns were converted:

* PQ First Sent to Client Date
* PO Sent to Vendor Date
* Scheduled Delivery Date
* Delivered to Client Date
* Delivery Recorded Date

This allowed me to perform date-based calculations and time-series analysis.

---

##  Shipment Mode Cleaning

Missing shipment modes were replaced with:

```text
Unknown
```

This allowed missing records to remain part of the analysis instead of being silently removed.

---

##  Weight & Freight Cost Conversion

The `Weight (Kilograms)` and `Freight Cost (USD)` columns contained both numerical values and text entries such as:

* `"Weight Captured Separately"`
* `"Freight Included in Commodity Cost"`
* `"Invoiced Separately"`
* References to ASN records

## These columns were therefore converted to numeric values using coercion, allowing invalid/non-numeric entries to become missing values and preventing them from interfering with numerical analysis.

# 3️ Feature Engineering

To make the dataset more useful for business analysis, I created several derived features.

###  Delivery Delay

I calculated:

```text
Delivery Delay = Actual Delivery Date - Scheduled Delivery Date
```

This allowed shipments to be classified based on whether they were delivered before, on, or after the scheduled date.

---

###  Processing Time

I calculated the time between the purchase order being sent to the vendor and the scheduled delivery date.

```text
Processing Time =
Scheduled Delivery Date - PO Sent to Vendor Date
```

This metric helps identify countries or operations where the supply chain takes longer to process orders.

---

###  Delivery Status

I created a categorical variable:

```text
On Time
Delayed
```

Shipments with zero or negative delivery delay were classified as **On Time**, while positive delays were treated as delayed deliveries.

---

###  Time-Based Features

I also extracted:

* Delivery Month
* Delivery Year

These features enabled monthly and yearly shipment trend analysis.

---

#  Exploratory Data Analysis

The EDA phase focused on understanding shipment patterns, transportation performance, costs, geographic concentration, suppliers, and operational efficiency.

---

##  Shipment Mode Analysis

Air transportation is the dominant shipment mode in the dataset, followed by Truck.

Air Charter and Ocean shipments represent much smaller volumes.

### Business Insight

Because Air handles a large proportion of shipments, improvements in air logistics can have a significant impact on overall supply-chain performance.

At the same time, some non-urgent shipments could potentially be evaluated for lower-cost transportation alternatives where delivery requirements allow.

---

##  Top Destination Countries by Shipment Volume

The analysis of destination countries showed that shipment activity is concentrated in a relatively small number of countries.

**South Africa** receives the highest shipment volume, followed by countries such as **Nigeria and Côte d'Ivoire**.

### Business Insight

High-volume markets should receive greater attention when allocating:

* Transportation capacity
* Warehouse resources
* Procurement resources
* Vendor support

Even small efficiency improvements in high-volume markets can have a meaningful impact on overall operations.

---

#  Delivery Performance Analysis

Delivery performance is one of the most important parts of this project.

The distribution of delivery delays shows that many shipments are delivered close to their scheduled dates, while a smaller number experience significant delays.

Overall, the majority of shipments are classified as **On Time**, while delayed shipments represent a smaller proportion.

### Why this matters

Instead of simply calculating the average delivery time, I analyzed delivery status and delay patterns to identify where operational problems may exist.

Potential causes of delayed shipments could include:

* Transportation issues
* Customs processes
* Supplier-related problems
* Scheduling issues
* Regional operational bottlenecks

---

#  Transportation Cost Analysis

Freight cost analysis showed a strongly right-skewed distribution.

Most shipments have relatively low freight costs, while a smaller number of shipments have exceptionally high transportation expenses.

This suggests that high-cost shipments should be investigated individually to determine whether the cost is driven by:

* Shipment mode
* Destination
* Urgency
* Shipment characteristics
* Transportation constraints

---

##  Average Freight Cost by Shipment Mode

The comparison of average freight costs across transportation modes revealed that:

* **Air Charter** has the highest average freight cost.
* **Ocean** is the second-highest.
* **Air and Truck** have relatively similar average freight costs.

### Business Recommendation

Air Charter should primarily be used for situations where urgency justifies the additional transportation cost.

For routine shipments, transportation planning should consider the trade-off between:

```text
Cost ↔ Speed ↔ Reliability
```

---

#  Delivery Delay by Transportation Mode

I compared average delivery delay across shipment modes to understand which transportation methods perform better.

The analysis found:

* Ocean shipments have the highest average positive delay.
* Air and Air Charter generally arrive earlier than scheduled.
* Truck shipments also perform relatively well.

### Business Recommendation

Transportation mode should be selected based on shipment urgency and required service levels.

For urgent shipments, faster modes may justify their additional cost.

Ocean shipments with recurring delays should be investigated for potential issues such as:

* Customs clearance
* Port congestion
* Scheduling
* Transit planning

---

#  Shipment Value Analysis

The shipment value distribution is highly right-skewed.

Most shipments have relatively low values, while a small number represent extremely high-value orders reaching several million USD.

### Business Implication

High-value shipments require greater attention because they create higher financial exposure.

Potential actions include:

* Additional shipment monitoring
* Better insurance planning
* Premium logistics services where justified
* Additional risk controls

---

#  Geographic Shipment Value Analysis

The country-level shipment value analysis identified **Nigeria** as the country with the highest total shipment value, followed by **Zambia and Mozambique**.

The analysis also showed that a significant share of high-value shipments is concentrated in African markets.

### Business Implication

High-value markets should receive greater attention during:

* Inventory planning
* Logistics capacity planning
* Risk management
* Supply-chain expansion

Concentration in a small number of markets also creates potential financial exposure if disruptions occur.

---

#  Processing Time Analysis

Processing time was analyzed to identify countries where shipments take longer to move through the supply-chain process.

The analysis found that **Pakistan** has the highest average processing time, followed by **Guatemala and Afghanistan**.

### Business Implication

Countries with unusually high processing times should be investigated for potential:

* Administrative delays
* Customs procedures
* Documentation issues
* Warehouse inefficiencies
* Supplier-related delays

Reducing processing time can improve delivery speed while potentially reducing inventory holding costs.

---

#  Vendor Analysis

Vendor concentration was another important area of the analysis.

The analysis found that **SCMS from RDC** contributes an exceptionally large share of total shipment value compared with other vendors.

### Key Risk

High dependence on a limited number of suppliers creates supply-chain concentration risk.

If a major supplier experiences:

* Production problems
* Quality issues
* Transportation disruptions
* Capacity constraints

the impact on the overall supply chain could be significant.

### Recommendation

Supplier diversification should be considered to improve:

* Supply-chain resilience
* Negotiation power
* Continuity of supply
* Risk management

---

#  Manufacturing Site Analysis

The analysis of manufacturing locations showed that **Aurobindo Unit III, India** is the largest manufacturing site in terms of shipment contribution.

Other major manufacturing sites include:

* Mylan
* Hetero
* Cipla

Many of the major manufacturing locations are concentrated in India.

### Business Implication

Heavy dependence on a limited number of manufacturing locations can create concentration risk.

Diversifying production locations can improve supply-chain resilience.

---

#  Shipment Trends Over Time

I analyzed shipment volumes across years to understand long-term demand patterns.

Shipment activity increased significantly during the earlier years, with peak shipment activity occurring around **2014**. A decline appears in the final year, although this may be related to incomplete data rather than an actual business decline.

### Business Implication

Historical shipment trends can support:

* Capacity planning
* Transportation planning
* Procurement planning
* Warehouse resource allocation

---

#  Monthly Seasonality

Monthly analysis showed noticeable variation in shipment activity.

**August** records the highest shipment activity, while **January and December** have comparatively lower shipment volumes.

### Business Recommendation

Supply-chain resources can be planned around seasonal demand.

Before high-volume periods, organizations can prepare:

* Transportation capacity
* Workforce
* Inventory
* Procurement requirements

---

#  Freight Cost vs Shipment Value

I used a scatter plot to investigate the relationship between shipment value and freight cost.

The analysis showed that:

* Most shipments have relatively low shipment values and moderate freight costs.
* Freight cost increases with shipment value only to a certain extent.
* Shipments with similar values can have significantly different freight costs.
* Some shipments have unusually high freight costs despite moderate shipment values.

### Key Takeaway

Shipment value alone does not fully explain transportation cost.

Other factors such as:

* Destination
* Shipment mode
* Urgency
* Route
* Operational constraints

may influence freight expenses.

This creates an opportunity for deeper cost optimization analysis.

---

#  Delivery Performance Across Shipment Modes

I compared delivery status across transportation modes.

The analysis indicates that:

* Air handles the largest shipment volume and maintains strong delivery performance.
* Truck also performs well.
* Air Charter has a higher proportion of delayed shipments despite its smaller volume.
* Ocean has relatively low shipment volume.

### Business Takeaway

For routine operations, Air and Truck appear to provide a strong combination of volume and delivery reliability.

Air Charter should be used selectively when the urgency of a shipment justifies the higher cost and operational variability.

---

#  Correlation Analysis

I created a correlation heatmap using key numerical variables including:

* Line Item Quantity
* Line Item Value
* Freight Cost
* Weight
* Delivery Delay
* Processing Time
* Unit Price
* Pack Price

The analysis found a strong positive correlation of approximately **0.84 between Line Item Quantity and Line Item Value**.

Freight cost showed only a moderate relationship with shipment value and weight.

More importantly, **Delivery Delay showed almost no correlation with freight cost, shipment value, or quantity**.

### Business Interpretation

This suggests that delivery delays are likely influenced more by operational factors than simply by shipment size or transportation expenditure.

Therefore, simply spending more on transportation may not solve delivery-delay problems.

Instead, organizations should investigate:

* Supplier coordination
* Scheduling
* Customs
* Processing bottlenecks
* Transportation planning
* Regional operational issues

---

#  Key Business Insights

Based on the complete analysis, the major findings are:

### 1. Air dominates transportation

Air transportation handles the majority of shipments while maintaining strong delivery performance.

### 2. Most shipments are delivered on time

Overall delivery performance appears strong, although a smaller group of delayed shipments requires further investigation.

### 3. Transportation mode affects cost and delivery performance

Air Charter is expensive, while Ocean shows higher average delivery delays.

### 4. Shipment value is geographically concentrated

Nigeria and several African countries account for substantial shipment value.

### 5. Supplier concentration is a potential risk

A small number of vendors contribute a large proportion of shipment value.

### 6. Processing efficiency varies by country

Pakistan, Guatemala, and Afghanistan show relatively high average processing times.

### 7. Shipment demand is seasonal

August shows particularly high shipment activity.

### 8. Shipment value does not fully explain freight cost

Freight cost varies significantly even among shipments with similar values.

### 9. Delivery delays are not strongly associated with shipment size

The correlation analysis suggests that operational factors are more important potential drivers of delays.

---

#  Business Recommendations

Based on the findings, I would recommend the following actions:

###  1. Optimize Transportation Mode Selection

Use Air and Truck strategically for time-sensitive shipments while evaluating lower-cost options for shipments where delivery urgency is lower.

###  2. Investigate High-Cost Shipments

Analyze freight-cost outliers to identify expensive routes, transportation choices, or operational circumstances.

###  3. Investigate Processing Bottlenecks

Countries with high processing times should be reviewed for administrative, customs, supplier, and warehouse-related delays.

###  4. Reduce Supplier Concentration Risk

Diversifying suppliers can improve resilience and reduce dependency on a small number of vendors.

###  5. Prioritize High-Value Markets

Countries receiving high-value shipments should receive greater attention in logistics planning and risk management.

###  6. Plan for Seasonal Demand

Higher shipment volumes during peak months should be incorporated into procurement, workforce, inventory, and transportation planning.

###  7. Improve Operational Data Quality

Missing shipment modes and non-standard entries in fields such as weight and freight cost indicate opportunities for better operational data collection and reporting.

---

#  Key Visualizations

The following visualizations summarize the most important findings from the project:

###  Delivery Performance by Shipment Mode

`![Delivery Status by Shipment Mode](images/delivery_status_by_mode.png)`

###  Average Freight Cost by Shipment Mode

`![Average Freight Cost by Shipment Mode](images/average_freight_cost_by_mode.png)`

###  Average Delivery Delay by Shipment Mode

`![Average Delivery Delay by Shipment Mode](images/average_delivery_delay_by_mode.png)`

###  Top Countries by Shipment Value

`![Top Countries by Shipment Value](images/top_countries_by_shipment_value.png)`

###  Top Vendors by Shipment Value

`![Top Vendors by Shipment Value](images/top_vendors_by_shipment_value.png)`

###  Countries with Highest Processing Time

`![Processing Time by Country](images/processing_time_by_country.png)`

###  Correlation Heatmap

`![Correlation Heatmap](images/correlation_heatmap.png)`

---

#  Technical Skills Demonstrated

Through this project, I applied the following skills:

### Python

* Data loading
* Data manipulation
* Conditional logic
* Feature engineering
* Date/time manipulation

### Pandas

* DataFrame operations
* Missing-value analysis
* GroupBy
* Aggregation
* Sorting
* Filtering
* Datetime operations
* Feature creation

### NumPy

* Numerical operations
* Conditional transformations
* Array-based calculations

### Data Visualization

* Matplotlib
* Seaborn
* Plotly
* Bar charts
* Count plots
* Histograms
* Line charts
* Scatter plots
* Correlation heatmaps

### Analytical Skills

* Exploratory Data Analysis
* Data cleaning
* Missing-value treatment
* Trend analysis
* Distribution analysis
* Correlation analysis
* Outlier identification
* Business interpretation
* Supply-chain analysis

---

#  What I Learned

This project helped me understand that effective data analysis is not only about creating visualizations.

The important part is connecting the analysis to a business problem.

For example, instead of simply identifying that Air is the most common shipment mode, I looked at its relationship with **cost and delivery performance**.

Similarly, instead of only calculating shipment volumes by country, I analyzed **shipment value and processing time** to identify potential operational and financial risks.

The project strengthened my ability to move from:

```text
Raw Data
    ↓
Cleaning
    ↓
Analysis
    ↓
Pattern Identification
    ↓
Business Insight
    ↓
Recommendation
```

---

#  Limitations

There are some limitations to this analysis.

### 1. Historical Dataset

The analysis is based on historical delivery records, so the findings may not represent current logistics operations.

### 2. Missing Operational Data

Some fields such as weight and freight cost contain missing or non-standard values.

### 3. Correlation ≠ Causation

The correlation analysis identifies relationships between variables but does not prove causal relationships.

### 4. Final-Year Shipment Volume

The decline observed in the final year may be related to incomplete data rather than an actual decline in operations.

---

#  Future Improvements

This project can be extended beyond exploratory analysis.

### Predictive Analytics

Develop a machine-learning model to predict:

* Delivery delays
* Freight costs
* Processing time

### Delay Risk Prediction

Create a classification model that predicts whether a shipment is likely to be delayed.

### Freight Cost Prediction

Build a regression model using:

* Shipment mode
* Weight
* Shipment value
* Destination
* Vendor
* Product group

to estimate expected freight costs.

### Interactive Dashboard

Build a **Power BI dashboard** containing:

* Shipment KPIs
* Delivery performance
* Transportation costs
* Vendor analysis
* Country analysis
* Monthly trends
* Delay analysis

### Supply Chain Risk Score

Develop a risk-scoring framework based on:

* Vendor concentration
* Manufacturing concentration
* Processing time
* Delivery delays
* Shipment value

---

#  Project Structure

```text
fedex-logistics-supply-chain-analysis/
│
├──  FedEx_Logistics_Supply_Chain_Analysis.ipynb
│
├──  data/
│   └── scms_delivery_history_raw.csv
│
├──  images/
│   ├── delivery_status_by_mode.png
│   ├── average_freight_cost_by_mode.png
│   ├── average_delivery_delay_by_mode.png
│   ├── top_countries_by_shipment_value.png
│   ├── top_vendors_by_shipment_value.png
│   ├── processing_time_by_country.png
│   └── correlation_heatmap.png
│
└──  README.md
```

---

#  How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/sakshi200-code/fedex-logistics-supply-chain-analysis.git
```

### 2. Navigate to the project

```bash
cd fedex-logistics-supply-chain-analysis
```

### 3. Install required libraries

```bash
pip install pandas numpy matplotlib seaborn plotly
```

### 4. Open the notebook

```bash
jupyter notebook
```

Alternatively, the notebook can be opened directly using **Google Colab**.

---

#  Project Highlights

| Area                | Analysis                                         |
| ------------------- | ------------------------------------------------ |
| Dataset             | 10,324 records, 33 columns                       |
| Data Cleaning       | Missing values, duplicates, data types           |
| Feature Engineering | Delivery Delay, Processing Time, Delivery Status |
| Transportation      | Shipment mode analysis                           |
| Cost                | Freight cost analysis                            |
| Geography           | Country-level shipment analysis                  |
| Vendors             | Vendor concentration analysis                    |
| Manufacturing       | Manufacturing-site analysis                      |
| Time Series         | Yearly and monthly shipment trends               |
| Performance         | Delivery delay and on-time analysis              |
| Statistics          | Correlation analysis                             |
| Visualization       | Matplotlib, Seaborn, Plotly                      |
| Business Output     | Recommendations and operational insights         |

---

#  Conclusion

This project provided an end-to-end analysis of pharmaceutical supply-chain operations using historical shipment data.

The analysis identified important patterns in **transportation mode usage, delivery performance, freight costs, shipment value, supplier concentration, country-level processing time, and seasonal shipment activity**.

One of the most important conclusions is that supply-chain performance cannot be evaluated using a single metric. A transportation mode may be fast but expensive, a supplier may handle high shipment value but create concentration risk, and a shipment may have a high value without necessarily having a proportionally high freight cost.

Therefore, effective supply-chain decision-making requires looking at **cost, speed, reliability, geography, suppliers, and operational processes together**.

This project demonstrates my ability to take a raw business dataset, clean and transform it, perform exploratory analysis, identify meaningful patterns, and translate those findings into **business-oriented recommendations**.

---

#  Author

### Sakshi Chore

**Aspiring Data Analyst | Data Science Enthusiast**

Skills:

`Python` • `SQL` • `Pandas` • `NumPy` • `Power BI` • `Excel` • `Data Visualization` • `Machine Learning`

### GitHub

[GitHub – sakshi200-code](https://github.com/sakshi200-code)

### Project Repository

[FedEx Logistics Supply Chain Analysis](https://github.com/sakshi200-code/fedex-logistics-supply-chain-analysis)

---

 **If you found this project interesting, feel free to explore the notebook and analysis.**


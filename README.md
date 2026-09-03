# 🚆 Railway Ticket Confirmation Analysis

## 📌 Project Overview

This project analyzes a **Railway Ticket Confirmation** dataset to understand booking behavior, ticket confirmation patterns, waitlisting, travel demand, and seat availability.

The goal was not just to calculate numbers, but to follow a practical **Data Analyst workflow**:

> **Raw Data → Data Cleaning → Feature Engineering → Exploratory Data Analysis → Business Insights**

The analysis was performed using **Python, Pandas, NumPy, Matplotlib, and Seaborn**.

---

## 🎯 Why I Did This Project

Railway booking data contains several factors that can influence the booking and confirmation experience, such as:

- Travel class
- Booking quota
- Booking channel
- Booking lead time
- Waitlist position
- Journey date
- Route
- Train
- Travel distance
- Seat availability
- Peak-season travel
- Passenger group size

I wanted to use these fields to answer practical business questions such as:

- How many bookings and passengers are represented?
- What percentage of bookings are confirmed?
- Does travel class show different confirmation patterns?
- Does quota affect confirmation?
- Do booking channels show different confirmation rates?
- Does booking earlier relate to confirmation?
- How does waitlisting relate to confirmation?
- Does peak season affect confirmation?
- When is journey demand highest?
- Which routes and trains receive the most bookings?
- Which trains have low average seat availability?

This makes the project closer to a real **business-oriented data analysis project** rather than only a dataset-cleaning exercise.

---

## 📊 Dataset

The original dataset contains:

- **30,000 bookings**
- **21 columns**
- **90,181 passengers** represented across the bookings

### Main columns

| Column | Description |
|---|---|
| `PNR Number` | Unique booking/PNR identifier |
| `Train Number` | Train identifier |
| `Date of Journey` | Passenger journey date |
| `Class of Travel` | Travel class such as 1AC, 2AC, 3AC, Sleeper |
| `Quota` | Booking quota |
| `Source Station` | Starting station |
| `Destination Station` | Destination station |
| `Booking Date` | Date on which the booking was made |
| `Current Status` | Current booking status |
| `Number of Passengers` | Number of passengers in the booking |
| `Age of Passengers` | Passenger age category |
| `Booking Channel` | Channel used for booking |
| `Travel Distance` | Journey distance |
| `Number of Stations` | Number of stations in the journey |
| `Travel Time` | Travel duration |
| `Train Type` | Type of train |
| `Seat Availability` | Available seats |
| `Special Considerations` | Passenger-specific consideration |
| `Holiday or Peak Season` | Whether the journey falls in a peak/holiday period |
| `Waitlist Position` | Waitlist position when applicable |
| `Confirmation Status` | Final confirmation outcome |

---

# 🔄 Project Workflow

## 1. Data Cleaning

The first notebook focuses on understanding and preparing the raw dataset before analysis.

### Initial checks

I started by checking:

- Dataset shape
- Column names
- Data types
- Summary statistics
- Missing values
- Duplicate records
- PNR uniqueness
- Invalid numeric values
- Categorical value distributions

### Missing values

Two columns contained missing values:

- `Special Considerations` → **9,955 missing values**
- `Waitlist Position` → **19,947 missing values**

Instead of blindly deleting these rows, I interpreted the meaning of the missing values.

#### Special Considerations

A missing value was treated as:

`No Special Consideration`

This preserves the booking instead of unnecessarily removing valid records.

#### Waitlist Position

A missing waitlist position indicates that the passenger was not waitlisted.

Two fields were therefore created/used:

- `Was Waitlisted` → Boolean indicator
- `Waitlist Position` → converted into a numeric value, with non-waitlisted bookings represented as `0`

The original dataframe was copied before cleaning so that the raw dataset remained unchanged during the transformation process.

### Duplicate check

No duplicate rows were found in the dataset.

The `PNR Number` field was also checked for uniqueness.

### Data type conversion

The following date columns were converted from strings to datetime:

- `Date of Journey`
- `Booking Date`

This allows date-based calculations and analysis.

### Data validation

I also checked important numeric columns for invalid values, including:

- Number of Passengers
- Travel Distance
- Number of Stations
- Travel Time
- Seat Availability

Categorical columns were also reviewed using value counts to understand their available categories.

---

# 🧩 2. Feature Engineering

After cleaning the dataset, I created additional variables to make the data more useful for analysis.

### Booking Lead Time

```text
Booking Lead Time = Date of Journey - Booking Date
```

This represents how many days before the journey the booking was made.

### Waitlist Number

The numeric portion of the waitlist position was extracted.

For example:

```text
WL097 → 97
WL011 → 11
```

This makes waitlist positions easier to analyze numerically.

### Route

A new route field was created:

```text
Source Station → Destination Station
```

Example:

```text
NDLS->CSMT
```

This allows route-level demand analysis.

### Journey Month

The month was extracted from the journey date to identify monthly demand patterns.

### Journey Day

The day of the week was extracted to understand demand by weekday.

### Journey Year

The journey year was extracted for time-based analysis.

### Waitlist Category

Waitlist positions were grouped into meaningful categories:

| Category | Range |
|---|---|
| `No WL` | No waitlist |
| `WL 1-10` | 1–10 |
| `WL 11-50` | 11–50 |
| `WL 51-100` | 51–100 |
| `WL 100+` | Above 100 |

### Booking Lead-Time Category

Booking lead time was grouped into:

| Category | Range |
|---|---|
| `Last Minute` | 0–1 days |
| `2-7 Days` | 2–7 days |
| `8-30 Days` | 8–30 days |
| `31-90 Days` | 31–90 days |
| `90+ Days` | More than 90 days |

### Distance Category

Travel distance was grouped into:

- Short
- Medium
- Long
- Very Long

### Passenger Group Size

Bookings were grouped according to passenger count:

- 1 Passenger
- 2 Passengers
- 3–4 Passengers
- 5+ Passengers

These engineered features make the dataset easier to analyze from a business perspective.

---

# 🔎 3. Exploratory Data Analysis

The EDA stage focuses on answering business questions rather than simply generating charts.

## Key Questions Analyzed

### 1. How many bookings do we have?

**30,000 bookings**

### 2. How many passengers are represented?

**90,181 passengers**

This also demonstrates an important analytical distinction:

> **Bookings ≠ Passengers**

One booking can contain multiple passengers.

---

## 3. What is the confirmation rate?

The dataset shows:

| Confirmation Status | Percentage |
|---|---:|
| Confirmed | **66.49%** |
| Not Confirmed | **33.51%** |

Approximately two-thirds of bookings are confirmed, while about one-third are not confirmed.

---

## 4. Does travel class have a relationship with confirmation?

Confirmation rates were compared across travel classes.

| Class | Confirmed | Not Confirmed |
|---|---:|---:|
| 1AC | 66.52% | 33.48% |
| 2AC | 66.46% | 33.54% |
| 3AC | **66.96%** | 33.04% |
| Sleeper | 66.03% | **33.97%** |

In this dataset, **3AC has the highest confirmation rate**, while Sleeper has the lowest.

However, the differences are relatively small, so travel class does not appear to create a large confirmation-rate gap in this dataset.

---

## 5. Does quota affect confirmation?

Confirmation rates were compared across booking quotas.

| Quota | Confirmed | Not Confirmed |
|---|---:|---:|
| General | **67.02%** | 32.98% |
| Ladies | 66.26% | 33.74% |
| Premium Tatkal | 66.50% | 33.50% |
| Tatkal | 66.19% | 33.81% |

General quota has the highest confirmation rate in the analyzed data, while Tatkal has the lowest.

Again, the differences are relatively small.

---

## 6. Does booking channel show different confirmation patterns?

| Booking Channel | Confirmed | Not Confirmed |
|---|---:|---:|
| Counter | 65.79% | 34.21% |
| IRCTC Website | 66.79% | 33.21% |
| Mobile App | **66.88%** | 33.12% |

The **Mobile App** has the highest confirmation rate among the three channels in this dataset.

The Counter channel has the lowest.

---

## 7. Does booking earlier relate to confirmation?

The analysis created booking lead-time categories to investigate whether booking earlier is associated with a different confirmation rate.

In the available dataset, the EDA output places the analyzed bookings in the `90+ Days` lead-time category, with a confirmation rate of **66.49%**.

Because the data does not provide enough variation across the lead-time categories in the resulting analysis, a strong relationship between booking lead time and confirmation should **not** be claimed from this analysis alone.

---

## 8. How does waitlisting relate to confirmation?

The dataset contains:

- **19,947 non-waitlisted bookings**
- **10,053 waitlisted bookings**

The EDA shows:

| Waitlisted | Confirmed | Not Confirmed |
|---|---:|---:|
| No | 100% | 0% |
| Yes | 0% | 100% |

This is a very strong pattern in the dataset.

However, this should be interpreted carefully: `Confirmation Status` is effectively aligned with waitlist status in these records. Therefore, this result shows a **direct relationship in the dataset**, but it should not be presented as evidence that waitlisting independently causes non-confirmation.

The same limitation applies to the waitlist-position analysis: every `No WL` record is confirmed, while waitlisted records are not confirmed.

---

## 9. Does peak season affect confirmation?

The dataset contains:

- **15,089 peak/holiday-season bookings**
- **14,911 non-peak bookings**

Confirmation rates:

| Season | Confirmed | Not Confirmed |
|---|---:|---:|
| Non-Peak | **66.82%** | 33.18% |
| Peak | 66.16% | 33.84% |

Peak-season bookings have a slightly lower confirmation rate than non-peak bookings.

The difference is small, so this should be treated as an observed pattern rather than a causal conclusion.

---

# 📅 Demand Analysis

## 10. Which months have the highest journey demand?

The monthly booking distribution is fairly balanced.

The highest number of bookings occurs in:

**October → 2,563 bookings**

Other high-volume months include:

- January → 2,542
- March → 2,542
- July → 2,542
- August → 2,542
- September → 2,490
- December → 2,542

The monthly pattern does not show an extreme concentration in one month.

---

## 11. Which days have the highest demand?

The number of bookings is also highly balanced across weekdays.

The highest observed counts are:

- Monday → 4,286
- Tuesday → 4,286
- Wednesday → 4,286
- Thursday → 4,286
- Sunday → 4,286

Friday and Saturday each have **4,285** bookings.

This suggests that the dataset does not contain a strong weekday demand difference.

---

# 🚆 Train & Route Analysis

## 12. Which trains have the most bookings?

The top observed train numbers include:

| Train Number | Bookings |
|---:|---:|
| 49540 | 5 |
| 90260 | 5 |
| 54196 | 5 |
| 61441 | 5 |
| 89496 | 5 |

Several other trains have four bookings.

The relatively low booking count per individual train suggests that train-level rankings should be interpreted carefully when using this dataset.

---

## 13. Which routes have the most bookings?

Top routes include:

| Route | Bookings |
|---|---:|
| KOAA → SC | 80 |
| GKP → LTT | 79 |
| LKO → MAS | 78 |
| BCT → LTT | 77 |
| GKP → JHS | 76 |
| BCT → MMCT | 76 |
| SC → LTT | 75 |
| BBS → KOAA | 75 |
| SC → UMB | 74 |
| PNBE → NDLS | 73 |

**KOAA → SC** is the highest-volume route in the analyzed dataset.

---

# 💺 Seat Availability Analysis

The dataset's `Seat Availability` ranges from:

- Minimum → **0**
- Maximum → **499**
- Average → **248.49**

The analysis also identified trains with the lowest average seat availability.

Several trains have an average availability of **0**, indicating that these trains have no available seats across the records represented for them.

This can be useful for identifying trains that may require closer capacity monitoring.

---

# 💡 Key Business Insights

Based on the completed analysis, the main observations are:

1. **Overall confirmation rate is 66.49%.**
2. **30,000 bookings represent 90,181 passengers**, showing why booking count and passenger count should be analyzed separately.
3. **3AC has the highest confirmation rate (66.96%)** among travel classes, although the difference between classes is small.
4. **General quota has the highest confirmation rate (67.02%)** among the analyzed quotas.
5. **Mobile App bookings have the highest confirmation rate (66.88%)** among the booking channels.
6. **Peak-season bookings have a slightly lower confirmation rate** than non-peak bookings.
7. **Waitlist status is perfectly aligned with confirmation status in this dataset**, making it a strong descriptive indicator but not an independent causal factor.
8. **October has the highest monthly booking volume** with 2,563 bookings.
9. **Demand is almost evenly distributed across weekdays.**
10. **KOAA → SC is the highest-volume route** with 80 bookings.
11. **Seat availability varies from 0 to 499**, with an average of approximately 248.49.
12. Some train-level availability averages are **0**, which may indicate capacity pressure in the represented records.

---

# 🧠 Important Analytical Limitations

A good data analyst should also identify what the data **cannot** prove.

### 1. Correlation is not causation

The analysis identifies relationships and patterns. It does not prove that one variable causes another.

### 2. Waitlist and confirmation are strongly coupled

In this dataset, waitlisted records are not confirmed and non-waitlisted records are confirmed. Therefore, waitlist status should not be presented as an independently tested predictor of confirmation.

### 3. Booking lead-time analysis has limited variation

The resulting EDA places the analyzed bookings in the `90+ Days` category. Therefore, the project cannot reliably compare confirmation performance across all lead-time groups using the current data.

### 4. Train-level rankings have small counts

The most-booked trains have only around 4–5 bookings each. These rankings are therefore useful for demonstrating the analysis workflow, but they are not strong enough to represent real-world train popularity.

### 5. Dataset representativeness

The dataset used in this project contains 30,000 records, but no external source or sampling methodology was provided with the project. Therefore, the findings should be treated as **dataset-specific observations**, not as conclusions about the entire railway system.

---

# 🛠️ Tools & Technologies

### Programming & Analysis
- Python
- Pandas
- NumPy

### Visualization
- Matplotlib
- Seaborn

### Environment
- Jupyter Notebook

### File Formats
- CSV
- Excel

---

# 📁 Project Structure

```text
Railway-Ticket-Confirmation-Analysis/
│
├── Railway Ticket Confirmation(2).csv
│
├── 1_Railway_Cleaning.ipynb
├── 2_Railway_Featuring.ipynb
├── 3_Railway_EDA.ipynb
│
├── 1_Railway_Cleaned.csv
├── 1_Railway_Cleaned.xlsx
│
├── 2_Railway_Featured.csv
├── 2_Railway_Featured.xlsx
│
└── README.md
```

---

# 🔬 Analysis Pipeline

```text
Raw Railway Data
       ↓
Data Understanding
       ↓
Missing Value Analysis
       ↓
Duplicate & Data Validation
       ↓
Data Cleaning
       ↓
Date & Data Type Conversion
       ↓
Feature Engineering
       ↓
Business Questions
       ↓
Exploratory Data Analysis
       ↓
Visualizations
       ↓
Insights & Limitations
```

---

# 📌 What This Project Demonstrates

This project demonstrates practical Data Analyst skills including:

- Data loading and inspection
- Data quality checking
- Missing-value treatment
- Duplicate detection
- Data type conversion
- Data validation
- Feature engineering
- Categorical analysis
- GroupBy analysis
- Cross-tabulation
- Percentage calculations
- Business-question-driven EDA
- Data visualization
- Insight generation
- Analytical limitations and interpretation

---

# 🚀 Future Improvements

The analysis can be extended by adding:

- A dashboard using **Power BI or Tableau**
- Statistical significance testing
- Correlation and association analysis
- More detailed route-level analysis
- Train-type performance comparison
- Seat availability vs. confirmation analysis
- Passenger demographic analysis
- Time-series demand analysis
- A predictive model for confirmation probability
- Interactive filters for class, quota, route, train, and booking channel

---

# 👨‍💻 Project Purpose

This project was created as a practical **Data Analytics portfolio project** to demonstrate the complete process of turning raw railway booking data into structured, interpretable business insights.

The focus is on the **thinking process of a Data Analyst**:

> **Understand the data → Clean the data → Transform the data → Ask the right questions → Analyze patterns → Communicate insights → Identify limitations**


# 🚆 Railway Ticket Confirmation Analysis

## 📌 About the Project

A practical **Data Analytics project** using railway booking data to understand **ticket confirmation, waitlisting, booking behavior, demand, and seat availability**.

The project follows a complete analytics workflow:

**Data Cleaning → Feature Engineering → EDA → Insights**

## 🎯 Why I Did This

I wanted to work with a real-world style dataset and practice how a Data Analyst turns raw booking data into meaningful business insights.

Key questions explored:
- What is the overall confirmation rate?
- Does class, quota, or booking channel affect confirmation?
- How does waitlisting relate to confirmation?
- When is railway demand highest?
- Which routes have the most bookings?
- How does seat availability vary?

## 🧹 Data Cleaning

- Checked missing values, duplicates, data types, and invalid values.
- Handled missing **Special Considerations**.
- Processed missing **Waitlist Position** values.
- Converted date columns into datetime format.
- Validated important numeric and categorical columns.

## 🧩 Feature Engineering

Created useful features such as:
- Booking Lead Time
- Waitlist Number
- Route
- Journey Month
- Journey Day
- Journey Year
- Waitlist Category
- Booking Lead-Time Category
- Distance Category
- Passenger Group Size

## 📊 Key Findings

- **30,000 bookings** and **90,181 passengers**
- **66.49%** overall confirmation rate
- **3AC** had the highest confirmation rate at **66.96%**
- **General quota** had the highest confirmation rate at **67.02%**
- **Mobile App** had the highest confirmation rate among channels at **66.88%**
- **October** had the highest monthly booking volume
- **KOAA → SC** was the highest-volume route with **80 bookings**
- Seat availability ranged from **0 to 499**

## 🛠️ Tools Used

**Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter Notebook**

## 📁 Project Structure

```text
├── Railway Ticket Confirmation(2).csv
├── 1_Railway_Cleaning.ipynb
├── 2_Railway_Featuring.ipynb
├── 3_Railway_EDA.ipynb
└── README.md
```

## 💡 What I Learned

This project helped me practice the complete Data Analyst workflow — from **understanding and cleaning raw data to creating features, performing EDA, and communicating insights**.

## 🚀 Future Scope

- Build a **Power BI/Tableau dashboard**
- Perform statistical analysis
- Analyze route and train performance in more depth
- Build a model to predict ticket confirmation

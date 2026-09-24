
# Task 4 - Shopify Stock Data Analysis

## Project Overview

This project performs **Exploratory Data Analysis (EDA)** on Shopify stock market data using Python.

The analysis focuses on understanding:

- Shopify stock price trends
- Opening, high, low, and closing prices
- Trading volume
- Moving averages
- Daily returns
- Distribution of daily returns

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook / Google Colab

## Dataset

The dataset used in this project is:

```text
shopify_stock.csv
```

The dataset contains Shopify stock market information such as:

- Date
- Open price
- High price
- Low price
- Close price
- Volume

---

# Steps Performed

## Step 1 - Import Required Libraries

The required Python libraries are imported.

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

### Purpose

| Library | Purpose |
|---------|---------|
| NumPy | Numerical operations |
| Pandas | Data loading and analysis |
| Matplotlib | Data visualization |
| Seaborn | Statistical visualization |

---

## Step 2 - Load the Dataset

The Shopify stock dataset is loaded using Pandas.

```python
df = pd.read_csv("/content/shopify_stock.csv")
```

The dataset is stored in a DataFrame named `df`.

---

## Step 3 - Display the First Rows

The first few records are displayed using:

```python
df.head()
```

This helps to understand the structure and contents of the dataset.

---

## Step 4 - Display the Last Rows

The last few records are displayed using:

```python
df.tail()
```

This helps to check the ending records of the dataset.

---

## Step 5 - Check Dataset Shape

The number of rows and columns is checked using:

```python
df.shape
```

This provides the size of the dataset.

---

## Step 6 - Check Dataset Information

The structure and data types of the dataset are checked using:

```python
df.info()
```

This shows:

- Column names
- Number of entries
- Data types
- Non-null values

---

## Step 7 - Generate Statistical Summary

Descriptive statistics are generated using:

```python
df.describe()
```

This provides statistical information such as:

- Count
- Mean
- Standard deviation
- Minimum
- Maximum
- Quartiles

for the numerical columns.

---

## Step 8 - Convert Date Column

The `date` column is converted into datetime format.

```python
df["date"] = pd.to_datetime(df["date"], utc=True)
```

The data type is then checked:

```python
df["date"].dtype
```

This makes the date column suitable for time-series analysis.

---

## Step 9 - Sort Data by Date

The dataset is sorted according to the date.

```python
df = df.sort_values("date")
```

Sorting the data chronologically helps in correctly analyzing stock price trends over time.

---

# Data Visualization

## Step 10 - Shopify Stock Price Trend

The opening, high, low, and closing prices are plotted.

```python
plt.figure(figsize=(16, 8))

plt.plot(df["date"], df["open"], label="Open")
plt.plot(df["date"], df["high"], label="High")
plt.plot(df["date"], df["low"], label="Low")
plt.plot(df["date"], df["close"], label="Close")

plt.title("Shopify Stock Price")
plt.xlabel("Date")
plt.ylabel("Price")
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Purpose

This visualization helps understand how Shopify's stock prices changed over the dataset period.

---

## Step 11 - Shopify Stock Trading Volume

The trading volume is plotted using:

```python
plt.figure(figsize=(16, 8))

plt.plot(df["date"], df["volume"], label="Volume")

plt.title("Shopify Stock Volume")
plt.xlabel("Date")
plt.ylabel("Volume")
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Purpose

This graph shows changes in Shopify's trading volume over time.

---

## Step 12 - Calculate Moving Averages

Two moving averages are calculated:

```python
df["MA20"] = df["close"].rolling(window=20).mean()

df["MA50"] = df["close"].rolling(window=50).mean()
```

### Moving Averages Used

| Moving Average | Description |
|----------------|-------------|
| MA20 | 20-day moving average |
| MA50 | 50-day moving average |

Moving averages help smooth short-term price fluctuations and show the general price trend.

---

## Step 13 - Shopify Closing Price Trend

The closing price is visualized separately.

```python
plt.figure(figsize=(12, 6))

plt.plot(df["date"], df["close"], label="Daily Close")

plt.title("Shopify Stock Closing Price Trend")
plt.xlabel("Date")
plt.ylabel("Price")
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Purpose

This visualization focuses specifically on the daily closing price trend.

---

## Step 14 - Calculate Daily Returns

Daily returns are calculated using the percentage change in closing price.

```python
df["Daily_Return"] = df["close"].pct_change()
```

The updated DataFrame is then displayed:

```python
df
```

### Formula

```text
Daily Return = (Current Close - Previous Close) / Previous Close
```

The `pct_change()` function calculates this automatically.

---

## Step 15 - Visualize Daily Returns

A histogram with a KDE curve is created using Seaborn.

```python
plt.figure(figsize=(10, 6))

sns.histplot(
    df["Daily_Return"].dropna(),
    bins=50,
    kde=True
)

plt.title("Shopify Daily Returns")
plt.xlabel("Daily Return")
plt.ylabel("Frequency")
plt.tight_layout()
plt.show()
```

### Purpose

This visualization shows the distribution and frequency of Shopify's daily stock returns.

---

# Project Workflow

```text
Shopify Stock Dataset
        ↓
Load Dataset
        ↓
Explore Dataset
        ↓
Check Shape and Information
        ↓
Generate Statistical Summary
        ↓
Convert Date Column
        ↓
Sort Data by Date
        ↓
Analyze Stock Prices
        ↓
Analyze Trading Volume
        ↓
Calculate MA20 and MA50
        ↓
Analyze Closing Price
        ↓
Calculate Daily Returns
        ↓
Visualize Daily Return Distribution
```

---

# Project Structure

```text
Task4_EDA/
│
├── Task4_EDA.ipynb
├── shopify_stock.csv
└── README.md
```

---

# How to Run the Project

## Using Google Colab

1. Open `Task4_EDA.ipynb` in Google Colab.
2. Upload the `shopify_stock.csv` dataset.
3. Make sure the dataset is available at:

   ```text
   /content/shopify_stock.csv
   ```

4. Run the notebook cells from top to bottom.
5. View the generated stock price, volume, closing price, and daily return visualizations.

## Using Jupyter Notebook

Install the required libraries:

```bash
pip install numpy pandas matplotlib seaborn jupyter
```

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
Task4_EDA.ipynb
```

Place `shopify_stock.csv` in the required location and run all cells.

---

# Key Analysis Areas

| Analysis | Description |
|----------|-------------|
| Dataset Exploration | Examines the structure and contents of the dataset |
| Stock Price | Analyzes open, high, low, and close prices |
| Trading Volume | Examines changes in stock trading volume |
| Moving Average | Calculates 20-day and 50-day moving averages |
| Closing Price | Visualizes the daily closing price trend |
| Daily Return | Calculates percentage changes in closing price |
| Return Distribution | Visualizes the distribution of daily returns |

---

# Conclusion

This project demonstrates how Python can be used to perform Exploratory Data Analysis on stock market data.

The analysis includes:

- Dataset exploration
- Date processing
- Stock price visualization
- Trading volume analysis
- Moving average calculation
- Closing price analysis
- Daily return distribution

The project provides a basic understanding of **Shopify stock price behavior and daily return patterns** using Python data analysis and visualization techniques.

# 🛍️ Mall Customer Segmentation Using Unsupervised Learning

### Unsupervised Learning — Practical Project 1 (PR-1)

> A complete Unsupervised Machine Learning project for discovering meaningful customer segments using **K-Means, Agglomerative Hierarchical Clustering, and DBSCAN**.

---

## 📌 Project Overview

Customer segmentation helps businesses understand groups of customers with similar characteristics and spending behaviour.

This project uses the **Mall Customers Dataset** to identify customer segments based on:

- 👤 Age
- 💰 Annual Income
- 🛍️ Spending Score

Three different unsupervised clustering algorithms are implemented and compared:

| Algorithm | Approach |
|---|---|
| 🔵 K-Means | Centroid-based clustering |
| 🟣 Agglomerative Hierarchical Clustering | Hierarchical clustering |
| 🟢 DBSCAN | Density-based clustering |

The project covers the complete machine learning workflow:

**Data Acquisition → EDA → Feature Selection → Standardization → Clustering → Evaluation → Customer Profiling → Business Insights**

---

# 🎯 Objectives

The main objectives of this project are to:

- Perform Exploratory Data Analysis on customer data
- Identify suitable features for clustering
- Standardize numerical features
- Apply multiple clustering algorithms
- Determine suitable clustering configurations
- Evaluate clustering quality using multiple metrics
- Visualize customer segments
- Profile the resulting customer groups
- Translate clusters into potential business and marketing insights

---

# 📊 Dataset

### Source

**Kaggle — Customer Segmentation Tutorial in Python**

https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python

The dataset is downloaded programmatically using **KaggleHub**.

### Dataset Summary

| Property | Value |
|---|---:|
| Customers | 200 |
| Original Features | 5 |
| Missing Values | 0 |
| Duplicate Records | 0 |
| Dataset Type | Customer demographic & spending data |

### Original Features

| Feature | Description |
|---|---|
| `CustomerID` | Unique customer identifier |
| `Gender` | Customer gender |
| `Age` | Customer age |
| `Annual Income (k$)` | Annual income in thousands of dollars |
| `Spending Score (1-100)` | Customer spending score |

---

# 🎯 Feature Selection

The primary clustering features are:

```text
Age
Annual Income
Spending Score

## 📌 Feature Description

| 📊 Feature | 📝 Description | 🎯 Role in Clustering |
|---|---|---|
| 👤 **Age** | Age of the customer in years. | Helps identify differences in customer behaviour across age groups. |
| 💰 **Annual Income** | Annual income of the customer measured in thousands of dollars (k$). | Helps identify customers according to their purchasing capacity. |
| 🛍️ **Spending Score** | Mall-assigned spending score ranging from 1 to 100. | Represents the customer's spending behaviour and engagement level. |

### 🎯 Feature Selection Rationale

The three selected features represent different dimensions of customer behaviour:

- 👤 **Age** → Demographic characteristic
- 💰 **Annual Income** → Financial characteristic
- 🛍️ **Spending Score** → Behavioural characteristic

Using these three variables allows the clustering algorithms to identify customer groups based on a combination of demographic, financial, and spending characteristics.

### 🚫 Features Excluded from Clustering

**CustomerID** was excluded because it is only an identification field and does not provide meaningful behavioural information.

**Gender** was retained for descriptive analysis but was not included in the primary clustering feature matrix. The main clustering objective was to use the numerical customer characteristics directly related to segmentation.

---

# 🔎 Exploratory Data Analysis (EDA)

Exploratory Data Analysis was performed before applying clustering algorithms to understand the structure, distribution, relationships, and variability within the dataset.

### 🎯 EDA Objectives

The EDA stage was used to:

- 📊 Understand numerical feature distributions.
- 🔍 Identify unusual observations.
- 📈 Examine relationships between selected features.
- 📋 Understand feature ranges and variability.
- 🧩 Determine the need for feature scaling.
- 💡 Support meaningful interpretation of customer segments.

### 📊 Dataset Summary

| 📌 Statistic | 👤 Age | 💰 Annual Income (k$) | 🛍️ Spending Score |
|---|---:|---:|---:|
| Mean | 38.85 | 60.56 | 50.20 |
| Standard Deviation | 13.97 | 26.26 | 25.82 |
| Minimum | 18 | 15 | 1 |
| Maximum | 70 | 137 | 99 |

### 📈 Distribution Analysis

Histograms and KDE plots were used to understand the distribution of:

- 👤 Age
- 💰 Annual Income
- 🛍️ Spending Score

These visualizations help identify:

- Central tendency
- Spread of observations
- Distribution shape
- Customer concentration
- Potential unusual observations

### 👥 Gender Distribution

The original dataset contains:

- 👩 **112 Female customers**
- 👨 **88 Male customers**

Gender was used for descriptive understanding but was not included as a primary clustering feature.

### 🔗 Correlation Analysis

A correlation heatmap was created to examine relationships between the selected clustering features.

| 🔗 Feature Pair | 📊 Correlation |
|---|---:|
| 👤 Age – 🛍️ Spending Score | -0.327 |
| 💰 Annual Income – 🛍️ Spending Score | 0.010 |
| 👤 Age – 💰 Annual Income | -0.012 |

The strongest observed relationship is between **Age and Spending Score**, showing a moderate negative relationship. The other feature relationships are close to zero.

### 📦 Outlier Assessment

An IQR-based assessment was performed to identify potentially unusual observations.

| 📊 Feature | 🔎 IQR-Based Outliers |
|---|---:|
| 👤 Age | 0 |
| 💰 Annual Income | 2 |
| 🛍️ Spending Score | 0 |

The two unusual Annual Income observations were retained because unusual customers may represent meaningful customer behaviour and should not automatically be removed from an unsupervised learning analysis.

---

# ⚙️ Feature Scaling

Because the selected clustering algorithms use distance-based calculations, feature scaling was applied before clustering.

### 🛠️ Scaling Method

`StandardScaler` from Scikit-learn was used to standardize:

- 👤 Age
- 💰 Annual Income
- 🛍️ Spending Score

After standardization, the features have approximately:

```text
Mean = 0
Standard Deviation = 1

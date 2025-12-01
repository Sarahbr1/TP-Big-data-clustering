# K-Means Clustering: Scikit-Learn vs Apache Spark

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/sklearn-latest-orange.svg)](https://scikit-learn.org/)
[![Apache Spark](https://img.shields.io/badge/PySpark-3.x-red.svg)](https://spark.apache.org/)

## 📋 Overview

This repository contains an **academic exercise** that aims to compare the performance, scalability, and implementation complexity of K-Means clustering across two dominant computational frameworks: **Scikit-Learn** (in-memory, single-node) and **Apache Spark MLlib** (distributed computing).

## 📊 Datasets Tested

We started testing the implementation logic with different size of synthetic data

| Dataset | Samples | Features | Use Case |
|---------|---------|----------|----------|
| **Wine Quality** | 4,898 | 12 | Small-scale validation |
| **MNIST** | 70,000 | 784 | High-dimensionality test |
| **HIGGS** | 1M - 2M | 28 | Large-scale performance |

## 🔍 Key Findings

### 1. The Spark Overhead Floor
Apache Spark exhibits a **~7-10 second fixed startup cost** (JVM initialization, task scheduling, serialization), making it inefficient for datasets **< 100k samples** on single nodes.

### 2. Efficiency Crossover Point
Performance gap narrows between **500k - 1M samples**. Spark remains slower in absolute time but the overhead-to-computation ratio decreases significantly.

### 3. Dimensionality Sensitivity
- **Scikit-Learn**: Highly sensitive to feature count (MNIST 70k×784 slower than HIGGS 1M×28)
- **Spark**: Performance depends more on row count than dimensionality

### 4. Memory Stability vs Speed
```
Scikit-Learn = Speed + Simplicity + RAM Limitation
Apache Spark  = Scalability + Stability + Overhead Cost
```

At 2M samples: Scikit-Learn consumed **427 MB** (approaching limits), Spark operated comfortably with disk-spillable architecture.

### 5. Mathematical Equivalence
Both frameworks produce **identical Inertia values** across all tests, confirming algorithmic consistency.

## 📈 Performance Summary

| Dataset Size | Scikit-Learn | Apache Spark | Ratio |
|--------------|--------------|--------------|-------|
| 5k (Wine) | 0.04s | 2.39s | **60× slower** |
| 70k (MNIST) | 81.89s | 99.41s | **1.2× slower** |
| 1M (HIGGS) | 6.04s | 73.76s | **12× slower** |
| 2M (HIGGS) | 13.22s | 133.19s | **10× slower** |

*Note: Spark slower due to single-node serialization overhead; excels in multi-node clusters.*

## 💡 Practical Recommendations

### Use **Scikit-Learn** when:
✅ Dataset < 1GB or < 500k rows  
✅ Rapid prototyping required  
✅ Single-machine infrastructure  
✅ Code simplicity is priority  

### Use **Apache Spark** when:
✅ Dataset > 10GB or > 1M rows  
✅ Data approaching/exceeding RAM limits  
✅ Production Big Data pipelines  
✅ Horizontal cluster scaling needed  
✅ Fault tolerance critical  


## 📝 Key Takeaway

> **Start with Scikit-Learn.** Prototype quickly, validate your approach, and only migrate to Spark when encountering memory errors or when data growth demands it. The best tool is the simplest one that solves your problem.

## 🛠️ Technologies Used

- **Python 3.8+**
- **Scikit-Learn**: Machine learning library for in-memory processing
- **Apache Spark 3.x (PySpark)**: Distributed computing framework
- **Pandas & NumPy**: Data manipulation
- **Matplotlib**: Visualization
- **Google Colab**: Development environment

## 📄 License

This project is for **educational purposes** only.

## 👤 Author

Sara BRAHITI
M2 TNI - Paris Saclay

---

**📖 For detailed analysis, methodology, and visualizations, see the [[full report]([url](https://github.com/Sarahbr1/TP-Big-data-clustering/blob/main/Report_Big_Data_Clustering.pdf))].**

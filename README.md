# **Fawry Data Engineering Architecture**

This case study outlines the data engineering infrastructure required for Fawry to process massive daily transaction volumes. The objective is to design a system that ensures payments remain **fast**, **secure**, and **accurately recorded**.

---


## **Project Scope**

The proposed architecture addresses three major challenges in the fintech domain:

### **1. Real-Time Fraud Detection**
- Detect and block suspicious activities instantly.  
- Target latency: **< 500 ms** before the transaction is finalized.

### **2. Financial Reconciliation**
- Achieve **zero data loss**.
- Ensure all transactions match across systems by end of day.

### **3. Scalability**
- Efficiently handle traffic spikes, especially during salary payout days.

---

## **Architecture Overview**

The design follows the **Lambda Architecture** — combining real-time and batch processing for accuracy and speed.

### **Layers & Components**

| **Component** | **Tech Stack**        | **Role** |
|---------------|------------------------|----------|
| **Ingestion** | Apache Kafka           | Serves as a buffer; absorbs high POS traffic. |
| **Speed Layer** | Apache Flink        | Real-time stream processing; detects fraud. |
| **Batch Layer** | Apache Spark        | Processes historical data; generates end-of-day financial reports. |
| **Storage** | Data Lake (S3)          | Secure storage for all raw transaction logs. |

---

## **Submission Details**

**Submitted By:** Mahmoud Ali AbdelMaksoud Salem  
**ID:** 21139149  
**Group:** MNF4_AIS5_S1  
**Course:** Data Engineering Project  

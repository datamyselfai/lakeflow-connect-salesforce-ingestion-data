# lakeflow-connect-salesforce-ingestion-data
Lakeflow Connect Salesforce Ingestion Sample Data. This is the dataset for this video: https://www.youtube.com/watch?v=neH6vJv8AbE
https://developer.salesforce.com/docs/atlas.en-us.dataLoader.meta/dataLoader/data_loader_intro.htm

# 🧾 Salesforce Data Preparation for Databricks Demo

This short guide explains how to prepare Salesforce with custom fields and import the provided CSV files using **Salesforce Data Loader**.  
It ensures that all object relationships (Account ↔ Contact ↔ Opportunity ↔ Campaign) are created correctly for later ingestion into Databricks.

---

## ⚙️ Step 1 – Create Custom External ID Fields

In Salesforce, go to:  
**Setup → Object Manager → [Object Name] → Fields & Relationships → New**

Create the following field on each object:

| Object | Field Label | Field Name | Type | Notes |
|---------|--------------|-------------|------|-------|
| **Account** | External Id | External_Id__c | Text | Mark as **External ID** and **Unique** |
| **Contact** | External Id | External_Id__c | Text | Mark as **External ID** and **Unique** |
| **Opportunity** | External Id | External_Id__c | Text | Mark as **External ID** and **Unique** |
| **Campaign** | External Id | External_Id__c | Text | Mark as **External ID** and **Unique** |

> 💡 The External ID fields allow Salesforce to link records across multiple CSVs (e.g., matching Opportunities to their parent Accounts) during import.

---

## 📦 Step 2 – Import Data Using Salesforce Data Loader

1. **Download and install Salesforce Data Loader**  
   👉 [Official Salesforce Data Loader Guide]([https://help.salesforce.com/s/articleView?id=sf.data_loader.htm&type=5](https://developer.salesforce.com/docs/atlas.en-us.dataLoader.meta/dataLoader/data_loader_intro.htm))
   👉 Installation Guide: https://www.youtube.com/watch?v=vZOsb9gvFu4 
   👉 Video Guide once installed: https://www.youtube.com/watch?v=8xtJ_Ft5nVQ&t=113s

3. **Login** to Data Loader using your Salesforce credentials (choose **Production** or **Sandbox**).

4. **Import the CSVs in this order (you find it in this git repo in data folder):**
   1. `Accounts.csv`  
   2. `Contacts.csv`  
      - **Match on:** `External_Id__c`  
      - **Account lookup field:** `Account:External_Id__c`
   3. `Opportunities.csv`  
      - **Match on:** `External_Id__c`  
      - **Account lookup field:** `Account:External_Id__c`
   4. `Campaigns.csv`  
   5. `CampaignMembers.csv`  
      - **Campaign lookup field:** `Campaign:External_Id__c`  
      - **Contact lookup field:** `Contact:External_Id__c`
   6. `Cases.csv`  
      - **Account lookup field:** `Account:External_Id__c`

5. **Verify the imports:**  
   - Open **Salesforce → App Launcher → Sales**  
   - Check that Accounts, Contacts, and Opportunities are correctly linked.

---

✅ **Result:**  
Your Salesforce org now contains realistic, relational CRM data ready for Databricks ingestion and analysis.

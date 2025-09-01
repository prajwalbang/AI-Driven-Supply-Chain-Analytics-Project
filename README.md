# 📦 AI-Driven Supply Chain Analytics Project

This project automates the flow of **daily sales data** from Gmail → Postgres (Supabase) → AI-powered spreadsheets (Quadratic), generating supply chain KPIs like **OTIF, Fill Rates, On-Time %, and In-Full %**.

It demonstrates how **automation + cloud databases + AI analytics** can solve real-world supply chain problems (like order fill rates and SLA tracking) with minimal manual effort.

<img width="1904" height="903" alt="image" src="https://github.com/user-attachments/assets/bc32a191-29a3-4990-8fdc-0d56e6ed2706" />
<img width="1910" height="921" alt="image" src="https://github.com/user-attachments/assets/bcfad116-119b-470f-b3d3-ff946af26e07" />
<img width="1912" height="910" alt="image" src="https://github.com/user-attachments/assets/d34a82dd-9cf6-4150-9219-e648435ade98" />


For Detailed Instructions follow the uploaded manuals

Summary Below
---

## 🚀 Tech Stack

- **n8n** → Workflow automation (email monitoring, CSV extraction, Postgres ingestion)  
- **Supabase/Postgres** → Cloud-hosted relational DB with star schema  
- **Quadratic (AI Spreadsheet)** → Prompt-based analysis & Python execution  
- **Open Exchange Rates API** → Automated USD↔INR currency conversion  
- **Python (via Quadratic)** → Data cleaning, merging fact/dim tables, KPI calculations  

---

## 🗂️ Project Workflow

### 1. Setup n8n on Localhost
Install Node.js, then run:  
```bash
npm install -g n8n
n8n
```
n8n starts at: `http://localhost:5678`  
Create an account and open the UI.  

<img width="805" height="246" alt="image" src="https://github.com/user-attachments/assets/85eb3614-8757-43ad-b7ce-eb69b42b5262" />


---

### 2. Configure Gmail API OAuth
1. Go to Google Cloud Console → Create Project.  
2. Enable Gmail API.  
3. Create OAuth consent screen → Add test users.  
4. Create OAuth Client ID → Web App → Redirect URI:  
   ```
   http://localhost:5678/rest/oauth2-credential/callback
   ```  
5. Download `client_secret.json` (⚠️ do not upload to GitHub).  
6. Connect in n8n for Gmail node authentication.  

---

### 3. Setup Postgres DB in Supabase
1. Sign up at [Supabase](https://supabase.com).  
2. Create a new project + database.  
3. Build schema:  
   - `fact_orders_aggregate`  
   - `fact_order_line`  
   - `dim_customers`  
   - `dim_products`  
   - `dim_target_orders`  
4. Import sample CSVs from `/datasets`.  
5. Verify date formats and data types.  



---

### 4. Automate Data Ingestion with n8n
Workflow:  
- Trigger: Gmail (filter subject = "Daily Sales")  
- Node: Extract CSV → JSON  
- Node: Postgres → Insert Rows into `fact_orders_aggregate` and `fact_order_line`  

⚡ Handle date parsing with Luxon format (`dd-MM-yyyy`).  

---

### 5. Connect Quadratic to Postgres
1. Open [Quadratic](https://www.quadratichq.com).  
2. Create a new file → connect to Postgres via Supabase credentials.  
3. Query and import tables into sheets.  
4. Use AI prompts to:  
   - Create **DimDate** table.  
   - Generate **ExchangeRate** table (USD↔INR via Open Exchange Rates API).  
   - Merge fact + dim tables into a **fact_summary**.  



---

### 6. Generate Supply Chain KPIs
KPIs calculated:  
- **Line Fill Rate** = lines delivered ÷ lines ordered  
- **Volume Fill Rate** = qty delivered ÷ qty ordered  
- **On-Time Delivery %**  
- **In-Full Delivery %**  
- **OTIF % (On-Time In-Full)**  



---

### 7. Business Insights
With Quadratic prompts:  
- Identify customers with largest OTIF gaps.  
- Find product categories with low “In-Full” rates.  
- Calculate average delay for late deliveries.  
- Estimate revenue loss from undelivered orders.  


---

## 📊 Supply Chain Learning
Beyond the tech, this project deepened my understanding of **supply chain reliability metrics**.  

👉 Companies like Amazon achieve *“next-day delivery”* because they **plan months in advance** — optimizing suppliers, warehouses, and logistics so the customer only sees the fast last-mile step.  

---

## 📂 Repo Contents
- `datasets/` → Sample sales data (scrubbed)  
- `docs/` → Summary of setup steps & prompts  
- `screenshots/` → n8n workflows, Supabase schema, Quadratic analysis  
- `README.md` → Project documentation  

---

## ⚠️ Notes
- Never upload `client_secret.json` or API keys.  
- Keep only anonymized sample CSVs.  
- Add screenshots at 📸 placeholders.  


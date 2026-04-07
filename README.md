# 🚀 Online Food Delivery Business Analytics System — SQL Project 3

> A comprehensive enterprise-level SQL business analytics system built on an online food delivery platform — covering customer segmentation, restaurant performance, delivery analysis, payment insights, advanced SQL objects, performance optimization, and database automation.

**Level:** 🔴 Expert | **Status:** 🔄 In Progress | **Part:** 3 of 3

---

## 🔗 Demo Link

> _This project is currently in progress. Screenshots and outputs will be added to the `/Screenshots` folder upon completion._

---

## 📑 Table of Contents

- [Business Understanding](#business-understanding)
- [Data Understanding](#data-understanding)
- [Screenshots](#screenshots)
- [Technologies](#technologies)
- [Setup](#setup)
- [Approach](#approach)
- [Status](#status)
- [Credits](#credits)

---

## 💼 Business Understanding

Building on the analytics foundations from Projects 1 and 2, this project constructs a **complete business analytics system** for an online food delivery platform. Real-world businesses need more than one-time queries — they need automated, optimised, and reusable systems that continuously monitor performance, enforce business rules, and scale with data growth.

**Goal:** Design and implement a full-stack SQL business analytics system covering 9 structured phases — from exploratory analysis and customer segmentation through to database automation with triggers, stored procedures, and performance indexes.

**Why this project?**
This is the third and final project in a 3-part SQL portfolio series. It represents the most advanced and complete demonstration of SQL engineering skills, including:
- Multi-phase structured analytics across revenue, customers, restaurants, and delivery
- Enterprise SQL objects: stored procedures, views, triggers
- Database performance engineering: indexes for query optimisation
- Business automation: triggers enforcing real-time data integrity rules

**Challenges faced:**
- Designing a customer segmentation model (Gold/Silver/Bronze) with meaningful and defensible spending thresholds
- Writing stored procedures flexible enough to accept dynamic parameters (e.g., Top N restaurants)
- Building triggers that enforce business rules at the database level without breaking existing insert operations
- Balancing index creation for query performance without over-indexing the database
- Integrating delivery agent data and payment fields not present in earlier projects

---

## 📊 Data Understanding

### Datasets Used
This project uses an **extended dataset** with 5 tables — adding delivery agent tracking and payment/discount fields not available in Projects 1 and 2:

| Table | Description |
|---|---|
| `customers` | Customer details including name, city, and spending history |
| `restaurants` | Restaurant information including name, city, and rating |
| `delivery_agents` | Delivery agent details for tracking delivery performance |
| `orders` | Full transaction records including payment method, discount, and delivery time |
| `order_items` | Line-item breakdown of items per order with pricing |

### Dataset Relationships
```
customers ──< orders ──< order_items
                │
          restaurants
                │
          delivery_agents
```

### New Capabilities vs Projects 1 & 2
| Feature | Project 1 & 2 | Project 3 |
|---|---|---|
| Delivery agent tracking | ❌ | ✅ |
| Delivery time analysis | ❌ | ✅ |
| Payment method data | ❌ | ✅ |
| Discount impact analysis | ❌ | ✅ |
| Customer spending tiers | ❌ | ✅ Gold/Silver/Bronze |
| Stored procedures | ❌ | ✅ |
| Triggers | ❌ | ✅ |
| Performance indexes | ❌ | ✅ |

**Future enhancements:**
- Connect the analytics views to a live Power BI dashboard
- Schedule monthly revenue reports using MySQL Event Scheduler
- Expand the stored procedure library for city-level and agent-level reporting

---

## 📸 Screenshots

> Screenshots will be added to the `/Screenshots` folder upon project completion.

---

## 🛠️ Technologies

| Tool | Purpose |
|---|---|
| **MySQL 8.x** | Core database engine — procedures, triggers, indexes, CTEs |
| **VS Code** | Primary development IDE |
| **SQLTools Extension** | MySQL connection and query execution within VS Code |
| **SQLTools MySQL/MariaDB Driver** | VS Code driver to connect to MySQL server |
| **MySQL Workbench** | Backend MySQL server (connected via SQLTools) |
| **Power BI / Google Sheets / Excel** | Visualisation of analytics outputs |
| **Git & GitHub** | Version control and project showcase |

---

## ⚙️ Setup

### Prerequisites
- MySQL Server installed and running (port 3306)
- VS Code with SQLTools + MySQL Driver installed
- *(Optional)* Power BI Desktop or Google Sheets for visualisations

### Step 1 — Clone the Repository
```bash
git clone https://github.com/BuragapalliKamachari/online-food-delivery-sql-project-3.git
cd online-food-delivery-sql-project-3
```

### Step 2 — Configure SQLTools in VS Code
1. Open VS Code → Click the **SQLTools icon** in the Activity Bar
2. Select **Add New Connection** → Choose **MySQL**
3. Enter connection details:
   - Host: `localhost`
   - Port: `3306`
   - Username: `root`
   - Password: _(your MySQL root password)_
4. Click **Test Connection** → **Save**

### Step 3 — Run SQL Scripts in Order
```
1. Database_Creation.sql          ← Create the project database
2. Table_Creation.sql             ← Create all 5 tables with constraints
3. Data_Insertion.sql             ← Load sample data for all tables
4. Phase1_Exploratory.sql         ← Revenue, orders, top customers
5. Phase2_Segmentation.sql        ← Gold / Silver / Bronze classification
6. Phase3_Restaurants.sql         ← Restaurant performance analysis
7. Phase4_Delivery.sql            ← Delivery time & late delivery analysis
8. Phase5_Payments.sql            ← Payment methods & discount impact
9. Phase6_Advanced_SQL.sql        ← CTEs, window functions, subqueries
10. Phase7_DB_Objects.sql         ← Views and stored procedures
11. Phase8_Indexes.sql            ← Performance optimization indexes
12. Phase9_Triggers.sql           ← Automation triggers
```

---

## 🔍 Approach

This project follows a **9-phase structured business analytics methodology**, progressing from exploration to automation.

---

### 🔵 Phase 1 — Exploratory Analysis

| # | Business Question | SQL Technique |
|---|---|---|
| 1 | Total revenue generated | `SUM(price * quantity)` |
| 2 | Total orders per city | `COUNT`, `GROUP BY city` |
| 3 | Top 10 customers by spending | `SUM`, `ORDER BY DESC`, `LIMIT 10` |

---

### 🟡 Phase 2 — Customer Segmentation

| # | Business Question | SQL Technique |
|---|---|---|
| 1 | Classify customers as Gold / Silver / Bronze by total spending | `CASE WHEN`, `SUM`, `GROUP BY` |

**Segmentation Logic:**
```sql
CASE
  WHEN total_spending >= 10000 THEN 'Gold'
  WHEN total_spending BETWEEN 5000 AND 9999 THEN 'Silver'
  ELSE 'Bronze'
END AS customer_category
```

---

### 🟠 Phase 3 — Restaurant Performance

| # | Business Question | SQL Technique |
|---|---|---|
| 1 | Top 10 restaurants by revenue | `SUM`, `JOIN`, `ORDER BY DESC` |
| 2 | Average rating vs revenue correlation | `AVG`, `SUM`, `GROUP BY` |

---

### 🔴 Phase 4 — Delivery Analysis

| # | Business Question | SQL Technique |
|---|---|---|
| 1 | Average delivery time per city | `AVG(delivery_time)`, `GROUP BY city` |
| 2 | Late deliveries (above 45 minutes) | `WHERE delivery_time > 45` |

---

### 🟣 Phase 5 — Payment & Discount Analysis

| # | Business Question | SQL Technique |
|---|---|---|
| 1 | Payment method distribution | `COUNT`, `GROUP BY payment_method` |
| 2 | Discount impact on total revenue | `SUM`, `CASE WHEN discount > 0` |

---

### ⚡ Phase 6 — Advanced SQL

| # | Technique | Purpose |
|---|---|---|
| 1 | CTE (Common Table Expression) | Monthly revenue calculation |
| 2 | Window Function — `RANK() OVER` | Rank restaurants by revenue |
| 3 | Subquery | Identify above-average revenue restaurants |

**Monthly Revenue CTE:**
```sql
WITH monthly_revenue AS (
  SELECT
    MONTH(order_date) AS month,
    SUM(total_amount) AS revenue
  FROM orders
  GROUP BY MONTH(order_date)
)
SELECT * FROM monthly_revenue ORDER BY month;
```

**Restaurant Revenue Ranking:**
```sql
SELECT
  restaurant_name,
  SUM(total_amount) AS total_revenue,
  RANK() OVER (ORDER BY SUM(total_amount) DESC) AS revenue_rank
FROM orders
JOIN restaurants USING (restaurant_id)
GROUP BY restaurant_name;
```

---

### 🗄️ Phase 7 — Database Objects

| Object | Name | Purpose |
|---|---|---|
| **View** | `revenue_view` | Reusable virtual table for revenue reporting |
| **Stored Procedure** | `get_top_n_restaurants` | Accepts N as parameter, returns top N restaurants by revenue |

**Stored Procedure:**
```sql
DELIMITER //
CREATE PROCEDURE get_top_n_restaurants(IN n INT)
BEGIN
  SELECT restaurant_name, SUM(total_amount) AS revenue
  FROM orders
  JOIN restaurants USING (restaurant_id)
  GROUP BY restaurant_name
  ORDER BY revenue DESC
  LIMIT n;
END //
DELIMITER ;

-- Usage:
CALL get_top_n_restaurants(5);
```

---

### ⚙️ Phase 8 — Performance Optimization

| Index | Column | Purpose |
|---|---|---|
| `idx_order_date` | `order_date` | Speeds up monthly revenue reports |
| `idx_customer_name` | `customer_name` | Optimises customer name joins |
| `idx_restaurant_name` | `restaurant_name` | Accelerates restaurant-level aggregations |

```sql
CREATE INDEX idx_order_date      ON orders(order_date);
CREATE INDEX idx_customer_name   ON customers(customer_name);
CREATE INDEX idx_restaurant_name ON restaurants(restaurant_name);
```

---

### 🤖 Phase 9 — Automation Logic

| Trigger | Rule | Action |
|---|---|---|
| `prevent_negative_discount` | Discount cannot be negative | Raises SQL error before INSERT/UPDATE |
| `delivery_delay_warning` | Delivery time > 45 minutes | Flags the record as a late delivery automatically |

**Trigger 1 — Prevent Negative Discount:**
```sql
CREATE TRIGGER prevent_negative_discount
BEFORE INSERT ON orders
FOR EACH ROW
BEGIN
  IF NEW.discount < 0 THEN
    SIGNAL SQLSTATE '45000'
    SET MESSAGE_TEXT = 'Discount cannot be negative.';
  END IF;
END;
```

**Trigger 2 — Delivery Delay Warning:**
```sql
CREATE TRIGGER delivery_delay_warning
BEFORE INSERT ON orders
FOR EACH ROW
BEGIN
  IF NEW.delivery_time > 45 THEN
    SET NEW.delivery_status = 'Late';
  END IF;
END;
```

---

## 📌 Status

```
🔄 In Progress — April 2026
```

### Phase Completion Tracker
| Phase | Description | Status |
|---|---|---|
| Phase 1 | Exploratory Analysis | 🔄 In Progress |
| Phase 2 | Customer Segmentation | 🔄 In Progress |
| Phase 3 | Restaurant Performance | 🔄 In Progress |
| Phase 4 | Delivery Analysis | 🔄 In Progress |
| Phase 5 | Payment & Discount Analysis | 🔄 In Progress |
| Phase 6 | Advanced SQL | 🔄 In Progress |
| Phase 7 | Database Objects | 🔄 In Progress |
| Phase 8 | Performance Optimization | 🔄 In Progress |
| Phase 9 | Automation Logic | 🔄 In Progress |

This is **Part 3 of 3** in the Online Food Delivery SQL Portfolio Series:
- ✅ Project 1 — Beginner Analysis
- ✅ Project 2 — Advanced Analytics
- 🔄 Project 3 — Business Analytics System ← You are here

---

## 🙏 Credits

| Contributor | Role |
|---|---|
| **Buragapalli Kamachari** | Project Author — SQL Engineering, Analytics & Automation |
| **MySQL Documentation** | Reference for stored procedures, triggers, and indexes |
| **SQLTools by Matheus Teixeira** | VS Code MySQL integration extension |
| **Power BI / Google / Microsoft** | Visualisation platforms used for reporting |
| **GitHub** | Repository hosting and portfolio showcase |

---

*Online Food Delivery SQL Project 3 of 3 | Buragapalli Kamachari | April 2026*

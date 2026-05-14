# 🔥 Fire Safety Management Database

A relational SQL database project modeling fire safety systems across buildings. Designed to support facility managers, safety inspectors, and data analysts in tracking fire detection infrastructure and maintenance history.

---

## 📌 Project Overview

This project demonstrates the design and implementation of a normalized relational database for managing **fire safety systems** in buildings. It covers real-world scenarios such as:

- Registering buildings with location and construction metadata
- Assigning one or more fire systems per building
- Tracking detector counts, error rates, and inspection history

---

## 🗄️ Database Schema

### Table: `Buildings`

Stores core information about each building.

| Column             | Type         | Description                        |
|--------------------|--------------|------------------------------------|
| `BuildingID`       | INT (PK)     | Unique building identifier         |
| `BuildingName`     | VARCHAR      | Name of the building               |
| `BuildingType`     | VARCHAR      | Type (e.g., residential, office)   |
| `ConstructionYear` | INT          | Year the building was constructed  |
| `BuildingSize`     | DECIMAL      | Size of the building (m²)          |
| `City`             | VARCHAR      | City where the building is located |
| `PostCode`         | VARCHAR      | Postal code                        |

---

### Table: `FireSystems`

Stores fire safety system details linked to buildings.

| Column               | Type         | Description                              |
|----------------------|--------------|------------------------------------------|
| `SystemID`           | INT (PK)     | Unique system identifier                 |
| `BuildingID`         | INT (FK)     | Reference to `Buildings.BuildingID`      |
| `Supplier`           | VARCHAR      | System supplier/manufacturer             |
| `SmokeDetector`      | INT          | Number of smoke detectors                |
| `MultiDetector`      | INT          | Number of multi-function detectors       |
| `Others`             | INT          | Count of other sensor types              |
| `Detectors`          | INT          | Total number of detectors                |
| `TotalErrors`        | INT          | Number of recorded faults/errors         |
| `FirstInspectionYear`| INT          | Year of first inspection                 |
| `FirstControl`       | INT          | Year of first official control           |

---

## 🔗 Entity Relationship

```
Buildings (1) ──────< FireSystems (many)
     │                      │
 BuildingID  ←──────  BuildingID (FK)
```

One building can have **one or more** fire safety systems assigned to it.

---

## 📁 Project Structure

```
fire-safety-db/
├── README.md
├── schema/
│   ├── create_buildings.sql      # DDL: Buildings table
│   ├── create_firesystems.sql    # DDL: FireSystems table
│   └── relationships.sql        # Foreign key constraints
├── queries/
│   └── sample_queries.sql       # Example SELECT queries
└── data/
    └── sample_data.sql           # Sample INSERT statements
```

---

## 💡 Sample Queries

```sql
-- Get all buildings with their fire system supplier
SELECT b.BuildingName, b.City, f.Supplier, f.Detectors, f.TotalErrors
FROM Buildings b
JOIN FireSystems f ON b.BuildingID = f.BuildingID;

-- Buildings with more than 10 total errors
SELECT b.BuildingName, f.TotalErrors
FROM Buildings b
JOIN FireSystems f ON b.BuildingID = f.BuildingID
WHERE f.TotalErrors > 10
ORDER BY f.TotalErrors DESC;

-- Total detectors per city
SELECT b.City, SUM(f.Detectors) AS TotalDetectors
FROM Buildings b
JOIN FireSystems f ON b.BuildingID = f.BuildingID
GROUP BY b.City;
```

---

## 🛠️ Technologies

- **SQL** (compatible with MySQL / PostgreSQL / MS SQL Server)
- Relational database design
- Primary & Foreign Key constraints
- JOIN operations and aggregate queries

---

## 🚀 How to Use

1. Clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/fire-safety-db.git
   ```
2. Open your SQL client (e.g., MySQL Workbench, DBeaver, pgAdmin)
3. Run `schema/create_buildings.sql` first
4. Run `schema/create_firesystems.sql`
5. Optionally load `data/sample_data.sql` for test data
6. Explore queries in `queries/sample_queries.sql`

---

## 📚 Learning Goals

This project was built to practice:
- Relational database design and normalization
- Writing clean DDL (Data Definition Language) scripts
- Using foreign keys and JOIN queries
- Structuring a SQL project for readability and maintainability

---

## 👤 Author

**[Your Name]**  
📧 your.email@example.com  
🔗 [LinkedIn](https://linkedin.com/in/yourprofile) | [GitHub](https://github.com/YOUR_USERNAME)

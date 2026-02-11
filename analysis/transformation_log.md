# Cycling Data Transformation Log

## Session: 2026-02-12

### Objective
Standardise 3 tables (Ben, Bob, Bill) into one unified dataset.

---

### Step 1: Add Week Column to Ben figures
**Completed:** 09:45

**Table Structure Before:**
| Cycling | Swimming | Running |
|---------|----------|---------|
| 1       | 3        | 0       |
| 2       | 3        | 0       |
| 2.5     | 1        | 0.5     |
| 2       | 1        | 1       |

**Power Query Steps:**
1. Added Index Column (from 1)
2. Added Custom Column `Week` with formula: `= "Week " & Text.From([Index])`
3. Removed Index column

**Table Structure After:**
| Cycling | Swimming | Running | Week   |
|---------|----------|---------|--------|
| 1       | 3        | 0       | Week 1 |
| 2       | 3        | 0       | Week 2 |
| 2.5     | 1        | 0.5     | Week 3 |
| 2       | 1        | 1       | Week 4 |

---

### Step 2: Standardise Bob figures
**Completed:** 09:52

**Table Structure Before (12 rows):**
| Week | Hours | Activity |
|------|-------|----------|
| 1    | 1.0   | Swimming |
| 1    | 1.5   | Cycling  |
| ...  | ...   | ...      |

**Power Query Steps:**
1. Pivot Column on Activity, Values = Hours, Don't Aggregate
2. Changed Week data type to Text
3. Added Custom Column `WeekText`: `= "Week " & Text.From([Week])`
4. Removed original Week column, renamed WeekText to Week
5. Added Custom Column `Person`: `= "Bob"`

**Table Structure After (4 rows):**
| Week   | Cycling | Swimming | Running | Person |
|--------|---------|----------|---------|--------|
| Week 1 | 1.5     | 1.0      | 2.0     | Bob    |
| Week 2 | 0.5     | 1.0      | 1.5     | Bob    |
| Week 3 | 1.0     | 2.5      | 0.5     | Bob    |
| Week 4 | 3.0     | 0.0      | 1.5     | Bob    |

---

### Step 3: Add Person column to Ben figures and Bill
**Completed:** 09:54

- Ben figures: Added Custom Column `Person` = "Ben"
- Bill: Added Custom Column `Person` = "Bill"

---

### Step 4: Append tables into Combined Data
**Completed:** 09:57

**Power Query Steps:**
1. Home → Append Queries → Append Queries as New
2. Selected Three or more tables
3. Added Ben figures, Bob figures, Bill
4. Renamed new query to "Combined Data"

**Combined Data Structure (12 rows):**
| Person | Week   | Cycling | Swimming | Running |
|--------|--------|---------|----------|---------|
| Ben    | Week 1 | 1.0     | 3        | 0.0     |
| Ben    | Week 2 | 2.0     | 3        | 0.0     |
| Ben    | Week 3 | 2.5     | 1        | 0.5     |
| Ben    | Week 4 | 2.0     | 1        | 1.0     |
| Bob    | Week 1 | 1.5     | 1.0      | 2.0     |
| Bob    | Week 2 | 0.5     | 1.0      | 1.5     |
| Bob    | Week 3 | 1.0     | 2.5      | 0.5     |
| Bob    | Week 4 | 3.0     | 0.0      | 1.5     |
| Bill   | Week 1 | 1.0     | 2        | 0.0     |
| Bill   | Week 2 | 1.5     | 2        | 0.5     |
| Bill   | Week 3 | 2.0     | 3        | 1.5     |
| Bill   | Week 4 | 1.5     | 2        | 1.0     |

---

### Step 5: Final Combined Data Structure
**Completed:** 10:30

**Final Combined Data Table:**
- **12 rows** (4 weeks × 3 people)
- **6 columns**: RowNumber (hidden key), Week, Cycling, Swimming, Running, Person
- **Data Types**: Week/Person (String), Activities (Double), RowNumber (Int64)
- **Relationships**: Auto-detected to source tables

**Complete Dataset:**
| Person | Week   | Cycling | Swimming | Running |
|--------|--------|---------|----------|---------|
| Bill   | Week 1 | 1.0     | 2.0      | 0.0     |
| Bill   | Week 2 | 1.5     | 2.0      | 0.5     |
| Bill   | Week 3 | 2.0     | 3.0      | 1.5     |
| Bill   | Week 4 | 1.5     | 2.0      | 1.0     |
| Bob    | Week 1 | 1.5     | 1.0      | 2.0     |
| Bob    | Week 2 | 0.5     | 1.0      | 1.5     |
| Bob    | Week 3 | 1.0     | 2.5      | 0.5     |
| Bob    | Week 4 | 3.0     | 0.0      | 1.5     |
| Ben    | Week 1 | 1.0     | 3.0      | 0.0     |
| Ben    | Week 2 | 2.0     | 3.0      | 0.0     |
| Ben    | Week 3 | 2.5     | 1.0      | 0.5     |
| Ben    | Week 4 | 2.0     | 1.0      | 1.0     |

---

### Project Standardization
**Completed:** 10:37

**Repository Structure:**
- Moved .pbix to `powerbi/` directory
- Created standard directories: `screenshots/`
- Added README.md, .gitignore, LICENSE
- Follows academic best practices template
- Ready for git version control

**Files Created:**
- `README.md` - Professional project documentation
- `.gitignore` - Power BI appropriate exclusions
- `LICENSE` - MIT License
- `powerbi/cycling-dashboard.pbix` - Final dashboard

---

### Summary
Successfully transformed 3 disparate data formats into unified 12-row dataset with consistent schema. Project now follows standardized academic template matching website-data best practices.

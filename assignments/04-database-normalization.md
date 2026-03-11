# Homework 3: Database Normalization

**Course:** TIF2242 – Database Systems  
**Instructor:** Dr. Guntur D Putra  
**Due Date:** Monday, 16 March 2026 at **07.59**

## Objectives
- Practice identifying repeating groups, partial and transitive dependencies.  
- Convert unnormalized relations to 1NF, 2NF, and 3NF.  
- Produce final relational schemas with primary keys, foreign keys, and constraints.  
- Implement the normalized schema as logical design.

## Instructions
For each given unnormalized table below:
- Identify the candidate key(s), repeating groups, and functional dependencies.  
- Produce the 3NF version.
- Provide the final relational schemas (table name, attributes, PK, FK).  
- Create the ERD for the updated logical design.

When you submit, include: a short explanation of each normalization step and the anomalies (insertion, update, deletion) eliminated by your design.

---

## Part 1 — Example Unnormalized Tables

### Example A — Orders

| OrderID | OrderDate  | CustomerName    | CustomerPhone | Items                                 | TotalAmount |
|---------|------------|-----------------|---------------|----------------------------------------|-------------|
| O1001   | 2026-03-01 | Alice Wijaya    | 081234567890  | (P01,2,$10),(P02,1,$25)                | 45.00       |
| O1002   | 2026-03-02 | Budi Santoso    | 082198765432  | (P03,1,$15)                            | 15.00       |
| O1003   | 2026-03-02 | Alice Wijaya    | 081234567890  | (P01,1,$10),(P04,3,$5)                 | 25.00       |

Tasks:
- Break this into appropriate tables and show PKs/FKs.
- Show how to remove redundancy and represent quantities/prices per order line.

---

### Example B — Employee Assignments

| EmpID | EmpName     | EmpPhone   | Projects                    | Skills               |
|-------|-------------|------------|-----------------------------|----------------------|
| E01   | Siti Nur     | 08111222333| (PR1,2025-01-01),(PR2,2025) | Java, SQL, Leadership|
| E02   | Joko Prabowo| 08112233444| (PR2,2025)                  | HTML, CSS            |

Tasks:
- Identify repeating attributes and propose normalized tables.
- Decide appropriate primary keys for many-to-many relationships.

---

### Example C — Library Borrowing

| BorrowID | BorrowerName | BorrowerCard | Book1Title       | Book1ISBN    | Book2Title        | Book2ISBN     | BorrowDate |
|----------|--------------|--------------|------------------|--------------|-------------------|---------------|------------|
| B900     | Rina Putri   | C100         | Database Systems | 978-1-23-45678 | Intro to SQL      | 978-0-11-22222 | 2026-02-25 |
| B901     | Ahmad Kurnia | C101         | Web Design       | 978-3-44-33333 | NULL              | NULL          | 2026-03-01 |

Tasks:
- Convert to a borrowing model where each borrowed book is a separate row in a BorrowedBooks table.
- Ensure the schema supports an arbitrary number of borrowed books per transaction.

---

## Part 2 — Deliverables
- A PDF containing: your ERD (Crow's Foot) of normalized schemas, brief explanation for each normalization step, and sample data showing correctness.

## Submission Instructions
- Submit a single PDF via eLOK. Include your name and student ID on the first page.  
- If you generated SQL files or dbdiagram links, include them as supplementary files or links inside the PDF.

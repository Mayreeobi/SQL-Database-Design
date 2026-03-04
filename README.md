# Database Design & Creation Projects

![MySQL](https://img.shields.io/badge/MySQL-Database-blue) ![SQL](https://img.shields.io/badge/SQL-Normalized%20Schemas-green)

A collection of normalized relational database systems built in MySQL, covering real-world operational domains. Each project follows Third Normal Form (3NF), enforces business rules at the database layer, and includes stored procedures, triggers, indexes, and analytical queries.

---

## Projects

| Project | Domain | Tables | Highlights |
|---|---|---|---|
| [Library Management System](library-management-system/) | Education | 6 | Automated inventory tracking, BorrowBook/ReturnBook procedures, views, SHA2 password hashing |
| [Hospital Management System](hospital-management-system/) | Healthcare | 7 | Department-doctor-patient-prescription chain, payment tracking, clinical reporting queries |


---

## Library Management System  

The Library Management System is designed to streamline and automate the processes involved in managing a library’s operations, including book tracking, student borrowing records, and author/genre categorization. This system ensures efficient book inventory management, real-time tracking of borrowed and returned books, and easy retrieval of student borrowing history. It improves the accuracy of record keeping, supports quick decision-making for acquisitions, and provides an organized structure for maintaining book-related data.

Tracks books, students, borrowing transactions, and staff — with inventory that updates automatically on every borrow and return.


### Objectives:
The core objective of the system is to:
    -  Manage and organize a large collection of books
    -  Track which books are issued, returned, or overdue
    -  Record information about students and their borrowing history
    -  Categorize books by genre and author
    -  Facilitate queries for library staff and users


**Key design decisions:**
- `CopiesAvailable` maintained in real time by `BorrowBook` and `ReturnBook` stored procedures
- `ReturnDate NULL` semantics cleanly represent currently borrowed books without a separate status column
- Trigger `trg_BeforeBorrowing` blocks invalid inserts at the database layer even if the stored procedure is bypassed
- Staff passwords stored as SHA2(256) hashes — never plain text


### Database Structure
The Library Management System is built on a relational database model. It consists of the following core tables:
 1. 📚 Students: Holds information about students who borrow books.
 2. 📖 Books: Stores details of books available in the library.
 3. ✍️ Authors: Stores information about authors of books.
 4. 🏷️ Genres: Holds the genres or categories of books.
 5. 📅 Borrowings: Tracks the borrowing and returning of books.

### 🧩 Entity Relationships
   - [Entity Relationship Diagram (ERD)](https://github.com/Mayreeobi/Brainwave_Matrix_Intern/blob/main/Library%20mgt%20EER.png)
   - One-to-Many: One student can borrow multiple books.
   - Many-to-One: Each book is written by one author and belongs to one genre.
   - One-to-Many: One author can write multiple books.
   - One-to-Many: One genre can include multiple books.

[View Project](https://github.com/Mayreeobi/Database-Creation/blob/main/librarymgt.sql)

---

## Hospital Management System

Manages the full patient care chain — departments, doctors, patients, appointments, prescriptions, and billing — in a single integrated schema.

**Key design decisions:**
- Table creation order determined by foreign key dependencies (Departments before Doctors, Patients before Appointments, etc.)
- `CHECK (Quantity > 0)` on Prescriptions and `CHECK (Amount >= 0)` on Payments enforce clinical and financial rules at the schema level
- `DEFAULT 'Scheduled'` on appointment status reduces manual data entry errors
- LEFT JOIN queries surface gaps — medications never prescribed, doctors with no appointments

### Database Structure
The HospitalMgt_db database is composed of several interconnected tables, each serving a specific purpose. Relationships between tables are established using primary and foreign keys to ensure data integrity and enable complex queries.
Here's a breakdown of each table:

1. 🏢 Departments Table: Stores information about the various departments within the hospital.
2. 🩺 Doctors Table: Contains information about the medical doctors and their specialties.
3. 👨‍⚕️ Patients Table: Stores demographic and contact information for all registered patients who receive medical care.
4. 📅 Appointments Table: Tracks appointments scheduled between patients and doctors.
5. 💊 Medications Table: Lists all available medications in the hospital.
6. 📝 Prescriptions Table: Records medications prescribed during an appointment.
7. 💳 Payments Table: Manages billing and payment information related to services rendered.


### 🧩 Entity Relationships
   - [Entity Relationship Diagram (ERD)](https://github.com/Mayreeobi/Brainwave_Matrix_Intern/blob/main/HosptialMgt_db.sql)
   - One-to-Many: One department can have many doctors.
   - One-to-Many: One doctor can have many appointments.
   - One-to-Many: One patient can have many appointments and payments.
   - Many-to-Many: Appointments and Medications are linked through Prescriptions.


[View Project](https://github.com/Mayreeobi/Database-Creation/blob/main/HosptialMgt_db.sql)


---

## Tech Stack

| Tool | Purpose |
|---|---|
| MySQL 8.0+ | Database engine for all three projects |
| SQL | Schema design, stored procedures, triggers, views, indexes, analytical queries |
| 3NF Normalization | Data modeling methodology |
| SHA2(256) | Password hashing (Library Management System) |

---

*Built by [Chinyere Obi](https://chinyereobi.netlify.app) - Data Analyst focused on building reliable data systems that enforce business rules at the source.*


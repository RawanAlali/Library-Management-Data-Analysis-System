# 📚 Library Management & Data Analysis System
A comprehensive SQL-based project demonstrating the complete data lifecycle—from database architecture to data seeding and complex business analytics.

📌 Project Overview
This project simulates a complete Library Management System. It is designed to handle book inventories, member registrations, borrowing transactions, 
and late-return fines while providing actionable insights into library usage patterns, popular book genres, and borrower behaviors.
---

* ** 🎯 Database Engine:** SQL Server Management Studio 
* **Tools Used:** SQL language

---

## 📁 Project Structure
* `1_schema.sql` - Creates the database tables and relations.
* `2_insert_data.sql` - Inserts sample data for testing.
* `3_analytics_queries.sql` - Contains SQL queries that answer business questions.

---

## 📐 Database Schema (ERD)

Below is the Entity Relationship Diagram (ERD) showing how the tables are connected:

![Database ERD Diagram](images/erd_diagram.png) <!-- 👈 Put your ERD image link here -->

## Main Tables:
1. **Books:** Stores book details and availability(isbn,book_title,category,rental_price,status,	author,publisher).
2. **Members:** Stores library members info(member_id,member_name,member_address,	reg_date).
3. **Issued_Books:** Tracks who borrowed which book and the issued dates(issued_id,	issued_member_id,issued_book_name,issued_date,issued_book_isbn	issued_emp_id).
4. **Return_Books:** Stores information about returnbook(return_id,issued_id,	return_book_name,return_date,return_book_isbn).
5. **Employee:** Stores library employee info(emp_id,emp_name,position,salary,branch_id).
6. **Branch:** Stores library branch info(branch_id,manager_id,branch_address,	contact_no) .


---

## 🛠️ Step 1: Creating Tables (DDL)

Here is a preview of the main tables and their relationships:
```sql
--create table issued_book_status

drop table if exists issued_book_status;
create table issued_book_status(
issued_id varchar(10) primary key,
issued_member_id  varchar(5) null,
issued_book_name varchar(55) null,
issued_date	 varchar(10) null,
issued_book_isbn varchar(25) null,	
issued_emp_id   varchar(10)
)

;

select * from issued_book_status

--change the type to make enable to make relation 
alter table issued_book_status
alter column issued_member_id  varchar(10)
--make relation between  issued_book_status and memebers
alter table issued_book_status
add foreign key (issued_member_id) 
REFERENCES members(member_id);

--make relation between  issued_book_status and books

alter table issued_book_status
add foreign key (issued_book_isbn) 
REFERENCES books(isbn);
--make relation between  issued_book_status and Employees

alter table issued_book_status
add foreign key (issued_emp_id) 
REFERENCES Employees(emp_id);

📥Step 2: Inserting Sample Data (DML)
We populated the database with test data to simulate real library operations.

BULK INSERT issued_book_status
FROM 'C:\Users\HP\Desktop\training\najirh_SQL project\Library System\issued_status.csv'
WITH
(
    FIELDTERMINATOR = ',', 
    ROWTERMINATOR = '\n',   
    FIRSTROW = 2             
);
📊 Step 3: Business Questions & SQL Solutions
❓ Question 1: What are the top 5 most borrowed books?
Goal: Find popular books to know which ones to buy more of.

💡 Key Insights & Recommendations
Popular Genres: Mystery and Fantasy are the most requested genres. The library should order more books in these categories.

Overdue Notifications: About 12% of books are returned late. Sending automated SMS/Email reminders 2 days before the due date can reduce late returns.

🤝 Connect with Me
If you have any questions or feedback about this project, feel free to reach out!

LinkedIn: [Your LinkedIn Profile URL]

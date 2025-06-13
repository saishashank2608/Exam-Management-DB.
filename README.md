# 🎓 University Examination System - Database Project

This project represents a **University Examination System** using SQL and Entity-Relationship design. It efficiently manages the data related to students, courses, departments, faculty members, exams, enrollments, and attendance.

---

## 📌 Project Overview

The goal of this project is to design and implement a relational database schema for a university’s examination management system. The system covers:

- Department-wise course offerings
- Faculty responsibilities
- Student enrollment and attendance
- Exam creation and attempt tracking

---

## 🧱 ER Design Description

### 🏢 Department
- Each department has a unique ID and name.
- Departments offer multiple courses.
- Each department is headed by a faculty member.

### 📚 Course
- Each course has a unique ID and name.
- Every course belongs to one department.
- Courses are taught and coordinated by faculty.

### 👨‍🏫 Faculty
- Faculty members have an ID and name.
- A faculty member can:
  - Teach multiple courses
  - Create exams
  - Head a department

### 🧑‍🎓 Student
- Each student has a unique roll number (ID) and name.
- A student belongs to one department.
- A student can enroll in multiple courses.
- For each course, attendance is recorded.
- Students can appear for multiple exams and have multiple attempts per exam.

### 📝 Exam
- Each exam is linked to a course and created by a faculty member.
- Contains fields like title, subject, date, duration, and type (internal/external).
- Students can attempt exams multiple times.

### 📊 Attendance
- Attendance is tracked per student per course.

---

## 🗂️ Tables and Relationships

### Student Table
```sql
CREATE TABLE Student (
    S_id INT PRIMARY KEY,
    S_Name VARCHAR(100),
    D_id INT,
    FOREIGN KEY (D_id) REFERENCES Department(D_id)
);
```

### Department Table
```sql
CREATE TABLE Department (
    D_id INT PRIMARY KEY,
    D_Name VARCHAR(100)
);
```

### Course Table
```sql
CREATE TABLE Course (
    C_id INT PRIMARY KEY,
    C_Name VARCHAR(100),
    D_id INT,
    FOREIGN KEY (D_id) REFERENCES Department(D_id)
);
```

### Faculty Table
```sql
CREATE TABLE Faculty (
    F_ID INT PRIMARY KEY,
    Faculty_Name VARCHAR(100)
);
```

### Teaches Table
```sql
CREATE TABLE Teaches (
    F_ID INT,
    C_id INT,
    FOREIGN KEY (F_ID) REFERENCES Faculty(F_ID),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);
```

### Exam Table
```sql
CREATE TABLE Exam (
    Exam_ID INT PRIMARY KEY,
    Subject VARCHAR(100),
    Type VARCHAR(50),
    Date DATE,
    Duration INT,
    Faculty_id INT,
    C_id INT,
    FOREIGN KEY (Faculty_id) REFERENCES Faculty(F_ID),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);
```

### Attendance Table
```sql
CREATE TABLE Attendance (
    S_id INT,
    C_id INT,
    Attendance_Percentage DECIMAL(5,2),
    PRIMARY KEY (S_id, C_id),
    FOREIGN KEY (S_id) REFERENCES Student(S_id),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);
```

### Enrollment Table (Recommended)
```sql
CREATE TABLE Enrollment (
    S_id INT,
    C_id INT,
    PRIMARY KEY (S_id, C_id),
    FOREIGN KEY (S_id) REFERENCES Student(S_id),
    FOREIGN KEY (C_id) REFERENCES Course(C_id)
);
```

---

## 📥 Sample Data Insertion

```sql
-- Department
INSERT INTO Department (D_id, D_Name) VALUES
(1, 'Computer Science'),
(2, 'Mechanical Engineering'),
(3, 'Electrical Engineering');

-- Student
INSERT INTO Student (S_id, S_Name, D_id) VALUES
(101, 'Ravi Kumar', 1),
(102, 'Anita Sharma', 2),
(103, 'Mohit Verma', 3);

-- Course
INSERT INTO Course (C_id, C_Name, D_id) VALUES
(201, 'Data Structures', 1),
(202, 'Thermodynamics', 2),
(203, 'Circuit Theory', 3);

-- Faculty
INSERT INTO Faculty (F_ID, Faculty_Name) VALUES
(301, 'Dr. Ramesh'),
(302, 'Prof. Neha'),
(303, 'Dr. Singh');

-- Teaches
INSERT INTO Teaches (F_ID, C_id) VALUES
(301, 201),
(302, 202),
(303, 203);

-- Exam
INSERT INTO Exam (Exam_ID, Subject, Type, Date, Duration, Faculty_id, C_id) VALUES
(401, 'Data Structures', 'Internal', '2025-06-20', 90, 301, 201),
(402, 'Thermodynamics', 'External', '2025-06-22', 120, 302, 202),
(403, 'Circuit Theory', 'Internal', '2025-06-24', 60, 303, 203);

-- Attendance
INSERT INTO Attendance (S_id, C_id, Attendance_Percentage) VALUES
(101, 201, 85.50),
(102, 202, 78.25),
(103, 203, 92.00);

-- Enrollment
INSERT INTO Enrollment (S_id, C_id) VALUES
(101, 201),
(102, 202),
(103, 203);
```

---

## 🧠 Learning Objectives

- Understand and apply **ER modeling** principles
- Practice **SQL table creation** with foreign keys
- Handle **many-to-many** relationships (Student-Course, Faculty-Course)
- Insert and query **relational data** effectively

---

## ✅ Future Enhancements

- Add `Marks` and `Attempt` tracking for each exam attempt
- Introduce `HeadOfDepartment` field in Department referencing Faculty
- Create views and stored procedures for exam reports and attendance summaries

---

## 🛠️ Tools Used

- SQL (MySQL or SQLite)
- ER Modeling (draw.io or similar

![image](https://github.com/user-attachments/assets/554587db-d31d-4124-b682-a01f8830d1f9)

![image](https://github.com/user-attachments/assets/bad2da6f-7a53-43ea-b230-8241aca0d4dc)



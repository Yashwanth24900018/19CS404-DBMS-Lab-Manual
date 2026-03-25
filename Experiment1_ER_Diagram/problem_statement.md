# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

<img width="541" height="250" alt="image" src="https://github.com/user-attachments/assets/5f162258-3ad9-4bce-8190-fbf387a8759b" />


### Entities and Attributes

| Entity      | Attributes (PK, FK)                                             | Notes                          |
|-------------|------------------------------------------------------------------|--------------------------------|
| MEMBER      | MemberID (PK), Name, MembershipType, StartDate                  | Stores member details          |
| PROGRAM     | ProgramID (PK), ProgramName                                     | Fitness programs               |
| TRAINER     | TrainerID (PK), Name, Specialization                            | Trainer details                |
| SESSION     | SessionID (PK), Date, Time, MemberID (FK), TrainerID (FK)       | Personal training sessions     |
| PAYMENT     | PaymentID (PK), Amount, Date, MemberID (FK)                     | Membership & session payments  |
| ATTENDANCE  | AttendanceID (PK), SessionID (FK), Status                       | Attendance tracking            |

### Relationships and Constraints

| Relationship            | Cardinality | Participation | Notes                                      |
|------------------------|------------|--------------|--------------------------------------------|
| MEMBER – PROGRAM       | M:N        | Total        | Members can join multiple programs         |
| PROGRAM – TRAINER      | M:N        | Total        | Programs can have multiple trainers        |
| MEMBER – TRAINER       | M:N        | Partial      | Through SESSION entity                     |
| SESSION – ATTENDANCE   | 1:1        | Total        | Each session has attendance                |
| MEMBER – PAYMENT       | 1:M        | Total        | One member can make many payments          |

### Assumptions
- A member can enroll in multiple fitness programs at the same time.
- Personal training sessions are optional and scheduled between one member and one trainer.
- Payments include both membership fees and personal training session charges.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

<img width="539" height="186" alt="image" src="https://github.com/user-attachments/assets/b4983078-b710-412b-bc2b-2c888b243f17" />


### Entities and Attributes

| Entity    | Attributes (PK, FK)                                                | Notes                      |
|-----------|---------------------------------------------------------------------|----------------------------|
| MEMBER    | MemberID (PK), Name                                                | Library members            |
| BOOK      | BookID (PK), Title, Author, Category                               | Book details               |
| LOAN      | LoanID (PK), LoanDate, ReturnDate, MemberID (FK), BookID (FK)      | Borrow records             |
| EVENT     | EventID (PK), Name, Date                                           | Library events             |
| SPEAKER   | SpeakerID (PK), Name                                               | Event speakers             |
| ROOM      | RoomID (PK), RoomName                                              | Rooms for events/study     |
| FINE      | FineID (PK), Amount, LoanID (FK)                                   | Late return fines          |

### Relationships and Constraints

| Relationship        | Cardinality | Participation | Notes                                      |
|--------------------|------------|--------------|--------------------------------------------|
| MEMBER – BOOK      | M:N        | Partial      | Via LOAN entity                            |
| EVENT – SPEAKER    | M:N        | Total        | Events have one or more speakers           |
| EVENT – ROOM       | M:1        | Total        | Each event assigned one room               |
| LOAN – FINE        | 1:1        | Partial      | Only for overdue returns                   |
| MEMBER – EVENT     | M:N        | Partial      | Members can register for events            |

### Assumptions

- A book can be borrowed multiple times but only by one member at a time.
- Fines are generated only if the book is returned after the due date.
- Each event is conducted in a single room but can have multiple speakers.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="547" height="248" alt="image" src="https://github.com/user-attachments/assets/14e3fb9a-c3ec-4e9d-adb3-d404c22bf680" />


### Entities and Attributes

| Entity        | Attributes (PK, FK)                                                  | Notes                      |
|---------------|------------------------------------------------------------------------|----------------------------|
| CUSTOMER      | CustomerID (PK), Name                                                 | Customer details           |
| RESERVATION   | ReservationID (PK), Date, Time, Guests, CustomerID (FK)              | Table booking              |
| TABLE         | TableID (PK), Capacity                                                | Restaurant tables          |
| WAITER        | WaiterID (PK), Name                                                   | Staff details              |
| ORDER         | OrderID (PK), ReservationID (FK)                                      | Food orders                |
| DISH          | DishID (PK), Name, Category                                           | Menu items                 |
| ORDER_ITEM    | OrderID (FK), DishID (FK), Quantity                                   | Order details (junction)   |
| BILL          | BillID (PK), TotalAmount, ReservationID (FK)                          | Final billing              |

### Relationships and Constraints

| Relationship              | Cardinality | Participation | Notes                                      |
|--------------------------|------------|--------------|--------------------------------------------|
| CUSTOMER – RESERVATION   | 1:M        | Total        | One customer can have many reservations    |
| RESERVATION – TABLE      | M:1        | Total        | Each reservation has one table             |
| RESERVATION – WAITER     | M:1        | Total        | Each reservation assigned a waiter         |
| RESERVATION – ORDER      | 1:M        | Total        | Multiple orders per reservation            |
| ORDER – DISH             | M:N        | Total        | Via ORDER_ITEM                             |
| RESERVATION – BILL       | 1:1        | Total        | One bill per reservation                   |

### Assumptions

- Walk-in customers are also recorded in the system as customers.
- Each reservation is assigned to exactly one table and one waiter.
- A single bill is generated per reservation including all orders and charges.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**

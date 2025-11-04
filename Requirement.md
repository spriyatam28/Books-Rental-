# Requirements for Library Management System

##  Primary Goals:

- Apply OOP in a layered architecture
- Build REST APIs with Spring Boot + JPA
- Write Unit tests with JUnit and Integration tests
- Design so it can scale up to 3000 RPS (read-heavy workload)

--- 

## Functional Requirements:

### Admin:

1. Can create, update and list all the books
2. Can view user profile, restrict or block them
3. Can view and report all the list of books with overdue books returns and view active borrowing
4. Can pardon penalty
5. Can _promote_ and _demote_ a user to **Premium** or **Normal** or **Bad** borrower
6. Can permanently **Ban** users

### User:

1. Can register with email and password
2. Can borrow a book for upto 14 days and max. of 5 books
3. ***Normal*** user status by default
4. Can borrow only 3 books for the first month

### Policies:

1. Return borrowed books based on user level:
   1. Premium: Upto 24 days
   2. Normal: Upto 14 days
   3. Bad: 4 days
2. If a user accumulates 5 penalties, they will get demoted if they return all the books else, permanent ban
   1. From Premium to Normal: 3 penalities
   2. From Normal to Bad: 5 penalities
   3. Bad to Ban: 1 penality
   4. If a user borrow window is overdue for _30_ days: **Ban**
   5. If a **Premium** user **overdue** for over _15_ days: Bad
   6. If a **Normal** user **overdue** for 5 days: _Bad_ or _Ban_ if exceeded 10 days
3. Promotion Rules:
   1. Normal to Premium: 
      1. User for over a year and borrowed at least 60 books and returned all in due time, if there is no history of Bad
      2. Or borrowed 150 books over 6 months and returned all in due time, if there is no history of Bad
      3. If there is history, borrowed at least 200 books for over 2 years and returned all within due time
      4. Or borrowed at least 300 over a span of 1.5 years and returned all within due time
   2. Bad to Normal: 
      1. Borrowed 60 books within 6 months and returned all within due time
      2. Or Borrowed 100 books within 1 year and returned all within due time
   3. A user can never get promoted from Bad to Premium directly. 
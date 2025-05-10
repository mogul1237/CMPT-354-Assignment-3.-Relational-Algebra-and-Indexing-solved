# CMPT-354-Assignment-3.-Relational-Algebra-and-Indexing-solved

Download Here: [CMPT 354 Assignment 3. Relational Algebra and Indexing solved](https://jarviscodinghub.com/assignment/assignment-3-relational-algebra-and-indexing-solution/)

For Custom/Original Work email jarviscodinghub@gmail.com/whatsapp +1(541)423-7793

Objectives

In this assignment, you need to complete two tasks. In Task 1, you will be trained to write relational algebra queries. In Task 2, you will be trained to create indexes to speed up query performance.

In addition, you will get familiar with LaTeX (the de facto standard for the communication and publication of scientific documents), and learn more features about jupyter notebook.

Download A3.zip. Answer the questions in A3.ipynb.

Task 1. Relational Algebra (10 points)

You will use the similar bank database with A2. But with more tables and colomns. The database has 7 tables. The following shows their schemas.

Customer = {customerID, firstName, lastName, brithDate, income}
Account = {accNumber, type, balance, branchNumberFK-Branch}
Owns = {customerIDFK-Customer, accNumberFK-Account}
Transactions = {transNumber, accNumberFK-Account, amount, date, description}
Employee = {sin, firstName, lastName, salary, startDate, branchNumberFK-Branch}
PersonalBanker = {customerIDFK-Customer, sinFK-Employee}
Branch = {branchNumber, branchName, street, numberEmployees, managerSINFK-Employee, budget}

Write relational algebra queries to answer questions (1) to (10). Your answer to each question should consist of a single relational algebra query. You may use input relation names to differentiate between attributes with the same name in the results of a join or Cartesian product (such as referring to Employee.firstName or Customer.firstName in the results of the Cartesian product of Employee and Customer).

Preliminary
To write a relational algebra query in a cell, please first switch the cell to the Markdown cell. Then, you can type LaTeX equations in the cell. Here is a list of common symbols used by relational algebras.

Selection (σσ)
Projection (ππ)
Union (∪∪)
Intersect (∩∩)
Set Difference (−−)
Cross Product (××)
Rename (ρρ)
Join (⋈⋈)
Conjunction (∧∧)
Disconjunction (∨∨)
Greater Than or Equal To (≥≥)
Less Than or Equal To (≤≤)

Next, I am going to show you some RA queries. You can use them as training examples to learn how to write an RA query using latex equations.

Example 1. sID of all students who have earned some grade over 80 and some grade below 50. (See Slide 34)

πsID(σgrade80(Took))∩πsID(σgrade<50(Took))πsID(σgrade80(Took))∩πsID(σgrade<50(Took))

Example 2. Student number of all students who have taken CMPT 354 (See Slide 35)

πsID(σOffering.oID=Took.oID∧cNum=354(Offering×Took))πsID(σOffering.oID=Took.oID∧cNum=354(Offering×Took))

Example 3. The names of all students who have passed a breadth course (grade = 60 and breadth = True) with Martin (See Slide 44)

πlastName,firstName(σbreadth=True∧grade≥60∧instructor=′Martin′(Student⋈Took⋈Offering⋈Course))πlastName,firstName(σbreadth=True∧grade≥60∧instructor=′Martin′(Student⋈Took⋈Offering⋈Course))

Queries (1 point per question)

1. The customer IDs, first names, last names and incomes of customers who have an account at a branch with a budget no more than $1,000,000

REPLACE WITH YOUR ANSWER

2. The first and last names of customers who were born after 1st of January 1985 and whose income is less than $75,000.

REPLACE WITH YOUR ANSWER

3. The SINs, first and last names and salaries of employees who are both personal bankers and managers

REPLACE WITH YOUR ANSWER

4. The customer IDs of customers who own a joint account (an account that is owned by more than one customer)

REPLACE WITH YOUR ANSWER

5. The customer IDs of customers whose accounts have no transactions with amounts of which the absolute value is less than $5,000 (i.e. all their transactions are either greater than or equal to $5,000 or less than or equal to -$5,000).

REPLACE WITH YOUR ANSWER

6. The branch names of branches that employ at least one employee whose last name is “Martin”, and at least one employee whose last name is “Wang”; note that branch name is not a candidate key

REPLACE WITH YOUR ANSWER

7. The SINs and salaries of employees who earn more than the manager of their branch

REPLACE WITH YOUR ANSWER

8. The first names, last names and birth dates of customers who own an account in the Vancouver branch and the first names, last names and start dates of employees who work in the Vancouver branch (i.e. one query that returns one list of first and last names and dates of these 2 groups of people)

REPLACE WITH YOUR ANSWER

9. The customer IDs of customers who have personal bankers in either the Vancouver or Metrotown branches (note that the personal bankers must be distinct employees as an employee only works at one branch)

REPLACE WITH YOUR ANSWER

10. You are to find the SINs, and first and last names of employees who own an account in the branch in which they work.

REPLACE WITH YOUR ANSWER

Task 2. Indexing (10 points)

In this task, you will be asked to i) select suitable indexes to speed up query performance and ii) examine the query plan of an SQL query.

We are going to use a new database called flights.db. You can find it in A3.zip. In the database, there is a single table, called FLIGHTS. The following shows its schema:

FLIGHTS (fid, year, month_id, day_of_month, day_of_week_id, carrier_id, flight_num, origin_city, origin_state, dest_city, dest_state, departure_delay, taxi_out, arrival_delay, canceled, actual_time, distance)

Note that this task only needs to use four attributes: carrier_id, origin_city, actual_time, and dest_city.

Questions

1. Consider the following queries:

sqlite
(a): SELECT DISTINCT carrier_id
FROM Flights
WHERE origin_city = ‘Seattle WA’ AND actual_time <= 180;
sqlite
(b): SELECT DISTINCT carrier_id
FROM Flights
WHERE origin_city = ‘Gunnison CO’ AND actual_time <= 180;
sqlite
(c): SELECT DISTINCT carrier_id
FROM Flights
WHERE origin_city = ‘Seattle WA’ AND actual_time <= 30;

Choose one single simple index (index on one attribute) that is most likely to speed up all three queries. Write down the CREATE INDEX statement and explain why you chose that index below.

What is the CREATE INDEX statement (1 point)?REPLACE WITH YOUR ANSWER
Why did you choose the index (1 point)?REPLACE WITH YOUR ANSWER

Open a command line shell and start the sqlite program. Connect to the provided flights.db, and check whether the FLIGHTS table has the index that you indicate above. If not, add this index to the FLIGHTS table.

Does the FLIGHTS table has the index that you indicate above (0.5 points)?REPLACE WITH YOUR ANSWER

Please check whether each query used the index or not. Hint: you can use EXPLAIN QUERY PLAN … to see the query plan of each query.

Did Query (a) use the index? (0.5 point)?REPLACE WITH YOUR ANSWER
Did Query (b) use the index? (0.5 point)?REPLACE WITH YOUR ANSWER
Did Query (c) use the index? (0.5 point)?REPLACE WITH YOUR ANSWER

2. Consider this query:

sqlite
(d): SELECT DISTINCT F2.origin_city
FROM Flights F1, Flights F2
WHERE F1.dest_city = F2.dest_city
AND F1.origin_city=’Gunnison CO’
AND F1.actual_time <= 30;

Choose one simple index (index on one attribute), different from the index for the question above, that is likely to speed up this query. Write down the CREATE INDEX statement and explain why you chose that index as a SQL comment.

What is the CREATE INDEX statement (1 point)?REPLACE WITH YOUR ANSWER
Why did you choose the index (1 point)?REPLACE WITH YOUR ANSWER

Connect to the provided flights.db, and check whether the FLIGHTS table has this second index that you indicate above. If not, add this index to the FLIGHTS table.

Does the FLIGHTS table has the index that you indicate above (0.5 points)?REPLACE WITH YOUR ANSWER

Please check whether the query used this second index or not.

Did Query (d) use this second index? (0.5 point)?REPLACE WITH YOUR ANSWER

3. Now we want to know how effective the two indexes are. We compare the runtimes of the queries with and without indexes. Hint: use timer on to turn SQL timer on.

Execute queries (a) – (b) on the FLIGHTS table that do not have the two indexes. Please create a screenshot for the runtime of each query. I’ve put my screenshots below. You can find them in the runtime folder in the A3.zip. Please replace them with yours. (1.5 points)

Execute queries (a) – (b) on the FLIGHTS table that has the two indexes. Please create a screenshot for the runtime of each query. I’ve put my screenshots below. Please replace them with yours. (1.5 points)

Submission

Download A3.zip. Answer the questions in A3.ipynb. Put A3.ipynb and the runtime folder into A3-submission.zip. Please note that i) you need to update the runtime folder with your screenshots of the query runtimes; ii) you do not need to put the flights.db into A3-submission.zip.

Submit A3-submission.zip to the CourSys activity Assignment 3

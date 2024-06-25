## Project: Analysing Student's Mental Health (SQL Beginner)

Link to workbook: https://www.datacamp.com/datalab/w/7f13d06f-b411-4eeb-b6f8-635bcfac81b5/edit

## Does going to university in a different country affect your mental health?

A Japanese international university surveyed its students in 2018 and published a study the following year that was approved by several ethical and regulatory boards.

The study found that international students have a higher risk of mental health difficulties than the general population, and that social connectedness (belonging to a social group) and acculturative stress (stress associated with joining a new culture) are predictive of depression.

## Exploring the `students` Data Using PostgreSQL

To find out if you would come to a similar conclusion for international students and see if the length of stay is a contributing factor, we will explore the `students` data.

### Data Description

Here is a description of the columns you may find helpful:

| Field Name     | Description                                      |
| -------------- | ------------------------------------------------ |
| `inter_dom`    | Types of students (international or domestic)    |
| `japanese_cate`| Japanese language proficiency                    |
| `english_cate` | English language proficiency                     |
| `academic`     | Current academic level (undergraduate or graduate)|
| `age`          | Current age of student                           |
| `stay`         | Current length of stay in years                  |
| `todep`        | Total score of depression (PHQ-9 test)           |
| `tosc`         | Total score of social connectedness (SCS test)   |
| `toas`         | Total score of acculturative stress (ASISS test) |

### SQL Queries

Run this code to view a sample of the data in students:

```sql
SELECT * 
FROM students
LIMIT 10;
```

![image](https://github.com/NguyenMav/DataCamp_SQL_Beginner_Mental_Health/assets/149219810/740fc75f-7902-46a6-ae13-488b9d9a8afa)


Return a table with nine rows and five columns. The five columns should be aliased as: stay, count_int, average_phq, average_scs, and average_as, in that order. The average columns should contain the average of the todep (PHQ-9 test), tosc (SCS test), and toas (ASISS test) columns for each length of stay, rounded to two decimal places. The count_int column should be the number of international students for each length of stay. Sort the results by the length of stay in descending order.

Here's the SQL code according to the requirements of this project:

```sql
SELECT stay, COUNT(stay) AS count_int, ROUND(AVG(todep), 2) AS average_phq, ROUND(AVG(tosc), 2) AS average_scs, ROUND(AVG(toas), 2) AS average_as
FROM students 
WHERE inter_dom = 'Inter'
GROUP BY stay
ORDER BY stay DESC
LIMIT 9;
```

| stay | count_int | average_phq | average_scs | average_as |
|------|-----------|-------------|-------------|-------------|
| 10   | 1         | 13          | 32          | 50          |
| 8    | 1         | 10          | 44          | 65          |
| 7    | 1         | 4           | 48          | 45          |
| 6    | 3         | 6           | 38          | 58.67       |
| 5    | 1         | 0           | 34          | 91          |
| 4    | 14        | 8.57        | 33.93       | 87.71       |
| 3    | 46        | 9.09        | 37.13       | 78          |
| 2    | 39        | 8.28        | 37.08       | 77.67       |
| 1    | 95        | 7.48        | 38.11       | 72.8        |


### Thought Process
1. Write out SELECT, FROM first.
2. Add in the five fields (columns) and add LIMIT for only 9 entries (rows).
3. Use the AVG function on three of the fields, and alias (AS) three of the fields in that particular order.
4. Use the ROUND function to two decimal places for the average fields.
5. Use the COUNT function to count up all the students for each stay.
6. Use GROUP BY to group entries with the same length of stay together.
7. Sort the entries in descending order of the stay field, from highest to lowest.
8. Specify only international students by using WHERE to filter for inter_dom = 'Inter'.
9. This took me about ~5 attempts to fix all the errors and misspellings. I made sure to test the SQL by running it at roughly each step.

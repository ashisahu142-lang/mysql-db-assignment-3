# Database notes

## Assumed schema

The source assignment names an `employees` table and refers to these fields: `first_name`, `last_name`, `salary`, `department_id`, `hire_date`, and `job`. The assignment does not supply a schema definition. The reproducible test schema uses:

| Column | MySQL type | Purpose |
|---|---|---|
| `employee_id` | `INT PRIMARY KEY` | Test data row identifier; not used by the answers |
| `first_name` | `VARCHAR(50)` | Employee given name |
| `last_name` | `VARCHAR(50)` | Employee family name |
| `salary` | `DECIMAL(10,2)` | Salary amount, with cents |
| `department_id` | `INT` | Department number |
| `hire_date` | `DATE` | Employee hire date |
| `job` | `VARCHAR(50)` | Job/designation text |

A class database may use a different job field name (such as `job_id`) or store job labels in another table. Adapt the relevant queries to the schema actually provided by the course. These solutions follow the question wording by assuming a text column named `job` with values such as `Programmer` and `Shipping Clerk`.

## Test data

`sql/00-setup-sample-data.sql` creates database `mysql_db_assignment_3`, creates `employees` only when absent, and inserts eight illustrative rows with `INSERT IGNORE`. It does not drop or replace existing tables. Values are designed to exercise the filters (departments 30/100, salary boundary values, 1987 hire dates, names with both `b` and `c`, six-character surnames, and named jobs/surnames). This is synthetic practice data, not a transcription of an official HR dataset.

## Dependencies and execution order

- MySQL 8.0 or compatible MySQL SQL client/server.
- Run `sql/00-setup-sample-data.sql` first in a fresh assignment test database. The script is non-destructive; if an incompatible `employees` table already exists, review it and select another test database rather than deleting it.
- Then run any `sql/01-question.sql` through `sql/11-question.sql` independently. Each answer is a read-only `SELECT` and expects the current database to be `mysql_db_assignment_3` or another database containing the assumed table.

## Interpretation assumptions

- Question 2's unspecified ascending sort key is interpreted as ascending `department_id`.
- The salary range in Questions 1 and 3 is inclusive at both ends, matching MySQL `BETWEEN` semantics.
- Question 4 uses a half-open date interval from 1987-01-01 up to, but not including, 1988-01-01.
- Letter matching is case-insensitive using `LOWER` or `UPPER`.
- Question 9 returns each distinct non-NULL job once.
- Question 10 calculates PF as the unrounded expression `salary * 0.15`; display rounding depends on the client.
- No sub-questions or additional tables appear in the source document.

## Validation

All 11 solutions received static syntax/numbering review. Runtime testing was not possible in this environment because no MySQL client or server executable was found.

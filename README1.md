# Book Store SQL

A simple collection of SQL schema, sample data and useful queries for a bookstore database. This repository contains SQL scripts to create the schema, seed sample data, and run common queries and reports.

Contents
- sql/                — SQL scripts (schema, seeds, queries)
- data/               — optional sample data files (CSV, JSON)
- docs/               — documentation and ER diagram (ER_DIAGRAM.md)
- README.md           — this file

Quick start
1. Clone the repository:

       git clone https://github.com/anish-murshetwar/Book-Store-SQL.git
       cd Book-Store-SQL

3. Run the schema and seed scripts locally.

SQLite example:
- Create a database and run schema + seed:

        sqlite3 bookstore.db < sql/schema.sql
        sqlite3 bookstore.db < sql/seeds.sql

PostgreSQL example:
- Create a database and run scripts (replace DBNAME and USER):

        psql -U USER -d DBNAME -f sql/schema.sql
        psql -U USER -d DBNAME -f sql/seeds.sql

What to run (typical order)
1. sql/schema.sql   — creates tables and constraints
2. sql/seeds.sql    — seeds sample data (optional)
3. sql/queries.sql  — example queries and reports

ER diagram
See docs/ER_DIAGRAM.md for the database entity-relationship diagram and instructions for updating it also here is a preview.

<img width="1268" height="899" alt="DatabaseE-R" src="https://github.com/user-attachments/assets/d7b57b22-ca18-4aa1-8022-37a9074478b7" />


Notes
- The SQL scripts aim to be database-agnostic but may include dialect-specific parts. Check the top of each file for target DB hints.
- Do not commit sensitive production data. Use anonymized or synthetic sample data for examples.

Contributing
- Open an issue or pull request with schema improvements, additional queries, or sample data.
- When adding scripts, include a short README in sql/ describing the purpose and order.


Contact
Maintainer: anish-murshetwar

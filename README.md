# SQL Migration tool
SQL Migration tool that converts MySQL, Postgre, etc. to MSSQL - Custom tool I made for specific projects


# Database Migration Tool

## Description

The Database Migration Tool is a comprehensive solution designed for migrating database schemas and data between various relational database management systems (RDBMS), including MySQL, PostgreSQL, and MSSQL, and supports cloud database platforms like AWS RDS, Azure SQL, and Google Cloud SQL.

This tool performs the following tasks:
- Schema Conversion: Converts schemas from MySQL/PostgreSQL to MSSQL format.
- Data Migration: Migrates data (tables and `INSERT INTO` statements) from source to target.
- Conflict Resolution: Handles schema mismatches and data integrity issues.
- Data Transformation: Allows user-defined transformations (e.g., normalizing formats, adjusting data).
- Scheduling: Automates periodic migrations using cron jobs or task schedulers.

---

## Features
- Advanced Schema Conversion:
  - Converts MySQL/PostgreSQL data types to MSSQL (e.g., `VARCHAR` to `NVARCHAR`, `TEXT` to `NTEXT`, etc.).
  - Converts primary/foreign keys, indexes, constraints, and default values.
  - Transforms stored procedures and triggers from MySQL/PostgreSQL to MSSQL-compatible formats.

- Data Migration:
  - Migrates both schema and data from the source database to MSSQL.
  - Supports incremental migration (migrating only new or modified records).
  
- Cloud Database Support:
  - Supports cloud platforms such as AWS RDS, Azure SQL, and Google Cloud SQL.
  
- Conflict Resolution:
  - Resolves issues like column name conflicts, data type mismatches, and missing constraints.

- Data Transformation:
  - Allows user-defined transformations to the data during migration (e.g., date formatting, text adjustments).
  
- Scheduling:
  - Integrates with cron jobs (Linux/macOS) and Task Scheduler (Windows) for periodic migrations.

---

## Installation

### Prerequisites
1. ODBC Drivers:
   - Ensure you have the ODBC drivers for MySQL, PostgreSQL, and MSSQL installed.
     - For MSSQL: `ODBC Driver 17 for SQL Server`.
     - For MySQL/PostgreSQL: Ensure the appropriate ODBC drivers are installed.

2. Database Credentials:
   - Access credentials for your source and target databases (including cloud databases).

3. C++ Development Environment:
   - Make sure you have a C++ compiler and ODBC libraries (`sql.h`, `sqlext.h`) set up for compilation.

---

## Usage

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/database-migration-tool.git
cd database-migration-tool
```

### 2. Build the Script

If you're on Linux, use `g++` to compile the script:

```bash
g++ -o sql_migration_tool sql_migration_tool.cpp -lodbc
```

For Windows, make sure you have the ODBC libraries linked properly in your IDE or with `MinGW`.

### 3. Running the Script

Run the migration tool by providing the path to your SQL input file (`input.sql`):

```bash
./sql_migration_tool input.sql
```

### 4. Scheduling Migrations

You can schedule the script to run periodically using cron jobs (Linux/macOS) or Task Scheduler (Windows).

Linux/macOS (cron job):
To run the migration every day at midnight, add the following line to your crontab file (`crontab -e`):

```bash
0 0 * * * /path/to/sql_migration_tool ./input.sql
```

Windows (Task Scheduler):
- Open Task Scheduler.
- Create a new task that runs the `sql_migration_tool.exe` at your desired frequency.

---

## Cloud Database Support

The tool supports migrating to/from cloud databases like AWS RDS, Azure SQL, and Google Cloud SQL. When connecting to a cloud database, make sure to use the appropriate connection string.

For example:
- AWS RDS (MySQL):
    ```plaintext
    "DRIVER={MySQL ODBC 8.0 Driver};SERVER=aws-db-instance.rds.amazonaws.com;DATABASE=testdb;USER=username;PASSWORD=password;"
    ```
- Azure SQL:
    ```plaintext
    "DRIVER={ODBC Driver 17 for SQL Server};SERVER=yourserver.database.windows.net;DATABASE=testdb;UID=username;PWD=password;"
    ```
- Google Cloud SQL:
    ```plaintext
    "DRIVER={ODBC Driver 17 for SQL Server};SERVER=your-cloud-instance.db.google.com;DATABASE=testdb;UID=username;PWD=password;"
    ```

---

## Conflict Resolution

The script automatically resolves certain schema conflicts, such as column name mismatches and data type differences between the source and target databases. You can customize the conflict resolution logic based on specific requirements.

For example, if the source and target databases have a column with different names, the script can rename columns automatically or log the conflict for manual resolution.

---

## Data Transformation

The script allows user-defined transformations on data during the migration process. Common transformations include:
- Normalizing date formats (e.g., changing `MM-DD-YYYY` to `YYYY-MM-DD`).
- String adjustments (e.g., converting text to uppercase or lowercase).

Example:
```cpp
std::string transformData(const std::string& data, const std::string& transformRule) {
    if (transformRule == "normalize_date") {
        // Apply date transformation logic
    }
    return data;
}
```

---

## Scheduling Migrations

You can automate migrations using cron jobs (Linux/macOS) or Task Scheduler (Windows). This allows you to perform regular data migrations or synchronize data between databases on a schedule.

Example cron job (Linux/Mac):
```bash
0 0 * * * /path/to/sql_migration_tool ./input.sql
```

---

## Advanced Features

### 1. Incremental Migration
- The script supports incremental migration, migrating only data that has been modified since the last migration. This is useful for keeping databases synchronized without migrating all the data every time.

### 2. Multi-Database Support
- The tool can handle different database systems (MySQL, PostgreSQL, MSSQL) and migrate between them. It includes automatic conversions for data types and schema objects like tables, indexes, and constraints.

### 3. Scheduling
- The script allows you to schedule regular database migrations through cron jobs (Linux/Mac) or Task Scheduler (Windows), enabling automation for recurring migration tasks.

---

## Contributing

Feel free to open issues or submit pull requests for any bugs, improvements, or additional features you'd like to see.

1. Fork the repository and create your branch.
2. Make your changes and write tests.
3. Commit your changes.
4. Push your changes to your fork.
5. Create a pull request to the main repository.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### Contact
If you have any questions or suggestions, please feel free to reach out to the project maintainers or open an issue on GitHub.

---

### Example Use Case

1. Step 1: Create an `input.sql` file containing the source database schema and data.
2. Step 2: Run the tool to convert the schema and migrate the data to a new database:
    ```bash
    ./sql_migration_tool input.sql
    ```
3. Step 3: If desired, schedule the migration to run periodically using cron or Task Scheduler.

---

This script is a powerful solution for automating complex database migrations, including data transformation, conflict resolution, and cloud integration. It is ideal for use in environments where regular database synchronization or migration tasks are needed.

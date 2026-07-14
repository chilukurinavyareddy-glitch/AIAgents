# Discovery Plugin: SQL Server

Plugin id: `sqlserver-discovery`

Use when the project uses SQL Server.

Detect:

- SQL scripts, migrations, stored procedures, functions, views, triggers
- connection strings and database config references
- ORM mappings, repositories, raw SQL usage
- seed data and baseline scripts

Output notes:

- identify schema impact
- identify migration and rollback needs
- identify stored procedure parity risks
- map entities for rewrite planning

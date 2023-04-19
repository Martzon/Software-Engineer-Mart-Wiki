A class that is responsible for data access; Each entity or table should have its corresponding data gateway. This also exercises the Single Responsibility Principle. Data gateways should:
- Contain only codes that access the database; For example SqlConnection, SqlCommand classes that execute your queries.
- Not contain any unnecessary logic
- Depend from the SQL command factory class for building commands/queries it executes

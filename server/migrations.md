# Migrations

Migrations allow us to define a certain schema in time of the database: tables, columns, format whithin each of these.
For the server to run, no migration must be pending: use `npm run migrate` to run pending migrations.

## Create a migration

Use the command `npm run new_migration --name=$YOUR_AWESOME_MIGRATION_NAME`, a new file with your migration will appear in `src/migrations`.  
Within the file, a function is defined. Write the steps necessary to perform the migration inside of it.  
Use the provided `tx` transaction object to perform all changes: new table, table modification, record alteration. Make sure to `await` all calls.

### Create a table

Have a copy of the ORM class in the migration: this is the schema known at the time of migrating. This allows the migrations to be fully uncorrelated from heavy modifications of the source code. Do not import ORM classes into your migrations!  
Make sure the ORM class for the migration is indicated as `@Entity({schema: true})`.  
Within the migration body, perform `await tx.create_table(ORMClass)` to create the table `ORMClass`, for example.

### Add or remove a column

Have a copy of the ORM class in your migration, including as members the columns to add or remove.  
Simply invoke `await tx.add_columns(ORMClass, 'column1', 'column2')` and so on to add the columns `'column1'` and `'column1'` as specified in the ORM model.  
Invoke `await tx.remove_columns(ORMClass, 'column1', 'column2')` and so on to remove the columns `'column1'` and `'column1'` as specified in the ORM model.

# cannot ALTER TABLE "table" because it has pending trigger events

When you're altering a Postgres table, and this error occurs while you're not expecting
it, it can have (at least) two causes:

1. A column was added with 'NOT NULL' and there are null values in it.
2. Multiple alterations on the same table were applied within a transaction and not all
   constraints have been checked yet.

The solution to the first cause is simple: don't have null values in not null columns.

The solution to the second cause:

```SQL
SET CONSTRAINTS ALL IMMEDIATE;
```

This causes Postgres to check constraints right away after a statement.

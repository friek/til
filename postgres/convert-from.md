# Converting hex strings into text

Example hex string: `7468697320697320612068657820737472696e67` (actually: `this is a hex string`)  
When you've got such a string and need to convert it into a regular postgres string, you need
to use the `DECODE` function.

Example:
```sql
SELECT DECODE('7468697320697320612068657820737472696e67', 'hex');
```

This will convert it back into the text string.

However, when storing such a value into a TEXT or VARCHAR column, you also need to
convert it like this:
```sql
SELECT CONVERT_FROM(DECODE('7468697320697320612068657820737472696e67', 'hex'), 'UTF8');
```

Otherwise, the string will somehow still be binary.

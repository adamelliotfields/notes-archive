# Importing a CSV into MongoDB
> :calendar: *March 19, 2017*

```bash
mongoimport -db db -c collection --type csv --file file.csv --headerline
```

`-db` specifies the database. If it doesn't exist, MongoDB will create it.

`-c` specifies the collection. If it doesn't exist, MongoDB will create it.

`--type` specifies the file format. CSV files are delimited by commas. Wrap any values that have commas in double-quotes.

`--file` specifies the location of the file.

`--headerline` tells MongoDB to use the header to create keys for each document.

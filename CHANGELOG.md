# Changelog

## 1.1.2 (2026-10-02)

Image: [`harryopurba/bez:1.1.2`](https://hub.docker.com/r/harryopurba/bez/tags?name=1.1.2)

```
docker pull harryopurba/bez:1.1.2
```


### Features

- Show every SQL statement Bez runs in a log bar at the bottom of the page, with its values, timing and row count
- Add an About panel with build and connection details
- Show the connected database in the header
- Show the app version in the header
- Use the new bz mark as the app icon
- Remember recent database connections on the connect form
- Add a SQL Query page to run your own SQL, explain a query, see detailed errors and reuse past queries from history
- Page through large tables quickly, without counting every row first
- Sort tables by any column
- Filter rows with a control bar, including `LIKE` and `ILIKE` search
- Click a foreign key value to jump to the matching row in the related table
- Add a Structure tab showing columns, indexes and relations, with links to related tables
- Add tabs to switch between a table's rows, structure and insert form
- Edit rows with a full form: save, delete, checkboxes for booleans, large text boxes, and support for tables without a primary key
- Clone a row and edit the copy
- Show the host, port and database name in the browser tab title
- Browse the tables of a database and view their rows
- Connect to a PostgreSQL database from the browser

### Fixes

- Fix typed values being cleared while editing a row
- Fix copying selected table cells so they paste as tab-separated text
- Fix page scrolling, so tables use a single page scrollbar
- Fix foreign key links that failed to open the related table
- Allow opening tables in a new tab with ctrl-click or middle-click
- Fix timestamps shifting with the browser's timezone
- Fix filtering on non-text columns such as UUID
- Fix UUID arrays showing in the wrong format
- Fix inserts and updates on tables with column names that are reserved words
- Fix editing rows whose identifier could not be read from the URL
- Reset the sort order when switching to another table

### Other

- Make Bez faster: responses are compressed and cached, and startup no longer waits for a status check
- Make the sidebar faster on databases with many tables
- Publish one small Docker image for amd64 and arm64 with the frontend built in
- Use less common default ports to avoid clashing with other services on your machine
- Polish the look of tables, tabs, forms, sidebar and scrollbars

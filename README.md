## services (containers)
All applications require python 3.6 runtime.

The application services are:

### names
entrypoint: server.py
expects a GET request, returns a random name in the body.
listens on port 8000 by default

example:
```bash
curl localhost:8000
```

returns:
```<html><body><h1>Mary Jackson</h1></body></html>```

### numbers 

entrypoint: server.py
expects a GET request, returns a random number in the body
listens on port 8000 by default

example:
```bash
curl localhost:8000
```

returns:
```<html><body><h1>107</h1></body></html>```

### content
entrypoint server.py
expects a GET request, returns the list of customer names from DB
listens on port 8000 by default

required the following ENV VARS to configure the DB connection in the container:
MYSQL_HOST
MYSQL_USER
MYSQL_PASSWORD
MYSQL_DATABASE

requires the DB to have a table names customers with a column named "names" (see mysql dev content deployment dump instructions)

### scale
entrypoint: server.py
Expects a POST request with a number between 1 and 100 in the body (curl -X POST -d 54 localhost:8000)
Loads all cores on the server to the percentage specified in the POST body

example:
```bash
curl -X POST -d 54 localhost:8000
```

returns:
```<html><body><h1>Loading CPU to 54 percent</h1></body></html>```


## Database schema and configuration

The database required is a mysql 5.7 with InnoDB engine

The database schema is very simple
The db should be called "customers"
It consists of a single table called "customers" with the following columns:

	name VARCHAR(100)
	debt INT

A db dump file for import is in the repo root (customers.sql)
Can be used directly for import or reference

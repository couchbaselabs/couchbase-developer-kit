# Couchbase Developer Kit

Couchbase is a database platform. It has three main developer components:

* Server – A distributed database server
* Lite – An embedded database
* Gateway – An Internet gateway for reading, writing, and synchronizing data over the web

## Try Couchbase for the First Time

### CRUD

Couchbase records are JSON documents.

#### Setup

**TODO:** Setup steps

#### Server

```shell
# Navigate to the server directory
cd server

# Connect to the travel sample database 
./server couchbase://localhost/travel-sample -u admin -p password

# Read the record for San Francisco International airport
(server) get airport_3469

# Create a new record for Dawson Community Airport
(server) put airport_10000 {"airportname":"Dawson Community Airport"}
(server) get airport_10000

# Update the record for Dawson Community Airport to include more information
(server) put airport_10000 {"airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","type":"airport","tz":"America/Denver"}
(server) get airport_10000

# Delete the record for Dawson Community Airport
(server) rm airport_10000
(server) get airport_10000
```

#### Lite

```shell
# Navigate to the lite directory
cd lite

# Open the travel sample database
./lite --writeable samples/travel/db.cblite2

# Read the record for San Francisco International airport
(cblite) get airport_3469

# Create a new record for Dawson Community Airport
(cblite) put airport_10000 {"airportname":"Dawson Community Airport"}
(cblite) get airport_10000

# Update the record for Dawson Community Airport to include more information
(cblite) put airport_10000 {"airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","type":"airport","tz":"America/Denver"}
(cblite) get airport_10000

# Delete the record for Dawson Community Airport
(cblite) rm airport_10000
(cblite) get airport_10000
```

#### Gateway

```shell
# Navigate to the gateway directory
cd gateway

# Start the gateway with the travel sample config
./bin/sync_gateway samples/travel/config.json

# Connect to the gateway
./gateway -url http://localhost:4984/travel

# Read the record for San Francisco International airport
(gateway) cat airport_3469

# Create a new record for Dawson Community Airport
(gateway) put airport_10000 '{"airportname":"Dawson Community Airport"}'
(gateway) cat airport_10000

# Update the record for Dawson Community Airport to include more information
(gateway) put airport_10000 '{"airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","type":"airport","tz":"America/Denver"}'
(gateway) cat airport_10000

# Delete the record for Dawson Community Airport
(gateway) rm airport_10000
(gateway) cat airport_10000
```

### Query

Couchbase queries are SQL.

#### Server

```shell
# Navigate to the server directory
cd server

# Connect to the travel sample database 
./server couchbase://localhost/travel-sample -u admin -p password

# Find the San Francisco International airport record using it's airport code
(server) SELECT * FROM `travel-sample` WHERE faa='SFO'

# Find the first 10 airports in alphabetical order
(server) SELECT id, airportname FROM `travel-sample` WHERE airportname IS NOT NULL ORDER BY airportname LIMIT 10

# Find the altitude of the highest airport in each country
(server) SELECT country, max(geo.alt) AS alt FROM `travel-sample` group by country
```

#### Lite

```shell
# Navigate to the lite directory
cd lite

# Open the travel sample database
./lite samples/travel/db.cblite2

# Find the San Francisco International airport record using it's airport code
(cblite) SELECT * WHERE faa='SFO'

# Find the first 10 airports in alphabetical order
(cblite) SELECT id, airportname WHERE airportname IS NOT NULL ORDER BY airportname LIMIT 10

# Find the altitude of the highest airport in each country
(cblite) SELECT country, max(geo.alt) AS alt GROUP BY country
```

### Sync

#### Setup

Connect to the server travel sample database.

```shell
# Navigate to the server directory
cd server

# Connect to the travel sample database 
./server couchbase://localhost/travel-sample -u admin -p password
```

Start the gateway with the travel sample config.

```shell
# Navigate to the gateway directory
cd gateway

# Start the gateway with the travel sample config
./bin/sync_gateway samples/travel/config.json
```

Open the lite travel sample database.

```shell
# Navigate to the lite directory
cd lite

# Open the travel sample database
./lite --writeable samples/travel/db.cblite2

# Start sync with the gateway
(cblite) cp --bidi --continuous ws://localhost:4984/travel
```

#### Sync a new record from server to lite

In lite, look for Dawson Community Airport – it doesn't exist.

```shell
(cblite) get airport_10000
```

In server, create a new record for Dawson Community Airport.

```shell
(server) put airport_10000 {"airportname":"Dawson Community Airport"}
```

In lite, see that the new record for Dawson Community Airport synchronized from server.

```shell
(cblite) get airport_10000
```

#### Sync a record update from lite to server

In lite, update the record for Dawson Community Airport to include more information.

```shell
(cblite) put airport_10000 {"airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","type":"airport","tz":"America/Denver"}
```

In server, see that the new information for Dawson Community Airport synchronized from lite.

```shell
(server) get airport_10000
```

#### Sync a record delete

In server, delete the record for Dawson Community Airport.

```shell
(server) rm airport_10000
```

In lite, see that the deletion of Dawson Community Airport synchronized from server.

```shell
(cblite) get airport_10000
```

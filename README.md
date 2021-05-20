# Couchbase Developer Kit

Couchbase is a NoSQL database platform. It has three main developer components:

* Couchbase Server – A distributed database server
* Couchbase Lite – An embedded database
* Couchbase Gateway – An Internet gateway for reading, writing, and synchronizing data over the web

## Try Couchbase for the First Time

### Setup

**TODO:** Setups steps

### CRUD

Couchbase records are JSON documents.

#### Server

```shell
# Navigate to the server directory
cd server

# Connect to the travel sample database (enter the password when prompted)
./couchbase-server --password --bucket travel-sample

# Read the record for Ted Stevens Anchorage International Airport (Alaska)
doc get airline_16726 --flatten

# create a new record Williston Basin International Airport in North Dakota, code XWA
doc insert airport_3333 {"name":"Williston Basin International Airport" , "callsign":"XWA"}
doc get airport_3333 --flatten

# update the record created airport_3333 with type as airline
doc upsert airport_3333 {"name":"Williston Basin International Airport" , "callsign":"XWA" , "type": "airline"}
doc get airport_3333 --flatten

# delete record airport_3333
doc remove airport_3333
doc get airport_3333 --flatten
```

#### Lite

```shell
# Navigate to the lite directory
cd lite

# Open the travel sample database
./lite --writeable samples/travel/db.cblite2

# Read the record for San Francisco International airport
(cblite) cat airport_3469

# Create a new record for Dawson Community Airport
(cblite) put airport_10000 '{"airportname":"Dawson Community Airport"}'
(cblite) cat airport_10000

# Update the record for Dawson Community Airport to include more information
(cblite) put airport_10000 '{"airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","type":"airport","tz":"America/Denver"}'
(cblite) cat airport_10000

# Delete the record for Dawson Community Airport
(cblite) rm airport_10000
(cblite) cat airport_10000
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

Couchbase supports query using SQL.

#### Server

**TODO:** Short query exercise on travel sample database.

#### Lite

```shell
# Navigate to the lite directory
cd lite

# Open the travel sample database
./lite samples/travel/db.cblite2

# Find the San Francisco International airport record using it's airport code
(cblite) SELECT * WHERE faa="SFO"

# Find the first 10 airports in alphabetical order
(cblite) SELECT id, airportname WHERE airportname != null ORDER BY airportname ASC LIMIT 10

# Find the airport at the highest altitude for each country
(cblite) SELECT country, airportname, max(geo.alt) as alt GROUP BY country
```

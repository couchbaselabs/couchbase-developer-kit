# Couchbase Developer Kit

Couchbase is a NoSQL database platform. It has three main developer components:

* Couchbase Server – A distributed database server
* Couchbase Lite – An embedded database
* Sync Gateway – An Internet gateway

## Try Couchbase for the First Time

### Setup

**TODO:** Setups steps

### CRUD

Couchbase records are JSON documents.

#### Couchbase Server

```shell
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

#### Couchbase Lite

```shell
# Navigate to the Couchbase Lite directory
cd lite

# Open the Couchbase Lite travel sample database
./couchbase-lite --writeable samples/travel/db.cblite2

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
# Navigate to the Couchbase Gateway directory
cd gateway

# Start the Gateway with the travel sample config
./couchbase-gateway samples/travel/config.json

# Read the record for San Francisco International airport
curl -X GET http://localhost:4984/travel/airport_3469

# Create a new record for Dawson Community Airport
curl -X PUT http://localhost:4984/travel/airport_10000 -H "Content-Type: application/json" -d '{"airportname":"Dawson Community Airport"}'
curl -X GET http://localhost:4984/travel/airport_10000

# Update the record for Dawson Community Airport to include more information
curl -X PUT http://localhost:4984/travel/airport_10000 -H "Content-Type: application/json" -d '{"_rev":"1-eadd82459b221e07a78c9c75198e9cfb","airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","id":10000,"type":"airport","tz":"America/Denver"}'
curl -X GET http://localhost:4984/travel/airport_10000

# Delete the record for Dawson Community Airport
curl -X DELETE http://localhost:4984/travel/airport_10000?rev=2-34f55bdc0de9ebc545f46777612e634c
curl -X GET http://localhost:4984/travel/airport_10000
```

### Query

Couchbase supports query using SQL.

#### Couchbase Server

**TODO:** Short query exercise on travel sample database.

#### Couchbase Lite

```shell
# Navigate to the Couchbase Lite directory
cd lite

# Open the Couchbase Lite travel sample database
./couchbase-lite samples/travel/db.cblite2

# Find the San Francisco International airport record using it's airport code
(cblite) SELECT * WHERE faa="SFO"

# Find the first 10 airport names in alphabetical order
(cblite) SELECT id, airportname WHERE airportname != null ORDER BY airportname ASC LIMIT 10

# Find the id, name, and altitude of the airport at the highest altitude
(cblite) SELECT id, airportname, alt WHERE alt=max(alt) GROUP BY alt
```

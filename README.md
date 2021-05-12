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

**TODO:** Short CRUD exercise on travel sample database.

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
(cblite) cat airport_10000 # This will return the delete tombstone with an empty body

```

#### Sync Gateway

**TODO:** Short CRUD exercise on travel sample database.

# Developer CLI sketch

## CRUD

Couchbase records are JSON documents.

### Couchbase Server

```shell
# Navigate to the Couchbase Gateway directory
cd server

# Start the server with the travel sample config
./server samples/travel/config.json

# Read the record for San Francisco International airport
(server) cat airport_3469

# Create a new record for Dawson Community Airport
(server) put airport_10000 '{"airportname":"Dawson Community Airport"}'
(server) cat airport_10000

# Update the record for Dawson Community Airport to include more information
(server) put airport_10000 '{"airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","type":"airport","tz":"America/Denver"}'
(server) cat airport_10000

# Delete the record for Dawson Community Airport
(server) rm airport_10000
(server) cat airport_10000
```

### Couchbase Lite

```shell
# Navigate to the Couchbase Lite directory
cd lite

# Open the Couchbase Lite travel sample database
./lite samples/travel/db.cblite2

# Read the record for San Francisco International airport
(lite) cat airport_3469

# Create a new record for Dawson Community Airport
(lite) put airport_10000 '{"airportname":"Dawson Community Airport"}'
(lite) cat airport_10000

# Update the record for Dawson Community Airport to include more information
(lite) put airport_10000 '{"airportname":"Dawson Community Airport","city":"Glendive","country":"United States","faa":"GDV","geo":{"alt":2456,"lat":47.133071760160384,"lon":-104.8024315730339},"icao":"KGDV","type":"airport","tz":"America/Denver"}'
(lite) cat airport_10000

# Delete the record for Dawson Community Airport
(lite) rm airport_10000
(lite) cat airport_10000
```

### Gateway

```shell
# Navigate to the Couchbase Gateway directory
cd gateway

# Start the Gateway with the travel sample config
./gateway samples/travel/config.json

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

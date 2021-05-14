# Developer CLI sketch

## CRUD

Couchbase records are JSON documents.

### Couchbase Server

```shell
# Navigate to the server directory
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
# Navigate to the lite directory
cd lite

# Open the lite travel sample database
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
# Navigate to the gateway directory
cd gateway

# Start the gateway with the travel sample config
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

## Sync

### Setup

Start the server with the travel sample config.

```shell
# Navigate to the server directory
cd server

# Start the server with the travel sample config
./server samples/travel/config.json
```

Start the gateway with the travel sample config.

```shell
# Navigate to the gateway directory
cd gateway

# Start the gateway with the travel sample config
./gateway samples/travel/config.json
```

Open the lite travel sample database.

```shell
# Navigate to the lite directory
cd lite

# Open the lite travel sample database
./lite samples/travel/db.cblite2
```

### Sync a new record from server to lite

In lite, look for Arcata-Eureka Airport. It doesn't exist.

```shell
(lite) cat airport_10001
```

In server, create a new record for Arcata-Eureka Airport.

```shell
(server) put airport_10001 '{"airportname":"Arcata-Eureka Airport"}'
```

In lite, see that the new record for Arcata-Eureka Airport synchronized from server.

```shell
(lite) cat airport_10001
```

### Sync a record update from lite to server

In lite, update the record for Arcata-Eureka Airport to include more information.

```shell
(lite) put airport_10001 '{"airportname":"Arcata-Eureka Airport","city":"Humboldt County, California","country":"United States","faa":"ACV","geo":{"alt":222,"lat":40.977778,"lon":-124.108333},"icao":"KACV","type":"airport","tz":"America/Los_Angeles"}'
```

In server, see that the new information for Arcata-Eureka Airport synchronized from lite.

```shell
(server) cat airport_10001
```

### Sync a record delete

In server, delete the record for Arcata-Eureka Airport.

```shell
(server) rm airport_10001
```

In lite, see that the deletion of Arcata-Eureka Airport synchronized from server.

```shell
(lite) cat airport_10001
```

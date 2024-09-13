# RSMfmx_v3.1_API-Docs

Rest API Documentation for RSMfmx v3.1

## Auth

Add a new request header: `X-API-KEY: <YOUR API KEY>`

## v1 Endpoints

### Server Config

#### URL Path

GET | PUT `/v1/serverConfig`

This endpoint provides 2 methods. `GET` and `PUT`.

* `GET` - Gets the current server config in JSON format.
* `PUT` - Provide the data structure from the `GET` request with your modified version of the data values.

#### Setting the Map

When setting the map you need to set both the `MapName` and `MapIndex` properties.

```text
MapName: "Procedural Map"
MapIndex: 0

MapName: "Barren"
MapIndex: 1

MapName: "CraggyIsland"
MapIndex: 2

MapName: "Custom Map"
MapIndex: 3
```

Map options within provided Server Config:

```json
"Map": {
        "MapName": "CraggyIsland",
        "MapIndex": 2,
        "CustomMapURL": "",
        "MapSize": 3500,
        "MapSeed": 352165132
    },
```

#### Status Codes

* `200` - Success. Body may contain more information.
* `401` - Unauthorized, check your API key. The body will contain more info.
* `500` - Internal Server Error. The body will contain more info.

### Check Server Running Status

GET `/V1/serverStatus`

#### Response

Note: The `PID` field will always contain the last known ProcessID.

```json
{
    "isRunning": false,
    "PID": 3132
}
```

### Starting and Stopping the server

#### Starting

GET `/v1/startServer`

##### Status Codes

* `200` - Success. Body may contain more information.
* `401` - Unauthorized. Check your API key. The body will contain more info.
* `403` - Forbidden. RSM couldn't start your server. See the body for more information.
* `500` - Internal Server Error. The body will contain more info.

#### Stopping

RSM will send the `quit` command over RCON to start a propper shutdown.

GET `/v1/stopServer`

##### Status Codes

* `200` - Success. Body may contain more information.
* `401` - Unauthorized. Check your API key. The body will contain more info.
* `403` - Forbidden. RSM couldn't stop your server. See the body for more information.
* `500` - Internal Server Error. The body will contain more info.

#### Force Stopping the server

RSM Will kill the server process.

GET `/v1/forceStopServer`

* `200` - Success. Body may contain more information.
* `401` - Unauthorized. Check your API key. The body will contain more info.
* `403` - Forbidden. RSM couldn't stop your server. See the body for more information.
* `500` - Internal Server Error. The body will contain more info.

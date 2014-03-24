Data
====

Airport / Route Query
---------------------

### Airport

To get raw data

    http://data.hivetrix.com/raw/airports.geojson

To query an airport, use

    http://data.hivetrix.com/airport?q=<IATA>[,<IATA>]

for example

    http://data.hivetrix.com/airport?q=SFO
    http://data.hivetrix.com/airport?q=SFO,LAX

### Route

To query a route, use

    http://data.hivetrix.com/route?q=(<IATA>,<IATA>[,<IATA>])[,(<IATA>,<IATA>[,<IATA>])]

    http://data.hivetrix.com/route?q=(SFO,LAX)
    http://data.hivetrix.com/route?q=(SFO,LAX),(SFO,DEN)

Map
---

### World Map

    http://data.hivetrix.com/raw/world-50m.json

### US

    http://data.hivetrix.com/raw/us-states.json
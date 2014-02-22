Code / Services
===============










Airport / Route Query
---------------------

### Airport

To query an airport, use

    http://airportlookup.map4geek.com/airport?q=<IATA>[,<IATA>]

for example

    http://airportlookup.map4geek.com/airport?q=SFO
    http://airportlookup.map4geek.com/airport?q=SFO,LAX

### Route

To query a route, use

    http://airportlookup.map4geek.com/route?q=(<IATA>,<IATA>[,<IATA>])[,(<IATA>,<IATA>[,<IATA>])]

    http://airportlookup.map4geek.com/route?q=(SFO,LAX)
    http://airportlookup.map4geek.com/route?q=(SFO,LAX),(SFO,DEN)
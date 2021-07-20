# Haversines

Let's find the distance between Big Ben in London and the Statue of Liberty in
New York.

```ucm
.> cd .flight.Geodesy
```

```unison haversine.u
london =
    (Rad lat) = Convert.degToRad (Deg 51.5007)
    (Rad lng) = Convert.degToRad (Deg -0.1246)
    LatLng (Lat lat) (Lng lng)
newyork =
    (Rad lat) = Convert.degToRad (Deg 40.6892)
    (Rad lng) = Convert.degToRad (Deg -74.0445)
    LatLng (Lat lat) (Lng lng)
> london
> newyork
> Haversine.distance london newyork
```
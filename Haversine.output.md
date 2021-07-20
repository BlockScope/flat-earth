# Hello

```ucm
.> cd .flight.Geodesy

```
```unison
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

```ucm

  I found and typechecked these definitions in scratch.u. If you
  do an `add` or `update`, here's how your codebase would
  change:
  
    ⍟ These new definitions are ok to `add`:
    
      london  : LatLng
      newyork : LatLng
  
  Now evaluating any watch expressions (lines starting with
  `>`)... Ctrl+C cancels.

    9 | > london
          ⧩
          LatLng
            (Lat.Lat 0.8988567820818436)
            (Lng.Lng -2.1746802479849347e-3)
  
    10 | > newyork
           ⧩
           LatLng
             (Lat.Lat 0.7101605100024767)
             (Lng.Lng -1.2923203179929412)
  
    11 | > Haversine.distance london newyork
           ⧩
           5574840.456848554

```

# Vincenty

From the table in Vincenty's paper showing the results of solutions.

```
  TABLE II - RESULTS OF SOLUTIONS

Line       Φ₁                   Φ₂
           α₁                   L
           s                    α₂

(a) 55° 45' 00.00000"   -33° 26' 00.00000"
    96  36  08.79960    108  13  00.00000"
      14110526.170m     137  52  22.01454

(b) 37° 19' 54.95367"    26° 07' 42.83946"
    95  27  59.63089     41  28  35.50729
       4085966.703m     118  05  58.96161

(c) 35° 16' 11.24862"    67° 22' 14.77638"
    15  44  23.74850    137  47  28.31435
       8084823.839m     144  55  39.92147

(d)  1° 00' 00.00000"    -0° 59' 53.83076"
    89  00  00.00000    179  17  48.02997
      19960000.000m      91  00  06.11733

(e)  1° 00' 00.00000"     1° 01' 15.18952"
     4  59  59.99995    179  46  17.84244
      19780006.558m     174  59  59.88481

Notation
    Φ₁,Φ₂ - geodetic latitudes at points P₁ and P₂
    α₁,α₂ - azimuths of the geodesic; α₂ in the direction P₁ and P₂
       s  - length of the geodesic
```
 
```ucm
.> cd .flight.Geodesy
```

```unison vincenty.u
xys : [((DMS, DMS), (DMS, DMS))]
xys =
    [ ((( +55, +45,  0.00000), (  +0,  +0,  0.0)), (( -33, +26,  0.00000), (+108, +13,  0.00000)))
    , ((( +37, +19, 54.95367), (  +0,  +0,  0.0)), (( +26,  +7, 42.83946), ( +41, +28, 35.50729)))
    , ((( +35, +16, 11.24862), (  +0,  +0,  0.0)), (( +67, +22, 14.77638), (+137, +47, 28.31435)))
    , (((  +1,  +0,  0.00000), (  +0,  +0,  0.0)), ((  +0, -59, 53.83076), (+179, +17, 48.02997)))
    , (((  +1,  +0,  0.00000), (  +0,  +0,  0.0)), ((  +1,  +1, 15.18952), (+179, +46, 17.84244)))
    ]
        |> List.map (cases ((xLat, xLng), (yLat, yLng)) ->
            x = (DMS xLat, DMS xLng)
            y = (DMS yLat, DMS yLng)

            (x, y))

es = [bessel, hayford, hayford, hayford, hayford]

ds =
    [ 14110526.170
    ,  4085966.703
    ,  8084823.839
    , 19960000.000
    , 19780006.5584
    ]

fwdAzimuths : [DMS]
fwdAzimuths =
    List.map DMS
        [ ( +96, +36,  8.79960)
        , ( +95, +27, 59.63089)
        , ( +15, +44, 23.74850)
        , ( +89,  +0,  0.00000)
        , (  +4, +59, 59.99995)
        ]

revAzimuths : [DMS]
revAzimuths =
    List.map DMS
        [ (+137, +52, 22.01454)
        , (+118,  +5, 58.96161)
        , (+144, +55, 39.92147)
        , ( +91,  +0,  6.11733)
        , (+174, +59, 59.88481)
        ]

inversePoints : ((DMS, DMS), (DMS, DMS)) -> InverseProblem LatLng
inversePoints dmsLatLng =
    ((xLat, xLng), (yLat, yLng)) = dmsLatLng
    (Rad xLat') = Convert.degToRad (Deg (toDeg xLat))
    (Rad xLng') = Convert.degToRad (Deg (toDeg xLng))
    
    (Rad yLat') = Convert.degToRad (Deg (toDeg yLat))
    (Rad yLng') = Convert.degToRad (Deg (toDeg yLng))
    x = LatLng (Lat xLat') (Lng xLng')
    y = LatLng (Lat yLat') (Lng yLng')
    InverseProblem x y

solvedDistances =
    f e dmsLatLng =
      (InverseProblem x y) = inversePoints dmsLatLng
      Vincenty.distance e x y
    List.zipWith f es xys

> somes solvedDistances
```
# flat-earth

Here are solutions to the direct and inverse geodesy problems using [haversines
formula](https://en.wikipedia.org/wiki/Haversine_formula) on the sphere and
[Vincenty's formulae](https://en.wikipedia.org/wiki/Vincenty%27s_formulae) on
the ellipsoid as models of the Earth.

```unison
  {{ The inputs for the direct or forward problem in geodesy.
  
  * {x} The departure point on the ellipsoid.
  * {α₁} The azimuth from the departure point.
  * {s} The distance to the arrival point. }}
unique type DirectProblem a α s = { x : a, α₁ : α, s : s }

  {{ The outputs for the solution to the direct or forward problem in geodesy.
  
  * {y} The arrival point.
  * {α₂} The azimuth at the arrival point. }}
unique type DirectSolution a α = { y : a, α₂ : Optional α }
```

```unison
InverseProblem.doc =
  {{ The inputs for the inverse or reverse problem in geodesy.
  
  * {x} The departure point.
  * {y} The arrival point. }}
unique type InverseProblem a = { x : a, y : a }

  {{ The outputs for the solution to the inverse or reverse problem in geodesy.
  
  * {s} The distance between departure and arrival points.
  * {α₁} The azimuth at the departure point.
  * {α₂} The azimuth at the arrival point. }}
unique type InverseSolution s α = InverseSolution s α (Optional α)
```

The Haversine [transcript](Haversine.output.md) finds the distance from Big Ben,
London to the Statue of Liberty, New York, with inputs in decimal degrees and
outputs in metres.
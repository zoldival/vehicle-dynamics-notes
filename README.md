# vehicle dynamics notes

my notes from learning vehicle dynamics for [formula slug](https://github.com/formulaslug). everything here is written in my own words as i work through it, starting from the basics.

## yaw rate

working toward a model of yaw rate from things we can measure on the car (speed, steering, tire loads), validated against fs-3 data. code lives in [Sims-Data](https://github.com/formulaslug/Sims-Data) (issue #81).

| # | topic | status |
|---|---|---|
| 01 | [kinematic yaw rate](yaw-rate/01-kinematic.md) | done |
| 02 | [tire cornering forces](yaw-rate/02-tire-cornering.md) | done |
| 03 | [understeer gradient](yaw-rate/03-understeer-gradient.md) | done |
| 04 | [load transfer](yaw-rate/04-load-transfer.md) | done |
| 05 | [dynamic bicycle model](yaw-rate/05-bicycle-model.md) | done |

## laptime sim

(coming later)

## conventions

- units: SI (m, s, N, kg), angles in radians unless marked
- axes: SAE (x forward, y right, z down, right turn = positive yaw rate). slip angle follows Rajamani, so positive α gives positive Fy. note: FS-3 VDM logs x accel flipped and z reads +1 g at rest.

| symbol | meaning |
|---|---|
| r | yaw rate |
| V | forward speed |
| δ | steer angle (road wheel) |
| α | slip angle |
| β | sideslip angle at the CG |
| ψ | heading |
| μ | friction coefficient |
| Cα | cornering stiffness |
| L | wheelbase |

## sources

- Gillespie, *Fundamentals of Vehicle Dynamics* (SAE)
- Segers, *Analysis Techniques for Racecar Data Acquisition*, 2nd ed. (SAE, 2014)

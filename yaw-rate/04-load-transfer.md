# 04: load transfer

## load transfer, simplified

in a corner, the car's weight pushes outward, so load shifts from the inside tires to the outside tires. under braking, load shifts to the front, and under acceleration, to the rear.

from item 2, a tire's grip doesn't grow as fast as its load. so when load shifts, the outside tire gains less grip than the inside tire loses, and the axle loses total grip. whichever axle loses more grip slips more, and that changes understeer vs oversteer.

## lateral weight transfer (Segers §10.1)

in a turn, a centrifugal force acts on the CG and tries to throw the car outward. the tires resist it with their cornering force. since the CG sits above the ground, that pair of forces tips load from the inside wheels to the outside wheels.

the inertial force is:

$$F = W \cdot G_{lat}$$

taking moments about one of the wheel centers gives the total lateral weight transfer:

$$\Delta W_{lat} = \frac{W \cdot G_{lat} \cdot h_{CG}}{T}$$

| symbol | meaning |
|---|---|
| W | vehicle weight (kg) |
| G_lat | lateral acceleration at the CG (g) |
| h_CG | CG height from the ground (m) |
| T | track width (m) |
| ΔW_lat | load moved from the inside wheels to the outside wheels (kg) |

**what it says:** weight transfer goes up with more weight, more lateral g, or a higher CG, and goes down with a wider track.

### worked example

single-seater with 254 kg on each side, 1.0 g, CG height 0.381 m, track 1.435 m:

$$\Delta W_{lat} = \frac{(254 + 254) \cdot 1.0 \cdot 0.381}{1.435} = 134.88 \text{ kg}$$

- outside wheels: 254 + 134.88 = 388.88 kg
- inside wheels: 254 − 134.88 = 119.12 kg

so at just 1 g, the inside wheels lose over half their load.

## longitudinal weight transfer (Segers §10.2)

same idea front to back. when the car accelerates or brakes in a straight line, an inertial force acts at the CG and shifts load between the axles:

$$\Delta W_{long} = \frac{W \cdot G_{long} \cdot h_{CG}}{WB}$$

- G_long = longitudinal acceleration (g)
- WB = wheelbase (m)

it's the same as the lateral formula, with longitudinal g instead of lateral g and the wheelbase instead of the track width.

- **accelerating** (positive G_long): load moves to the rear axle
- **braking** (negative G_long): load moves to the front axle

## suspension modes

the four suspension corners (LF, RF, LR, RR) can move in a few basic patterns, or "modes." each mode has its own stiffness, which relates the total force in that mode to how far the suspension moves.

- F = vertical force at a corner
- x = suspension displacement at a corner

### heave

all four wheels move together, in the same direction (the whole car moves straight up or down).

the total force from heave is the sum of the vertical forces on each wheel, from the sum of each wheel's displacement:

$$F_{LF} + F_{RF} + F_{LR} + F_{RR} = K_H \cdot (x_{LF} + x_{RF} + x_{LR} + x_{RR})$$

K_H = heave stiffness

### pitch

the front and rear wheel pairs move in opposite directions (nose down / tail up, like under braking).

the pitch stiffness K_P relates the total pitch force to the pitch displacement:

$$F_{LF} + F_{RF} - F_{LR} - F_{RR} = K_P \cdot (x_{LF} + x_{RF} - x_{LR} - x_{RR})$$

### roll

the left and right wheel pairs move in opposite directions (the car leans in a corner).

the roll rate K_R is the ratio between the total roll force and the roll displacement:

$$F_{LF} - F_{RF} + F_{LR} - F_{RR} = K_R \cdot (x_{LF} - x_{RF} + x_{LR} - x_{RR})$$

## sources

- Segers, *Analysis Techniques for Racecar Data Acquisition*, §10.1 and §10.2 (PDF pp. 240–242, 249)
- Segers, *Analysis Techniques for Racecar Data Acquisition*, §10.5 "Determining Wheel Loads with Modal Analysis" (PDF pp. 259–265)

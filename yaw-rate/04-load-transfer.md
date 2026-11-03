# 04: load transfer

## load transfer, simplified

in a corner, the car's weight pushes outward, so load shifts from the inside tires to the outside tires. under braking, load shifts to the front, and under acceleration, to the rear.

from item 2, a tire's grip doesn't grow as fast as its load. so when load shifts, the outside tire gains less grip than the inside tire loses, and the axle loses total grip. whichever axle loses more grip slips more, and that changes understeer vs oversteer.

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

- Segers, *Analysis Techniques for Racecar Data Acquisition*, §10.5 "Determining Wheel Loads with Modal Analysis" (PDF pp. 259–265)

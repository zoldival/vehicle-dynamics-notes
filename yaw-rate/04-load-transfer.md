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

**why it matters for yaw:** braking into a corner moves load to the fronts, so the front gains grip, the rear loses grip, and the car rotates more on entry. accelerating out does the opposite and the car tends to push.

## tire load sensitivity (Gillespie Eq 6-36 to 6-49)

this is the link between load transfer and yaw rate.

### one tire (Eq 6-36)

a tire's cornering stiffness depends on its load:

$$F_y' = C_\alpha' \cdot \alpha = (a F_z - b F_z^2) \cdot \alpha$$

- Fy' = lateral force of one tire
- Cα' = cornering stiffness of one tire
- Fz = load on that tire
- a, b = tire coefficients

the **−b·Fz²** term means grip doesn't keep up with load. double the load gives less than double the force.

### both tires on an axle (Eq 6-37)

with zo = outside tire and zi = inside tire:

$$F_y = (a F_{zo} - b F_{zo}^2 + a F_{zi} - b F_{zi}^2) \cdot \alpha$$

in a corner, the outside tire gains load and the inside tire loses the same amount:

- outside: Fz + ΔFz
- inside: Fz − ΔFz

### plug in (Eq 6-40)

$$F_y = \left[2a F_z - 2b F_z^2 - 2b \, \Delta F_z^2\right] \cdot \alpha$$

- the **a** terms: ΔFz cancels out, no change
- the **b** terms: ΔFz doesn't cancel, leaving **−2b·ΔFz²**

that last term is grip lost just from load moving. it's squared, so 2× the load transfer costs 4× the grip.

### each axle gets weaker (Eq 6-41, 6-44, 6-45)

each axle's cornering stiffness at static load:

$$C_\alpha = 2a F_z - 2b F_z^2$$

with load transfer, each axle loses some of it:

$$F_{yf} = \left[C_{\alpha f} - 2b \, \Delta F_{zf}^2\right] \alpha_f \qquad F_{yr} = \left[C_{\alpha r} - 2b \, \Delta F_{zr}^2\right] \alpha_r$$

### K splits in two (Eq 6-48, 6-49)

$$K = K_{tires} + K_{load\ transfer}$$

$$K_{tires} = \frac{W_f}{C_{\alpha f}} - \frac{W_r}{C_{\alpha r}} \qquad K_{load\ transfer} = \frac{W_f \cdot 2b \, \Delta F_{zf}^2}{C_{\alpha f}^2} - \frac{W_r \cdot 2b \, \Delta F_{zr}^2}{C_{\alpha r}^2}$$

- K_tires is the same K from item 3
- **front load transfer always adds understeer**
- **rear load transfer always adds oversteer**

**big takeaway:** whichever axle takes more of the load transfer loses more grip. that's how teams tune balance. a stiffer front anti-roll bar puts more transfer on the front, which means more understeer.

## suspension modes (Segers §10.5)

the four suspension corners (LF, RF, LR, RR) can move in a few basic patterns, or "modes." each mode has its own stiffness, which relates the total force in that mode to how far the suspension moves.

- F = vertical force at a corner
- x = suspension displacement at a corner

### heave

all four wheels move together, in the same direction (the whole car moves straight up or down).

$$F_{LF} + F_{RF} + F_{LR} + F_{RR} = K_H \cdot (x_{LF} + x_{RF} + x_{LR} + x_{RR})$$

K_H = heave stiffness

### pitch

the front and rear wheel pairs move in opposite directions (nose down / tail up, like under braking).

$$F_{LF} + F_{RF} - F_{LR} - F_{RR} = K_P \cdot (x_{LF} + x_{RF} - x_{LR} - x_{RR})$$

K_P = pitch stiffness

### roll

the left and right wheel pairs move in opposite directions (the car leans in a corner).

$$F_{LF} - F_{RF} + F_{LR} - F_{RR} = K_R \cdot (x_{LF} - x_{RF} + x_{LR} - x_{RR})$$

K_R = roll rate

### warp

the diagonals move in opposite directions (LF + RR vs RF + LR), which twists the chassis.

$$F_{LF} - F_{RF} - F_{LR} + F_{RR} = K_W \cdot (x_{LF} - x_{RF} - x_{LR} + x_{RR})$$

K_W = warp stiffness

## review questions

**why does the inside tire losing load hurt more than the outside tire gaining it helps?**
because of the −b·Fz² term. grip doesn't grow as fast as load, so the outside tire gains less than the inside tire loses. the axle's net loss is 2b·ΔFz².

**if you lower the CG, what happens to load transfer?**
it goes down, since h_CG is on top in ΔW = W·G·h/T. less load transfer means less grip lost.

**does K stay the same at 0.5 g and 1.5 g?**
no. load transfer grows with lateral g, and the grip lost grows with its square. so K_load transfer gets bigger as g goes up, and the car's balance changes mid-corner.

<img width="1668" height="2157" alt="image" src="https://github.com/user-attachments/assets/58eee3e5-cec5-480e-b660-1d5337738d30" />

<img width="1668" height="2157" alt="image" src="https://github.com/user-attachments/assets/dd909cce-f999-45e2-86f0-d628cd6037e4" />

<img width="1668" height="2157" alt="image" src="https://github.com/user-attachments/assets/07066864-2026-434f-83d6-5ae7b672dede" />

<img width="1668" height="2157" alt="image" src="https://github.com/user-attachments/assets/7adf9cef-3cee-494b-b3d8-19407e691602" />

<img width="1668" height="2157" alt="image" src="https://github.com/user-attachments/assets/b69e38df-a818-42f7-98f3-ec4ae251274e" />


## sources

- Segers, *Analysis Techniques for Racecar Data Acquisition*, §10.1 and §10.2 (printed pp. 221–223, 230)
- Segers, *Analysis Techniques for Racecar Data Acquisition*, §10.5 (printed pp. 240–247)
- Gillespie, *Fundamentals of Vehicle Dynamics*, Ch 6 (printed pp. 215–217)0–242, 249)
- Segers, *Analysis Techniques for Racecar Data Acquisition*, §10.5 "Determining Wheel Loads with Modal Analysis" (PDF pp. 259–265)

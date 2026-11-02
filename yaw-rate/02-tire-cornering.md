# 02: tire cornering forces

## slip angle

**slip angle (α, alpha)** is the angle between the direction a tire is heading (pointing) and the direction it's actually traveling.

when the tire is dragged at that angle, it pushes back sideways with a **cornering force (Fy)**. that's the force that lets a car turn.

## force vs slip angle

- more slip angle = more cornering force, up to a point
- at low slip angles (about 5° or less) the curve is a straight line
- at bigger angles it bends over and flattens out as the tire runs out of grip

in the straight part, cornering force is:

$$F_y = C_\alpha \cdot \alpha$$

the constant **Cα is the cornering stiffness**: the slope of the straight part of the curve.

## what cornering stiffness depends on

tire size and type (radial vs bias-ply), number of plies, cord angles, wheel width and tread all matter. **load and inflation pressure are the main ones.**

## forces on the whole car

for a car moving forward at speed V, the lateral forces from the tires have to equal mass times centripetal acceleration:

$$\sum F_y = F_{yf} + F_{yr} = \frac{M V^2}{R}$$

- Fyf = lateral (cornering) force at the front axle
- Fyr = lateral (cornering) force at the rear axle
- M = mass of the vehicle
- V = forward velocity
- R = radius of the turn

since V²/R is lateral acceleration and r = V/R, this can also be written without R:

$$\sum F_y = M \cdot V \cdot r$$

## why a tire makes force at a slip angle

as the tire rolls, each tread element touches the road undeflected, so at first it carries no side force. because the tire is moving at an angle to where it points, the element stays stuck where it first touched the road while the tire moves on. that deflects it sideways relative to the tire, and the deflection is the force.

the force builds as the element moves toward the back of the contact patch, until it's bigger than the available friction and the element slides. so most of the force comes from the back half of the patch.

tires also make side force from **camber** (leaning the tire), on its own or combined with slip angle.

## aligning moment and pneumatic trail

since the force builds toward the back of the contact patch, the total side force acts a little behind the center of the patch. that distance is the **pneumatic trail**.

a force acting behind the center twists the tire back toward straight. that twist is the **aligning moment**:

$$M_z = F_y \cdot \text{pneumatic trail}$$

## force lag (relaxation length)

side force doesn't show up instantly when you steer. the sidewalls have to deflect first, which takes about **half to one full wheel revolution**. that distance is the **relaxation length**.

- at 10 revolutions per second, the lag is only about 0.05 s, but expert drivers can feel it as sluggish turn-in
- on rough roads, when load drops the tire slips across the whole patch and has to rebuild force over its relaxation length, so it has less grip on bumpy surfaces
- this is part of why steady-state models miss corner entry

## the full force curve

- 0° slip angle: zero side force
- first 5–10°: force builds fast and in a straight line
- 15–20°: force peaks, at about μ_peak × Fz
- bigger angles: force drops off toward a locked, sliding wheel

**cornering stiffness** is officially the slope of this curve at zero slip angle:

$$C_\alpha = -\left.\frac{\partial F_y}{\partial \alpha}\right|_{\alpha=0}$$

in SAE convention a positive slip angle makes a negative force, so the SAE defines Cα as the negative of the slope. that makes Cα a positive number.

## cornering stiffness and load

**cornering coefficient** = cornering stiffness ÷ load. it's biggest at light loads and drops as load goes up. so doubling the load on a tire doesn't double its cornering stiffness. this is why weight transfer matters for handling.

- radial tires have higher cornering stiffness than bias-ply
- lower-profile tires (lower aspect ratio) have higher cornering coefficients

## summary

a tire only makes cornering force when it's slipping at an angle. more angle means more force, in a straight line at first, until the tire runs out of grip.

## sources

- Gillespie, *Fundamentals of Vehicle Dynamics*, Ch 6 (PDF p. 134, Fig 6.2) and Ch 10 (PDF pp. 209–211)

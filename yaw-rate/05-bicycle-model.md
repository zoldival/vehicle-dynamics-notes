# 05: dynamic bicycle model

the steady-state model from item 3 only works once the car has settled into a corner. on corner entry the yaw rate has to build up, and that takes time because the car has yaw inertia. the dynamic bicycle model adds that, so it can predict yaw rate at every moment, not just in steady corners.

## how it works

1. use speed, steer angle, sideslip and yaw rate to get each axle's slip angle
2. use the slip angles to get each axle's side force (Fy = Cα·α)
3. the side forces push the car sideways and twist it around the CG
4. step forward a tiny bit of time and repeat

## the two states

the model keeps track of two things that change over time:

- **β (beta)** = sideslip angle at the CG, the angle between where the car points and where it's actually going
- **r** = yaw rate

Brian's code tracks **lateral velocity v_y** instead of β. same thing for small angles: v_y ≈ V·β

## variables

| symbol | meaning |
|---|---|
| V | forward speed (m/s) |
| δ | road wheel steer angle (rad) |
| m | mass (kg) |
| Iz | yaw inertia (kg·m²) |
| a | CG to front axle (m) |
| b | CG to rear axle (m) |
| Cf | front axle cornering stiffness (N/rad) |
| Cr | rear axle cornering stiffness (N/rad) |

**note:** the letters change between sources. Gillespie uses b and c, Brian's code uses Lf and Lr, and these notes use a and b.

## slip angles

$$\alpha_f = \delta - \beta - \frac{a \cdot r}{V} \qquad \alpha_r = -\beta + \frac{b \cdot r}{V}$$

front slip angle = steer angle minus the direction the front axle is actually moving.

the a·r/V and b·r/V parts come from rotation. when the car yaws, the front axle swings one way and the rear swings the other.

## tire forces

$$F_{yf} = C_f \cdot \alpha_f \qquad F_{yr} = C_r \cdot \alpha_r$$

same Fy = Cα·α from item 2, one per axle.

## equations of motion

sideways (newton's 2nd law):

$$m V (\dot{\beta} + r) = F_{yf} + F_{yr}$$

rotation (the tire moment equation from item 3):

$$I_z \cdot \dot{r} = a \cdot F_{yf} - b \cdot F_{yr}$$

in steady state ṙ = 0, which gives back Fyf·a = Fyr·b. so the steady-state model is just a special case of this one.

## all together

plugging the slip angles and tire forces into the equations of motion:

$$\dot{\beta} = -\frac{C_f + C_r}{m V}\beta + \left(\frac{b C_r - a C_f}{m V^2} - 1\right) r + \frac{C_f}{m V}\delta$$

$$\dot{r} = \frac{b C_r - a C_f}{I_z}\beta - \frac{a^2 C_f + b^2 C_r}{I_z V} r + \frac{a C_f}{I_z}\delta$$

## stepping forward in time

the code can't solve this in one go, so it steps forward in small chunks of time (dt) using the logged speed and steer angle at each step. simplest way is **euler integration**:

$$\beta_{next} = \beta + \dot{\beta} \cdot dt \qquad r_{next} = r + \dot{r} \cdot dt$$

dt has to be small (matching the data's sample rate is a good start), or the model can blow up.

## what Iz does

Iz is how hard the car is to rotate. bigger Iz means yaw rate builds up slower on corner entry. it doesn't change the final steady-state yaw rate, just how fast the car gets there.

**upper bound for FS:** if all the mass sat right on the axles, Iz = m·a·b = 300 × 0.8535 × 0.7365 ≈ 189 kg·m². the real value has to be smaller.

## how it connects to items 1–4

- **item 1:** with no tire slip, it turns back into r = V·δ/L
- **item 3:** set β̇ and ṙ to 0 and you get Eq 6-22. K = (m/L)·(b/Cf − a/Cr), same idea as Wf/Cαf − Wr/Cαr
- **item 4:** Cf and Cr can depend on tire load instead of being constants
- **item 2:** tire lag can be added later with relaxation length

## limits

- assumes small angles and linear tires, so it gets worse near the grip limit
- fix: cap tire force at μ·Fz, like the tanh curve in Brian's code, or use a full tire model (Pacejka "magic formula")
- Cf, Cr and Iz aren't known yet, so they have to be fit from data. fit on some laps, test on others

## review questions

**what does the dynamic model add that the steady-state one doesn't?**
yaw inertia. it shows how yaw rate builds up over time on corner entry instead of jumping straight to the steady-state value.

**what happens to the dynamic model in a steady corner?**
ṙ = 0, so the moments balance and it gives the same answer as Eq 6-22.

**what does a bigger Iz do?**
yaw rate builds slower, but ends up at the same steady-state value.

**why does the front slip angle have −a·r/V in it?**
when the car rotates, the front axle swings sideways, which changes the direction it's moving and so its slip angle.

## sources

- Rajamani, *Vehicle Dynamics and Control*, Ch 2
- Brian Lee, `double_bicycle_model.py` (Sims-Data, `double_bicycle_model` branch)

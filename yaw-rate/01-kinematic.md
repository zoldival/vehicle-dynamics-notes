# 01: kinematic yaw rate

## what yaw rate is

how fast the car rotates around a vertical axis. it's the rate of change of heading, measured in rad/s or deg/s. a gyro measures it directly.

- when a car starts to **oversteer**, yaw rate goes **up**
- when it **understeers**, yaw rate goes **down**

## yaw rate in a steady corner

in a steady-state corner, the car changes heading at a rate ω (angular velocity) that depends on its speed V and corner radius R:

$$\omega = \frac{V}{R}$$

**why:** one lap covers 2πR at speed V and rotates the car one full turn (2π), so rotation ÷ time = V/R.

step by step:

1. distance of one lap = $2\pi R$
2. time for one lap = distance ÷ speed = $\frac{2\pi R}{V}$
3. rotation in one lap = one full turn = $2\pi$ rad
4. yaw rate = rotation ÷ time:

$$\omega = \frac{2\pi}{2\pi R / V} = \frac{V}{R}$$

the 2π cancels, leaving V/R.

## swapping out R with lateral acceleration

cornering radius is set by speed and lateral acceleration:

$$R = \frac{V^2}{G_{lat}}$$

sub that in for R:

$$\omega = \frac{G_{lat}}{V}$$

this means you can get yaw rate from speed and lateral g, no turn radius needed. (Segers §7.6)

## low-speed geometry: the ackermann angle

at low speed the tires don't slip. the rear wheels don't steer, so they can only roll straight ahead, which means the turn center has to sit on the line extending the rear axle.

the steer angle a car needs to follow a turn when the tires aren't slipping is the **ackermann angle**:

$$\delta = \frac{L}{R}$$

- δ (delta) = steer angle at the road wheels
- L = wheelbase

## the kinematic model

combine ω = V/R and δ = L/R. from δ = L/R, 1/R = δ/L, so:

$$r = \frac{V \cdot \delta}{L}$$

R cancels out completely, so this gives yaw rate from speed and steering alone, no turn radius needed.

what it says:
- more speed → more yaw rate
- more steer → more yaw rate
- longer wheelbase → less yaw rate for the same steer

## where it breaks

- same steering angle, double the speed: the model says yaw rate doubles, but a real car usually gets less, because the tires slip more at speed
- it assumes zero slip angle, but tires have to slip to make side force

## using it on real data

- if measured yaw rate is higher than G_lat / V, the car is **oversteering**: it's rotating more than the cornering force explains

- **steering:** δ is the angle of the wheels on the road, not the steering wheel. fs-3 logs steering wheel angle, so it has to be divided by the steering ratio first. Segers measures this with the car on turn plates and fits a line (his Eq 7.7)
- **units:** δ has to be in radians: deg × π/180
- **gyro location:** it doesn't have to be at the CG for yaw rate. every point on a rigid car rotates at the same rate, so what matters is that the gyro's axis lines up with vertical. location does matter for accelerometers, since lateral g changes with distance from the CG when the car rotates

## quick check

V = 10 m/s, δ = 5°, L = 1.59 m (2025 spec sheet)

1. δ in radians: 5 × π/180 = 0.0873 rad
2. r = V·δ/L = (10 × 0.0873) / 1.59 = **0.549 rad/s**
3. in degrees: 0.549 × 57.3 ≈ **31.5 deg/s**

turn radius that implies: R = L/δ = 1.59 / 0.0873 ≈ 18.2 m

## conventions

SAE axes: x forward, y right, z down

## sources

- Gillespie, *Fundamentals of Vehicle Dynamics*, Ch 6 (PDF p. 133)
- Segers, *Analysis Techniques for Racecar Data Acquisition*, §7.6 (PDF pp. 182–183)

<img width="1668" height="2157" alt="IMG_0299" src="https://github.com/user-attachments/assets/bf3b4471-cb63-41d1-be7b-2be45c4447a3" />


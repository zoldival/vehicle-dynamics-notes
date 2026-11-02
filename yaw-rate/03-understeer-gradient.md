# 03: understeer gradient

at speed, both axles have to slip to make cornering force. whichever axle slips more decides if the car understeers or oversteers, and that balance is the **understeer gradient K**. it turns the kinematic model into one that accounts for tire slip.

## the bicycle model

for high-speed cornering, the two front wheels are treated as one wheel and the two rears as one wheel (a "bicycle").

- b = distance from the front axle to the CG
- c = distance from the CG to the rear axle
- R = turn radius

**note:** Gillespie uses b and c. other papers (and Brian's code) call these a and b.

in a steady corner the car isn't speeding up its rotation, so the moments about the CG balance:

$$F_{yf} \cdot b - F_{yr} \cdot c = 0 \quad\Rightarrow\quad F_{yf} = F_{yr} \cdot \frac{c}{b}$$

## the tire moment equation

in a transient (like corner entry), the moments don't balance, and the leftover moment speeds up the car's rotation:

$$I_z \cdot \dot{r} = F_{yf} \cdot b - F_{yr} \cdot c$$

- Iz = yaw inertia (how hard the car is to rotate)
- ṙ = yaw acceleration

steady state is just the special case where ṙ = 0. this is the core of the dynamic model.

## slip angle on each axle (Eq 6-12, 6-13)

each axle needs a slip angle to make its share of the cornering force:

$$\alpha_f = \frac{W_f V^2}{C_{\alpha f} \, g R} \qquad \alpha_r = \frac{W_r V^2}{C_{\alpha r} \, g R}$$

so slip angle = the load on that axle × lateral g ÷ that axle's cornering stiffness.

## geometry with slip (Eq 6-14)

$$\delta = 57.3 \frac{L}{R} + \alpha_f - \alpha_r$$

steer angle = ackermann angle + front slip − rear slip.

## the understeer gradient (Eq 6-15, 6-16)

$$\delta = 57.3 \frac{L}{R} + K a_y \qquad K = \frac{W_f}{C_{\alpha f}} - \frac{W_r}{C_{\alpha r}}$$

K is made of two terms, each the ratio of the load on an axle (front or rear) to the cornering stiffness of the tires on that axle. it's called the **understeer gradient** and has units of deg/g. this equation is very important to turning response.

| symbol | meaning (Gillespie's units) |
|---|---|
| δ | steer angle at the front wheels (deg) |
| L | wheelbase (ft) |
| R | radius of turn (ft) |
| V | forward speed (ft/s) |
| g | gravity = 32.2 ft/s² |
| Wf | load on the front axle (lb) |
| Wr | load on the rear axle (lb) |
| Cαf | cornering stiffness of the front tires (lb/deg) |
| Cαr | cornering stiffness of the rear tires (lb/deg) |
| K | understeer gradient (deg/g) |
| ay | lateral acceleration (g) |

## three possibilities

### 1. neutral steer

$$\frac{W_f}{C_{\alpha f}} = \frac{W_r}{C_{\alpha r}} \;\Rightarrow\; K = 0 \;\Rightarrow\; \alpha_f = \alpha_r$$

- on a constant-radius turn, no change in steer angle is needed as speed changes
- the steer angle needed is just the ackermann angle, 57.3·L/R
- physically, lateral acceleration at the CG causes an identical increase in slip angle at the front and rear wheels

### 2. understeer

$$\frac{W_f}{C_{\alpha f}} > \frac{W_r}{C_{\alpha r}} \;\Rightarrow\; K > 0 \;\Rightarrow\; \alpha_f > \alpha_r$$

- on a constant-radius turn, steer angle has to increase with speed, in proportion to K times lateral acceleration in g's
- so it increases linearly with lateral acceleration and with the square of speed
- lateral acceleration at the CG makes the front wheels slip sideways more than the rears

### 3. oversteer

$$\frac{W_f}{C_{\alpha f}} < \frac{W_r}{C_{\alpha r}} \;\Rightarrow\; K < 0 \;\Rightarrow\; \alpha_r > \alpha_f$$

- on a constant-radius turn, steer angle has to decrease as speed goes up
- the rear slips out more than the front
- above the **critical speed** the car goes unstable:

$$V_{crit} = \sqrt{\frac{-57.3 \, L g}{K}}$$

## characteristic speed (understeer only)

$$V_{char} = \sqrt{\frac{57.3 \, L g}{K}}$$

the speed where the car needs twice the ackermann angle to make the turn. it's also where the car is most responsive in yaw.

## yaw rate gain (Eq 6-22): the rung 2 model

$$\frac{r}{\delta} = \frac{V / L}{1 + \dfrac{K V^2}{57.3 \, L g}}$$

in radians, with K in rad/g, the 57.3 goes away:

$$\frac{r}{\delta} = \frac{V / L}{1 + \dfrac{K V^2}{L g}}$$

## review questions

**what does K measure in plain english?**
which axle has to slip more per g of cornering. positive means the front slips more (understeer).

**what does Eq 6-22 become when K = 0?**
r = V·δ/L, the kinematic model. a neutral steer car turns exactly like the geometry says.

**why does an understeering car have a "most responsive" speed?**
the top of the equation (V/L) grows with speed, but the K·V² term on the bottom grows faster. at V_char they balance, and after that more speed gives less yaw per degree of steer.

handwritten ones

<img width="953" height="1232" alt="image" src="https://github.com/user-attachments/assets/8746e9ad-2dc2-4c68-8b18-da6a3d03e62c" />

<img width="953" height="1232" alt="image" src="https://github.com/user-attachments/assets/a1d7527d-527d-4c8d-91dd-205b679000a3" />

<img width="953" height="1232" alt="image" src="https://github.com/user-attachments/assets/abd52540-0fdc-4d52-831f-782395d1f27e" />

<img width="953" height="1232" alt="image" src="https://github.com/user-attachments/assets/0a583050-933a-4235-a914-6cfa265421a6" />

<img width="953" height="1232" alt="image" src="https://github.com/user-attachments/assets/e0812d53-1f2c-4e65-8fb2-e99e12b94a14" />

## sources

- Gillespie, *Fundamentals of Vehicle Dynamics*, Ch 6 (PDF pp. 134–138)

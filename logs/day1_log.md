# Engineering Log: Day 1
**Date:** 20 April 2026
**Focus:** Understanding torque and its application in selecting a suitable motor for a quadruped robot leg.

---

## Work Completed

- Studied torque as a rotational force and how it differs from linear force
- Converted motor specifications from kg·cm to SI units (N·m)
- Applied torque equations to estimate lifting capacity at three arm lengths: 2 cm, 5 cm, and 10 cm
- Analyzed how operating voltage (6V vs 4.8V) affects torque output and load capacity

---

## Challenges Faced

**Force vs Torque:** The initial confusion was between force as a linear quantity and torque as a rotational one. Force pushes or pulls in a straight line. Torque is that same force applied at a distance from a pivot. Getting this distinction clear was the first thing that needed sorting before the calculations made sense.

**Visualizing the radius effect:** It was not immediately obvious why a longer arm reduces lifting capability when the motor strength stays the same. Working through the numbers at 2 cm, 5 cm, and 10 cm made it concrete. The torque is fixed, so as the distance grows, the force at the tip has to shrink to compensate.

**Theoretical vs real performance:** The datasheet gives a clean stall torque figure. Understanding why real operating torque is lower, and by how much, took some working through. Heat, friction, and voltage drop under load all pull the actual output below what the spec sheet suggests.

---

## Core Concept

The governing relationship for this entire project:

```
t = F x r

where F = m x g
so:   t = m x g x r
```

This equation connects motor strength directly to load and distance. For a fixed torque, increasing the arm length means less load can be supported. That single relationship drives every leg geometry decision in this project.

---

## Key Insights

Torque is not just force. It is force applied at a distance, and that distance is what makes a motor useful or insufficient for a given leg length.

Arm length is the most sensitive design variable. Going from 2 cm to 10 cm cuts the load capacity by 80 percent at the same voltage. That is not a small adjustment, it is the difference between a functional leg and one that collapses under the robot.

Voltage matters more than expected. The difference between 6V and 4.8V is not just a 20 percent drop in voltage. At 5 cm, it takes the load capacity from 2.6 kg down to 1.88 kg, which falls below the bare per-leg requirement before any safety factor is applied. Battery state during operation is going to be a real consideration.

Real-world torque is lower than rated. Friction in the gear train, heat buildup in the windings, and voltage sag under load all reduce the usable output. The stall torque figure is a ceiling, not an operating point. Designing against 60 to 70 percent of rated torque is more realistic.

---

## Reflection

Going through the torque calculations made clear why motor selection cannot be done by gut feel or by picking the highest rated option available. A motor that looks more than sufficient on a spec sheet can fail under real conditions once leg length, safety margins, and voltage variation are factored in.

The MG996R at 6V is workable for a small quadruped, but the margins are tighter than the raw numbers suggest. That became obvious only after running the numbers at both voltages and across multiple arm lengths.

---

## Conclusions

Day 1 established the quantitative foundation for everything that follows. The torque equation is simple, but the implications of running it at different arm lengths and voltages are what matter. The key conclusion is that leg length is the variable that eats into motor capability fastest, and it needs to be treated as a primary design constraint, not an afterthought.

The 4.8V results in particular flagged something worth carrying forward. If the power supply sags during operation, a 5 cm leg is already below the minimum load requirement before any safety factor. Voltage supply stability needs to be factored into the Day 5 testing setup.

---

## Next Steps

- Apply the robot load requirements (8 kg total, 4 legs, 2 kg per leg) with a safety factor of 2 to formally evaluate motor sufficiency (Day 2)
- Use torque limits to begin constraining leg geometry options
- Carry the voltage sensitivity finding into the experimental design for Day 5

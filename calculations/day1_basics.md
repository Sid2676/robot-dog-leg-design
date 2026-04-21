# Day 1: Torque Analysis and Motor Capability

> Working through the MG996R torque rating, converting it into usable numbers, and figuring out what arm lengths are actually viable before committing to a leg geometry.

---

## Table of Contents

- [Objective](#objective)
- [Why This Motor](#why-this-motor)
- [Converting the Spec Sheet Numbers](#converting-the-spec-sheet-numbers)
- [The Theory](#the-theory)
- [Why These Three Arm Lengths](#why-these-three-arm-lengths)
- [Calculations at 6V](#calculations-at-6v)
- [Calculations at 4.8V](#calculations-at-48v)
- [Results Summary](#results-summary)
- [On Stall Torque](#on-stall-torque)
- [Notes and Observations](#notes-and-observations)
- [Conclusions](#conclusions)

---

## Objective

Before designing anything physical, we needed to answer one question: given the MG996R rated torque, what can it actually support at different arm lengths?

The reason this matters is that torque alone does not tell you much. A spec sheet says 13 kg·cm. That number means nothing without knowing the distance at which the load is applied. This session was about turning that single spec into a set of load limits at real leg lengths, and seeing whether the motor is capable of supporting a small quadruped at all.

---

## Why This Motor

The MG996R was chosen for a few straightforward reasons.

The torque output at 13 kg·cm at 6V is high enough to be worth analyzing for a small quadruped. It is a metal gear servo, so it holds up better under load than plastic gear alternatives like the SG90. It is widely available, runs on standard PWM, and is cheap enough that we can stress test it without worrying about the cost of failure.

More importantly, it is a realistic choice. The goal here is not to use the most powerful servo available and have comfortable margins everywhere. It is to understand what a specific motor can and cannot do, and design within those limits. The MG996R sits right in the range where the design choices actually matter.

In the leg, this servo acts as the joint actuator. It holds the leg in position during stance, rotates the segment during swing, and bears the robot body weight through the joint. If the torque budget is wrong, the joint fails under load. That is why this calculation has to be done before anything gets built.

---

## Converting the Spec Sheet Numbers

Motor datasheets report torque in kg·cm. Physics equations need Newton-meters. Before doing anything else, the numbers have to be in the right units.

```
1 kg.cm = (1 x 9.8) / 100 = 0.0981 N.m

At 6V:   13 x 9.8 / 100 = 1.274 N.m
At 4.8V: 9.4 x 9.8 / 100 = 0.9212 N.m
```

| Supply Voltage | Datasheet Value | SI Value  |
|----------------|-----------------|-----------|
| 6 V            | 13 kg·cm        | 1.274 N·m |
| 4.8 V          | 9.4 kg·cm       | 0.922 N·m |

All calculations from this point use the SI values. The 6V case is the primary reference since that is the operating voltage the design is built around.

---

## The Theory

Torque is the product of force and the distance at which it acts:

```
t = F x r
```

Since force comes from supporting a mass against gravity:

```
F = m x g
```

Combining these:

```
t = m x g x r
```

The motor provides a fixed torque t. Gravity g is constant at 9.8 m/s². That leaves two variables: mass m and radius r. If r is known, we can solve for the maximum mass the motor can hold at that distance:

```
m = t / (g x r)
```

This is the calculation run three times, at three different arm lengths.

---

## Why These Three Arm Lengths

Three arm lengths were chosen to cover the practical range of leg segment sizes for a small quadruped.

| Arm Length | What It Represents |
|------------|--------------------|
| 2 cm       | Very short link. High load capacity but minimal reach. Good as a lower bound reference. |
| 5 cm       | A realistic leg segment for a small robot. The length we are most interested in designing around. |
| 10 cm      | A longer leg for better stride and ground clearance. Included to show how quickly load capacity degrades. |

Running all three makes the trade-off visible rather than abstract.

---

## Calculations at 6V

Using t = 1.274 N·m and m = t / (g x r):

**At r = 2 cm (0.02 m)**

```
1.274 = m x 9.8 x 0.02
m = 1.274 / 0.196
m = 6.5 kg

Lift force = 6.5 x 9.8 = 63.7 N
```

At 2 cm the motor can hold up to 6.5 kg. Plenty of margin, but a 2 cm arm is not a useful leg segment.

**At r = 5 cm (0.05 m)**

```
1.274 = m x 9.8 x 0.05
m = 1.274 / 0.49
m = 2.6 kg

Lift force = 2.6 x 9.8 = 25.48 N
```

At 5 cm load capacity is 2.6 kg. With a per-leg static requirement of 2 kg and a safety factor of 2, the joint needs to handle 4 kg. A 5 cm arm does not clear that bar cleanly.

**At r = 10 cm (0.10 m)**

```
1.274 = m x 9.8 x 0.1
m = 1.274 / 0.98
m = 1.3 kg

Lift force = 1.3 x 9.8 = 12.74 N
```

At 10 cm the motor can only support 1.3 kg. With a 2 kg bare requirement before any safety factor, a 10 cm arm is not viable with this motor.

---

## Calculations at 4.8V

Using t = 0.9212 N·m. Same method, lower torque input.

**At r = 2 cm (0.02 m)**

```
m = 0.9212 / (9.8 x 0.02)
m = 0.9212 / 0.196
m = 4.7 kg
```

**At r = 5 cm (0.05 m)**

```
m = 0.9212 / (9.8 x 0.05)
m = 0.9212 / 0.49
m = 1.88 kg
```

At 4.8V a 5 cm arm cannot even meet the bare 2 kg per-leg requirement before the safety factor is applied.

**At r = 10 cm (0.10 m)**

```
m = 0.9212 / (9.8 x 0.1)
m = 0.9212 / 0.98
m = 0.94 kg
```

---

## Results Summary

| Arm Length | Load at 6V | Load at 4.8V |
|------------|------------|--------------|
| 2 cm       | 6.5 kg     | 4.7 kg       |
| 5 cm       | 2.6 kg     | 1.88 kg      |
| 10 cm      | 1.3 kg     | 0.94 kg      |

The relationship is inversely proportional. Doubling the arm length halves the load capacity. The voltage difference is significant enough to affect design decisions, particularly around battery state during operation.

---

## On Stall Torque

The 13 kg·cm on the datasheet is the stall torque, meaning the peak output when the shaft is completely stationary. The motor cannot sustain this continuously without overheating.

In real operation, usable torque sits closer to 60 to 70 percent of the rated figure. The load values calculated above are theoretical ceilings, not safe operating targets. This is precisely why a safety factor gets applied in Day 2.

---

## Notes and Observations

The 4.8V case was included because the robot will not always run at a full 6V, especially as the battery discharges under load. The drop in capacity is significant enough to treat voltage supply as a design variable, not just an environmental condition.

The 10 cm arm result at either voltage shows that a longer leg would need a noticeably stronger motor. If the design ever scales up, motor selection gets revisited before leg geometry.

---

## Conclusions

A few things became clear by the end of Day 1.

The MG996R at 6V has enough torque on paper, but the usable margin is tighter than the raw numbers suggest. At 5 cm the theoretical load is 2.6 kg. With a safety factor of 2 and real operating torque sitting at 60 to 70 percent of stall, that margin gets uncomfortable quickly. Leg length is the most sensitive variable in the whole design.

The 4.8V case was worth running. The load capacity drops enough that a 5 cm arm cannot meet the bare 2 kg per-leg requirement before any safety factor is applied. Running this robot off a partially discharged battery is not a small concern, it is a design consideration that needs to be carried into the testing phase.

The core takeaway from today is simple: torque is fixed, distance is the variable, and every centimeter of leg length costs load capacity. That trade-off runs through every decision from here on.

# Day 1: Understanding Torque and Motor Capability

## Objective
The goal of this study is to understand how a servo motor’s torque translates into real-world lifting capability, and how arm length (leg length) affects performance.

This forms the foundation for designing a quadruped robot leg.

---

## Why This Motor?

We selected the **TowerPro MG996R servo motor** because:

- It is widely used in robotics projects
- It provides relatively high torque at low cost
- It is suitable for small to medium load applications like robotic legs

### Motor Specifications

- Stall Torque @ 6V = 13 kg·cm  
- Stall Torque @ 4.8V = 9.4 kg·cm  

### What This Means

This torque value represents the **maximum rotational force** the motor can provide when it is not moving (stall condition).

👉 However, in real applications, the motor operates below this value.

---

## Why Convert to SI Units?

Motor datasheets use **kg·cm**, but engineering calculations require **Newton-meters (Nm)**.

Conversion:

1 kg·cm = 0.098 Nm  

- At 6V → 1.274 Nm  
- At 4.8V → 0.9212 Nm  

👉 This allows us to use physics equations correctly.

---

## Core Theory

Torque defines how much rotational force a motor can apply:

τ = F × r  

Where:
- F = force
- r = distance from pivot (lever arm)

Also:

F = m × g  

So:

τ = m × g × r  

---

## Why We Chose 2 cm, 5 cm, 10 cm

These values simulate **different leg lengths**:

| Length | Meaning |
|------|--------|
| 2 cm | Very short link (high strength, low reach) |
| 5 cm | Practical robot leg segment |
| 10 cm | Long leg (realistic but weaker) |

👉 This helps us understand **design trade-offs**:
- Stability vs reach
- Strength vs mobility

---

## Calculations (Explained Step-by-Step)

### Formula Used

\tau = m \cdot g \cdot r

Where:
- τ = torque (Nm) → from motor specification  
- m = mass (kg) → what we are solving  
- g = 9.8 m/s² → gravity  
- r = distance from motor shaft (meters)  

---

## Case 1: Using 6V Torque (1.274 Nm)

---

### 🔹 At 2 cm (0.02 m)

Why 0.02?  
👉 2 cm = 0.02 meters (converted to SI units)

Substitute into formula:

1.274 = m × 9.8 × 0.02  

Step-by-step:

m = 1.274 / (9.8 × 0.02)  
m = 1.274 / 0.196  
m ≈ 6.5 kg  

Now calculate force:

F = m × g = 6.5 × 9.8 ≈ 63.7 N  

👉 Meaning:  
At 2 cm, the motor can lift about **6.5 kg**

---

### 🔹 At 5 cm (0.05 m)

Convert:
5 cm = 0.05 m  

1.274 = m × 9.8 × 0.05  

m = 1.274 / (9.8 × 0.05)  
m = 1.274 / 0.49  
m ≈ 2.6 kg  

Force:
F = 2.6 × 9.8 ≈ 25.48 N  

👉 Meaning:  
At 5 cm, lifting capacity drops to **2.6 kg**

---

### 🔹 At 10 cm (0.1 m)

Convert:
10 cm = 0.1 m  

1.274 = m × 9.8 × 0.1  

m = 1.274 / (9.8 × 0.1)  
m = 1.274 / 0.98  
m ≈ 1.3 kg  

Force:
F = 1.3 × 9.8 ≈ 12.74 N  

👉 Meaning:  
At 10 cm, motor can lift only **1.3 kg**

---

## Case 2: Using 4.8V Torque (0.9212 Nm)

Same formula, lower torque → lower results

---

### 🔹 At 2 cm

m = 0.9212 / (9.8 × 0.02)  
m ≈ 4.7 kg  

👉 Lower than 6V case

---

### 🔹 At 5 cm

m = 0.9212 / (9.8 × 0.05)  
m ≈ 1.88 kg  

---

### 🔹 At 10 cm

m = 0.9212 / (9.8 × 0.1)  
m ≈ 0.94 kg  

---

## Final Understanding

- Torque (τ) is fixed for a given motor  
- As distance (r) increases → mass (m) must decrease  
- This is why longer robot legs are weaker  

👉 This directly affects quadruped design decisions
## Key Insights

### 1. Length vs Strength Trade-off
Increasing leg length reduces lifting capability.

👉 This is the most important takeaway for leg design.

---

### 2. Voltage Matters
Lower voltage → lower torque → weaker robot

---

### 3. Torque ≠ Actual Performance
These values are based on **stall torque**

---

## Practical Reality (Very Important)

In real-world conditions:

- Motors cannot operate at stall torque continuously  
- Heat and friction reduce performance  
- Power supply is not ideal  

👉 Usable torque ≈ **60–70% of rated torque**

---

## What This Means for Our Robot

This analysis helps us answer:

- Can this motor lift the robot?  
- What should be the leg length?  
- Is this motor sufficient or not?  

👉 These questions will be answered in **Day 2**

---

## Conclusion

- Torque determines lifting capability  
- Arm length directly affects usable force  
- Voltage impacts motor performance  
- Real-world performance is lower than theoretical  

This analysis forms the **foundation for designing the quadruped leg system**.

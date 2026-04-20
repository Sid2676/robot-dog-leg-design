# 🔧 Day 1 – Engineering Log (Robotic Leg Project)

## 📌 Focus
Understanding torque and its application in selecting a suitable motor for a quadruped robot leg.

---

## ⚙️ Work Completed

- Studied the concept of torque as a rotational force  
- Converted motor specifications from kg·cm to SI units (Nm)  
- Applied torque equations to estimate lifting capacity at different arm lengths (2 cm, 5 cm, 10 cm)  
- Analyzed how motor voltage (6V vs 4.8V) affects torque output  

---

## ⚠️ Challenges Faced

- Initially confused **force (linear)** vs **torque (rotational)**  
- Difficulty visualizing how **distance from the joint (radius)** affects lifting capability  
- Understanding why theoretical torque differs from real-world performance  

---

## 💡 Key Insights

- Torque is **force applied at a distance**, not just force alone  
- Increasing arm length significantly reduces lifting capacity  
- Motor performance depends heavily on **supply voltage**  
- Real-world torque is lower due to:
  - friction  
  - heat losses  
  - inefficiencies in the system  

---

## 📊 Core Concept

Torque relationship:

τ = F × r  

Where:
- F = m × g  
- τ = m × g × r  

👉 This equation connects motor strength with load and distance.

---

## 🔍 Reflection

Understanding torque provided clarity on **why motor selection is critical** in robot design.

Even if a motor appears strong based on specifications, it may fail when:
- the leg length is too large  
- the load exceeds practical limits  
- real-world losses are considered  

This highlights the importance of combining **theory with practical constraints**.

---

## ➡️ Next Steps

- Use these calculations to evaluate if the motor can support the robot weight (Day 2)  
- Introduce a safety factor (1.5×–2×) in torque calculations  
- Begin translating torque limits into **leg design constraints**  

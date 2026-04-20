# 🐾 Quadruped Robot Leg Design

> Designing, analyzing, and validating a servo-driven robotic leg through a complete engineering workflow.

---

## 📌 Overview

This project focuses on building a **single leg of a quadruped robot** by combining theory, calculations, and real-world validation.

The goal is not just to build a mechanism, but to understand how **motor capability, load, and geometry interact** in robotic systems.

---

## 🎯 Objectives

- Understand torque and its real-world limitations  
- Convert motor specifications into usable engineering values  
- Analyze how leg length affects lifting capability  
- Design a functional robotic leg within torque constraints  
- Validate theoretical results through experiments  

---

## ⚙️ Motor Details

**Motor Used:** TowerPro MG996R Servo Motor  

| Voltage | Torque |
|--------|--------|
| 6V     | 13 kg·cm |
| 4.8V   | 9.4 kg·cm |

### 🔍 Role in the Robot

This motor acts as the **joint actuator**:
- Lifts and supports the robot’s weight  
- Controls leg movement  
- Determines the strength and stability of the leg  

👉 Motor selection directly impacts whether the robot can **stand, walk, or fail**

---

## 🧠 Key Insight (Day 1)

From torque calculations:

| Arm Length | Max Load (6V) |
|-----------|--------------|
| 2 cm      | 6.5 kg       |
| 5 cm      | 2.6 kg       |
| 10 cm     | 1.3 kg       |

### 🔥 Important Takeaway

- Increasing leg length reduces lifting capacity  
- Torque is constant, but **force decreases with distance**  

👉 This is the **core constraint in quadruped leg design**

---

## 📂 Project Structure


/calculations    → torque calculations and analysis
/comparisons     → motor comparison
/design          → leg geometry and CAD
/experiments     → validation and testing
/prototype       → physical build
/report          → final documentation
/videos          → explanation videos
/logs            → daily engineering logs



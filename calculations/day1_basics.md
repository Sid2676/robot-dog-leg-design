# Day 1: Understanding Torque

## Objective
To analyze the torque capabilities of the servo motor and determine its lifting capacity at different arm lengths.

---

## Motor Specification
Motor: TowerPro MG996R

- Stall Torque @ 6V = 13 kg·cm  
- Stall Torque @ 4.8V = 9.4 kg·cm  

---

## Conversion to SI Units

1 kg·cm = 9.8 × 0.01 = 0.098 Nm  

### At 6V:
13 × 0.098 = 1.274 Nm  

### At 4.8V:
9.4 × 0.098 = 0.9212 Nm  

---

## Theory

Torque is the rotational equivalent of force:

τ = F × r  

Also:

F = m × g  

Therefore:

τ = m × g × r  

Where:
- τ = torque (Nm)
- m = mass (kg)
- g = 9.8 m/s²
- r = distance from pivot (m)

---

## Calculations (Using 6V Torque)

### At 2 cm (0.02 m)
1.274 = m × 9.8 × 0.02  
m = 6.5 kg  

Force = 6.5 × 9.8 = 63.7 N  

---

### At 5 cm (0.05 m)
1.274 = m × 9.8 × 0.05  
m = 2.6 kg  

Force = 2.6 × 9.8 = 25.48 N  

---

### At 10 cm (0.1 m)
1.274 = m × 9.8 × 0.1  
m = 1.3 kg  

Force = 1.3 × 9.8 = 12.74 N  

---

## Calculations (Using 4.8V Torque)

### At 2 cm (0.02 m)
0.9212 = m × 9.8 × 0.02  
m ≈ 4.7 kg  

Force ≈ 46.06 N  

---

### At 5 cm (0.05 m)
0.9212 = m × 9.8 × 0.05  
m ≈ 1.88 kg  

Force ≈ 18.42 N  

---

### At 10 cm (0.1 m)
0.9212 = m × 9.8 × 0.1  
m ≈ 0.94 kg  

Force ≈ 9.21 N  

---

## Observations

- Increasing arm length reduces lifting capacity  
- Torque remains constant, but force decreases with radius  
- Lower voltage reduces motor performance  

---

## Practical Considerations

The given torque values are **stall torque**, which represents the maximum torque when the motor is not rotating.

In real-world conditions:
- Motors do not operate continuously at stall torque  
- Losses occur due to friction, heat, and voltage drops  
- Usable torque is approximately **60–70% of rated torque**

Therefore, actual lifting capacity will be lower than calculated values.

---

## Conclusion

- Torque is highly dependent on arm length and supply voltage  
- Shorter arm lengths provide higher lifting force  
- Practical designs must consider reduced usable torque  

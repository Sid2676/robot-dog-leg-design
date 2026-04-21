Quadruped Robot Leg Design
Overview
This project works through the design and validation of a single leg for a quadruped robot. The idea was to not just build something that moves, but to actually understand the numbers behind it — what the motor can handle, how leg geometry affects that, and where things break down if you get it wrong.
The work goes from reading a datasheet and doing torque calculations, all the way to building a physical prototype and comparing it against what the math predicted.

Problem Statement
Most hobby quadruped builds either overspec the motors out of guesswork or underspec them and wonder why the legs collapse. The actual question we wanted to answer was: given a fixed motor, what leg geometry is physically achievable, and can a standard servo like the MG996R realistically support a small quadruped under real load?
That question drives everything in this project.

Assumptions
These are the working assumptions used throughout the calculations and design:

The robot's total mass is taken as 8 kg, distributed equally across 4 legs — so 2 kg per leg under static load
A safety factor of 2 is applied, meaning the motor must handle twice the calculated minimum torque
The motor is operated at 6 V unless stated otherwise, corresponding to its rated peak torque of 13 kg·cm
Torque calculations treat the leg as a rigid arm rotating about the servo shaft — no flex, no linkage losses
Load is applied perpendicular to the arm, which gives the worst-case torque condition
Stall torque from the datasheet is used as the upper limit; continuous operating torque will be lower in practice


Objectives

Get a clear, practical understanding of torque and what it actually limits in a servo-driven joint
Convert motor specs from datasheet units into SI and verify the numbers make sense
Figure out what leg lengths are viable given the motor's torque rating
Design a leg geometry that stays within those limits with margin to spare
Build and test it, then compare the results against the calculations


Actuator Specifications
Motor: TowerPro MG996R Servo
Supply VoltageStall TorqueStall Torque (SI)6 V13 kg·cm1.275 N·m4.8 V9.4 kg·cm0.922 N·m
The conversion used is: 1 kg·cm = 0.0981 N·m, so 13 kg·cm × 0.0981 = 1.275 N·m at 6 V. All subsequent force and torque calculations are done in SI units (N, m, N·m) for consistency.
The MG996R handles both load-bearing and joint actuation. It is the single point of mechanical failure if undersized — which is why the torque budget needs to be verified before anything gets built.

Torque Analysis
The governing relationship is:
τ = F × r
Where τ is the available torque (fixed by the motor), F is the force the joint can support, and r is the effective arm length. Since τ is constant, F drops as r increases. A longer leg means less load capacity at the joint — that is the core trade-off in this design.
At 6 V, the maximum supportable load at three reference arm lengths:
Effective Arm LengthMax Supportable Load2 cm6.5 kg5 cm2.6 kg10 cm1.3 kg
Given the per-leg requirement of 2 kg with a safety factor of 2 (i.e., the joint must handle 4 kg effective load), a 5 cm leg is right at the edge and a 10 cm leg is not viable with this motor. This directly constrains the geometry explored in Day 4.

Repository Structure
/calculations    — Torque analysis and load calculations
/comparisons     — Motor selection and specification comparisons
/design          — Leg geometry and CAD models
/experiments     — Validation data and testing records
/prototype       — Physical build documentation
/report          — Final engineering report
/videos          — Technical explanation recordings
/logs            — Daily engineering logs

Status
Active development. Day 1 complete — torque analysis and base calculations done. Physical build and validation ongoing.


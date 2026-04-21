# Quadruped Robot Leg Design

> A complete engineering workflow covering torque analysis, leg geometry design, motor validation, and prototype testing for a servo-driven quadruped leg.

---

## Table of Contents

- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Assumptions](#assumptions)
- [Objectives](#objectives)
- [Actuator Specifications](#actuator-specifications)
- [Torque Analysis](#torque-analysis)
- [Repository Structure](#repository-structure)
- [Project Status](#project-status)

---

## Overview

This project works through the design and validation of a single leg for a quadruped robot. The goal was not just to build something that moves, but to actually understand the numbers behind it: what the motor can handle, how leg geometry affects that, and where things break down if you get it wrong.

The work covers everything from reading a datasheet and running torque calculations, through to building a physical prototype and comparing the results against what the math predicted.

---

## Problem Statement

Most hobby quadruped builds either overspec the motors out of guesswork or underspec them and wonder why the legs collapse. The question this project sets out to answer is: given a fixed motor, what leg geometry is physically achievable, and can a standard servo like the MG996R realistically support a small quadruped under real load?

That question drives every decision made here.

---

## Assumptions

The following assumptions are used consistently across all calculations and design decisions:

- Total robot mass is 8 kg, distributed equally across 4 legs, giving 2 kg per leg under static load
- A safety factor of 2 is applied throughout, so the motor must handle twice the calculated minimum torque
- The motor is operated at 6 V unless stated otherwise, corresponding to its rated peak torque of 13 kg·cm
- Torque calculations model the leg as a rigid arm rotating about the servo shaft, with no flex and no linkage losses
- Load is applied perpendicular to the arm, representing the worst-case torque condition
- Stall torque from the datasheet is treated as the upper limit; actual continuous operating torque will be lower

---

## Objectives

- Build a practical understanding of torque and what it limits in a servo-driven joint
- Convert motor specifications from datasheet units into SI and verify the values make sense
- Determine which leg lengths are viable given the motor's torque rating
- Design a leg geometry that stays within those limits with enough margin to be safe
- Build and test the leg, then compare the physical results against the theoretical predictions

---

## Actuator Specifications

**Motor:** TowerPro MG996R Servo

| Supply Voltage | Stall Torque | Stall Torque (SI) |
|----------------|--------------|-------------------|
| 6 V            | 13 kg·cm     | 1.275 N·m         |
| 4.8 V          | 9.4 kg·cm    | 0.922 N·m         |

Conversion used: 1 kg·cm = 0.0981 N·m, so 13 kg·cm x 0.0981 = 1.275 N·m at 6 V. All force and torque calculations in this project use SI units (N, m, N·m) for consistency.

The MG996R serves as both the load-bearing element and the joint actuator. If it is undersized for the application, it becomes the first point of failure in the entire leg. This is why verifying the torque budget before building is non-negotiable.

---

## Torque Analysis

The governing relationship used throughout this project is:

```
t = F x r
```

Where `t` is the available torque (fixed by the motor), `F` is the force the joint can support, and `r` is the effective arm length. Since torque is constant, force decreases as arm length increases. A longer leg gives better reach but reduces the load the joint can carry. That trade-off is the central design constraint.

At 6 V, the maximum supportable load at three reference arm lengths is as follows:

| Effective Arm Length | Max Supportable Load |
|----------------------|----------------------|
| 2 cm                 | 6.5 kg               |
| 5 cm                 | 2.6 kg               |
| 10 cm                | 1.3 kg               |

With a per-leg requirement of 2 kg and a safety factor of 2, the joint needs to handle an effective load of 4 kg. A 5 cm leg sits right at the boundary and a 10 cm leg is not achievable with this motor. These results directly constrain the geometry developed in Day 4.

---

## Repository Structure

```
quadruped-leg/
|
├── calculations/          # Torque analysis and load calculations
│   └── day1_basics/
│
├── comparisons/           # Motor selection and specification comparisons
│   └── day3_motor_selection/
│
├── design/                # Leg geometry and CAD models
│   └── day4_leg_geometry/
│
├── experiments/           # Validation data and test records
│   └── day5_validation/
│
├── prototype/             # Physical build documentation
│   └── day6_leg_build/
│
├── report/                # Final engineering report
├── videos/                # Explanation recordings
└── logs/                  # Daily engineering logs
```

---

## Project Status

| Day | Task | Status |
|-----|------|--------|
| Day 1 | Torque fundamentals, SI conversion, load calculations | Complete |
| Day 2 | Robot load analysis, motor sufficiency check | Pending |
| Day 3 | Motor comparison (MG996R vs second motor) | Pending |
| Day 4 | Leg geometry and single-DOF design | Pending |
| Day 5 | Physical experiment and validation | Pending |
| Day 6 | Prototype build and testing | Pending |
| Day 7 | Final report and documentation | Pending |


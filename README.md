# An Autonomous Maze Solver Robot

> An autonomous maze-solving robot built using a **Teensy 4.0 microcontroller, VL53L1X Time-of-Flight sensors, TB6612FNG motor driver, encoder motors, PID-based wall following, and a custom-designed PCB**.

The robot autonomously detects maze walls, identifies available paths, maintains its position inside corridors, performs controlled turns, and navigates through structured maze environments using real-time sensor feedback.

---

## Project Overview

Maze-solving robots are autonomous mobile robots designed to navigate through a maze without continuous human control.

A maze robot must continuously:

- Detect walls and open paths
- Measure the distance from surrounding obstacles
- Maintain proper alignment inside maze corridors
- Make real-time navigation decisions
- Move a fixed distance accurately
- Perform controlled left, right, and turnaround movements

This project implements an autonomous maze-solving robot using **three VL53L1X laser distance sensors** for wall detection and **wheel encoders** for accurate movement.

The robot uses a **PID-based wall-following algorithm** to maintain its position inside maze corridors. Encoder feedback is used to control the travel distance and improve turning accuracy.

A custom-designed PCB integrates the controller, motor driver, sensor interfaces, encoder connections, power system, push buttons, and status LEDs into a compact robotics platform.

---

# Project Objectives

- Develop an autonomous robot capable of navigating a structured maze.
- Detect walls and open paths in real time.
- Use distance sensors for front, left, and right wall detection.
- Maintain the robot near the center of the maze corridor.
- Reduce wall collisions and movement deviation.
- Implement PID-based wall-following control.
- Use wheel encoders for accurate distance measurement.
- Perform accurate left, right, and turnaround movements.
- Develop a compact custom PCB for the robot controller.
- Improve movement stability using real-time sensor feedback.
- Create a modular platform for robotics competitions and embedded systems learning.

---

# Our Solution — Maze Solver Robot

The Maze Solver Robot acts as an autonomous navigation system that continuously observes its surroundings and makes movement decisions based on real-time distance measurements.

The robot uses:

- A **front VL53L1X sensor** to detect walls and obstacles ahead.
- A **left VL53L1X sensor** to measure the distance from the left wall.
- A **right VL53L1X sensor** to measure the distance from the right wall.
- **PID control** to maintain proper alignment inside maze corridors.
- **Wheel encoders** to measure movement and control rotation.
- A **TB6612FNG motor driver** to independently control the left and right motors.
- A **Teensy 4.0 microcontroller** to process sensor information and execute navigation logic.

The robot continuously checks the maze environment and follows the programmed navigation rules.

For example:

> “If the front path is clear, move forward.”

> “If the front path is blocked, turn toward the open side.”

> “If the front and both sides are blocked, perform a turnaround.”

The system performs these operations autonomously without requiring continuous manual control.

---

# System Architecture

                    ┌──────────────────┐
                    │ VL53L1X Front    │
                    │ Distance Sensor  │
                    └────────┬─────────┘
                             │
                             ▼
┌────────────────┐    ┌───────────────┐    ┌────────────────┐
│ VL53L1X Left   │───▶│   Teensy 4.0  │◀───│ VL53L1X Right  │
│ Distance Sensor│    │ Microcontroller│    │ Distance Sensor│
└────────────────┘    └───────┬───────┘    └────────────────┘
                              │
                              ▼
                    ┌──────────────────┐
                    │ Navigation Logic │
                    │ PID Control      │
                    │ Wall Detection   │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │    TB6612FNG     │
                    │   Motor Driver   │
                    └───────┬───┬──────┘
                            │   │
                         ┌──▼┐ ┌▼──┐
                         │Left│ │Right
                         │Motor│Motor
                         └──┬─┘ └─┬──┘
                            │     │
                         ┌──▼─────▼──┐
                         │  Encoders │
                         └─────┬─────┘
                               │
                               ▼
                         Teensy 4.0

---

# Key Features

## Autonomous Maze Navigation

The robot independently detects available paths and makes movement decisions.

### Navigation Rules

1. If the front path is clear, move forward.
2. If the front path is blocked, check the left and right sides.
3. Turn toward the side with more available space.
4. If the front, left, and right sides are blocked, perform a turnaround.
5. Continue navigating through the maze.

This enables the robot to move autonomously through structured maze environments.

---

## Real-Time Wall Detection

The robot uses three **VL53L1X Time-of-Flight distance sensors**.

| Sensor | Position | Function |
|---|---|---|
| VL53L1X – Front | Front | Detects walls and obstacles ahead |
| VL53L1X – Left | Left side | Measures distance from the left wall |
| VL53L1X – Right | Right side | Measures distance from the right wall |

The sensors help the robot identify:

- Open paths
- Maze walls
- Left turns
- Right turns
- Dead ends
- Corridor boundaries
- Obstacles in front of the robot

---

## PID-Based Wall Following

The robot uses PID-based control to maintain proper alignment inside the maze.

The wall-following error is calculated using the left and right sensor measurements.

Error = Left Distance − Right Distance

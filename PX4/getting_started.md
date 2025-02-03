# PX4 Basics
- This document represents my understanding of PX4 and drones in general, with a primary focus on quadcopters.

## PX4 documentation
- The official documentation can be found on the PX4 website.
- [Px4 Documentation](https://docs.px4.io/main/en/getting_started/px4_basic_concepts.html)

## Drone in general
- A drone typically operates with flight firmware running on a flight controller, which manages both manual control and essential autonomous functions such as takeoff, landing, and basic navigation. The firmware interprets pilot commands, processes sensor data, and ensures stable flight by continuously adjusting motor outputs.
- In advanced drones, additional coprocessors may be used for tasks such as high-level flight planning, machine vision, real-time image processing, and advanced autonomous capabilities. These coprocessors enhance performance by handling complex computations independently from the main flight controller.

## PX4 Stack
- PX4 runs on the NuttX RTOS.  
- It offers advanced flight modes and robust safety features.  
- Companion computers can communicate with PX4 using ROS2 and MAVSDK.  
- It supports QGroundControl (QGC), a ground-based software for monitoring and controlling the vehicle.

## PX4 Drone APIs
- The Drone API enables control of a PX4-powered drone without requiring an understanding of its internal flight stack.  
- These APIs can run on a companion computer, allowing for advanced control, high-level automation, and integration with external systems such as AI-based navigation, real-time data processing, and mission planning.

- PX4 mainly supports **MAVSDK** and **ROS2**. 

## ROS2 & MAVSDK
### ROS2
- A general-purpose robotics framework extended for drone applications.
- Provides low-latency communication, essential for real-time control.
- Supports C++ and Python for flexible development.
- Well-suited for vision-based systems and AI-driven applications.
- Enables quick development by leveraging existing ROS2 modules and libraries.
- Still under development, with the message interface not being well-maintained or fully synchronized with PX4.
### MAVSDK
- MAVSDK APIs are optimized to run efficiently on low-end hardware.
- Has a smaller learning curve compared to ROS2, making it easier to adopt.
- Supports multiple programming languages, including C++, Python, Java, and more.
- Provides high-level drone control abstractions while maintaining performance efficiency.


# 🌦️ Multithreaded Weather Monitoring Simulation

![Language](https://img.shields.io/badge/language-C++-blue.svg)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey.svg)
![Course](https://img.shields.io/badge/Course-Operating%20Systems-orange.svg)
![Status](https://img.shields.io/badge/Status-Completed-green.svg)

A concurrent C++ application that simulates a real-time weather monitoring system. This project demonstrates core Operating System concepts including **multithreading**, **synchronization**, **producer-consumer patterns**, and **shared memory management**.

Implemented for the Operating Systems Multithreaded Programming Project.

---

## 📑 Table of Contents
- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Prerequisites](#-prerequisites)
- [Performance Analysis](#-performance-analysis)
- [Build & Run](#-build--run)


---

## 🔭 Overview

In this simulation, multiple "Sensor" threads generate synthetic weather data (temperature and humidity) concurrently. A central "Aggregator" thread processes these readings to calculate statistics, while a "Visualizer" thread renders a live dashboard to the console.

The project satisfies the course requirements by utilizing:
- **3+ Threads:** Sensors, Aggregator, and Visualizer.
- **Synchronization:** Mutexes and Condition Variables to prevent race conditions.
- **Performance Logging:** Real-time throughput calculation.

---

## ✨ Features

* **Multi-Sensor Simulation:** Spawns multiple worker threads to act as independent weather sensors.
* **Thread-Safe Data Pipeline:** Uses a shared, synchronized queue to transport data between threads.
* **Real-Time Dashboard:** Displays live statistics in the terminal, including:
    * Average Temperature & Humidity
    * Peak (High) & Low Temperatures
    * Total Readings Processed
    * System Throughput (Readings/sec)
* **Graceful Shutdown:** Ensures all threads finish their tasks and join safely upon user termination.

---

## 🏗️ Architecture

The system implements the **Producer-Consumer** pattern:


1.  **Producers (Sensors):** Generate `WeatherReading` objects and push them to a thread-safe queue.
2.  **Consumer (Aggregator):** Waits for data via a `std::condition_variable`, processes readings, and updates global statistics protected by a `std::mutex`.
3.  **Observer (Visualizer):** Periodically locks the stats mutex to read the current state and print the dashboard.

### Technologies Used
* **C++11/17**: Core language.
* **Standard Library**: `<thread>`, `<mutex>`, `<condition_variable>`, `<queue>`, `<atomic>`.

---

## ⚙️ Prerequisites

* **C++ Compiler**: GCC (`g++`) or MSVC supporting C++11 or later.
* **Make** (Optional): For easier build management.
* **OS**: Windows (MinGW/MSVC) or Linux.

---

## 📊 Performance Analysis
The application tracks Throughput (Readings Processed per Second) to measure the efficiency of the multithreaded design.

Low Contention: With sleep intervals in sensor threads, throughput is limited by data generation speed.

High Contention: With 0ms sleep intervals, throughput is limited by the mutex lock overhead on the shared queue.

---


## 🚀 Build & Run

### Compiling manually (g++)

If you are using MinGW (Windows) or Linux:

```bash
# Compile the source code
g++ -o weather_simulation weather_simulation.cpp -std=c++11 -pthread

# Run the executable
./weather_simulation

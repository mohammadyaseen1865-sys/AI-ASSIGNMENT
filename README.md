# Smart Traffic Signal Controller (AI Simulation)

A runnable Python simulation of a **Smart Traffic Signal Controller** designed to reduce congestion at an urban road intersection. This project implements a simple rule-based intelligent agent using the PEAS specification from the assignment.

## Features

- Observes vehicle queues on North, South, East, and West lanes (simulated sensors).
- Selects the lane with the largest queue to reduce congestion.
- Gives priority to an emergency vehicle when one is reported.
- Adjusts green-light duration according to the selected lane's queue.
- Simulates changing traffic arrivals and vehicle departures.
- Reports vehicles served, waiting time, traffic-flow efficiency, and utility.
- Supports readable terminal output and JSON output.

## Requirements

- Python 3.8 or newer
- No third-party Python packages are required.

## Project structure

```text
smart-traffic-signal-controller/
├── main.py
├── README.md
└── requirements.txt
```

## How to run

### 1. Download or clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd smart-traffic-signal-controller
```

Replace `<YOUR_GITHUB_REPOSITORY_URL>` with the HTTPS URL of your GitHub repository.

### 2. Run the program

```bash
python main.py
```

If your computer uses `python3` instead of `python`, run:

```bash
python3 main.py
```

### 3. Optional commands

Run 15 cycles with repeatable random traffic:

```bash
python main.py --steps 15 --seed 7
```

Simulate an emergency vehicle arriving in the East lane at cycle 3:

```bash
python main.py --steps 10 --emergency-step 3
```

Get machine-readable JSON output:

```bash
python main.py --steps 10 --seed 7 --json
```

## How the AI agent works

1. **Perception:** Reads the simulated number of vehicles in each lane.
2. **Decision:** Selects the lane with the longest queue. If an emergency vehicle is present, its lane is selected first.
3. **Action:** Turns the selected lane's light green for a calculated duration and serves vehicles.
4. **Learning/environment update:** New vehicles arrive randomly, so the traffic state changes after every cycle. This is a simulation, not a trained machine-learning model.

## PEAS specification

| PEAS element | Project implementation |
|---|---|
| Performance measures | Vehicle waiting time, vehicles served (throughput), emergency priority, traffic-flow efficiency |
| Environment | Four-way urban intersection with changing traffic |
| Actuators | Simulated traffic lights and green-light duration |
| Sensors | Simulated vehicle-queue observations representing CCTV/inductive-loop data |

## Task environment classification

- **Partially observable:** The simulation observes queue counts, not every real-world road condition.
- **Multi-agent:** Vehicles and the signal controller interact.
- **Stochastic:** New vehicle arrivals are random.
- **Sequential:** Each signal decision affects later queues.
- **Dynamic:** Queues change during each cycle.
- **Continuous (real-world specification):** Time and traffic flow are continuous in the real system; this simplified program uses discrete simulation cycles.

## Utility function

The assignment specifies:

```text
U = 0.7 × traffic_flow_efficiency − 0.3 × average_wait_time
```

The program calculates a demonstration utility using a normalized traffic-flow-efficiency score and average accumulated waiting per cycle. Since the waiting-time term is measured in simulation units, the utility is an illustrative score rather than a calibrated real-world metric.

## Important note

This is an educational simulation. It does **not** connect to physical traffic lights, CCTV cameras, GPS services, or emergency communication networks. Real deployment would require certified hardware, safety controls, real sensor integration, and extensive testing.

## Author

Mohammad Yaseen  
Department of Computer Science  
University of Sindh, Jamshoro

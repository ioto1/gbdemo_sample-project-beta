# Project Beta — Franka Simulation Suite

> High-fidelity physics simulation for Franka robots — test your code without hardware.

## Overview

Project Beta provides a Gazebo-based simulation environment for Franka Emika robots.
It wraps the official `franka_ros` packages with pre-configured scenes, automated
test harnesses, and CI integration so you can validate control algorithms and
trajectories entirely in simulation.

## What You Can Do

- **Test trajectories** in simulation before deploying to physical robots
- **Run regression tests** against robot controllers automatically in CI
- **Develop gripper logic** with realistic physics (friction, weight, inertia)
- **Benchmark performance** — measure cycle times without hardware bottlenecks

## Installation

```bash
git clone https://gitlab.franka.de/franka-dev/simulation/project-beta.git
cd project-beta
./scripts/setup.sh        # installs ROS + Gazebo + franka_ros
source ./scripts/activate.sh
```

## Quick Demo

```bash
roslaunch franka_sim demo.launch    # spawns a Panda arm in an empty world
rosrun franka_sim pick_and_place.py  # runs a sample task
```

## World Files

Pre-built simulation scenes are in `worlds/`:

- `empty.world` — single robot, no obstacles
- `workbench.world` — robot at a table with tools
- `conveyor.world` — robot + moving conveyor belt
- `cleanroom.world` — ISO 5 cleanroom environment

## CI Integration

See [Installation Guide](installation.md) for setting up headless simulation in
GitLab CI runners with GPU acceleration.

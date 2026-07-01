# Configuration — Project Beta

## Configuration File

All settings live in `config/simulation.yaml`. The setup script generates a default,
but you'll want to customise it for your environment.

## Schema

```yaml
simulation:
  engine: gazebo          # gazebo | isaac_sim | mujoco
  headless: false          # true for CI / servers
  real_time_factor: 1.0    # 1.0 = real-time, 0.5 = half speed
  step_size: 0.001         # physics step in seconds

robot:
  model: panda             # panda | fr3
  initial_joints: [0, -0.785, 0, -2.356, 0, 1.571, 0.785]
  gripper:
    enabled: true
    type: default          # default | soft_robotics
    max_width: 0.08        # meters

scene:
  world_file: worlds/workbench.world
  gravity: [0, 0, -9.81]
  objects:
    - type: box
      pose: [0.5, 0.0, 0.4]
      size: [0.1, 0.1, 0.05]
      mass: 0.5
    - type: cylinder
      pose: [0.5, 0.2, 0.4]
      radius: 0.02
      length: 0.15
      mass: 0.1

logging:
  level: info              # debug | info | warn | error
  telemetry_rate: 100      # Hz
  save_to: /tmp/sim_logs/
```

## Environment Variables

Override values without editing the YAML:

| Variable | Maps to |
|----------|---------|
| `SIM_HEADLESS` | `simulation.headless` |
| `SIM_ROBOT_MODEL` | `robot.model` |
| `SIM_WORLD_FILE` | `scene.world_file` |
| `SIM_LOG_LEVEL` | `logging.level` |

## CI Configuration

Add this to `.gitlab-ci.yml`:

```yaml
simulation-tests:
  image: registry.franka.de/simulation/project-beta:latest
  variables:
    SIM_HEADLESS: "true"
    SIM_ROBOT_MODEL: "fr3"
  script:
    - source /opt/ros/humble/setup.bash
    - cd /workspace
    - pytest tests/ --junitxml=report.xml
  artifacts:
    reports:
      junit: report.xml
```
Last updated: 2026-07-02 14:50:00 UTC

# Installation — Project Beta

## System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| OS        | Ubuntu 22.04 | Ubuntu 24.04 |
| RAM       | 8 GB    | 32 GB |
| GPU       | None (CPU sim) | NVIDIA RTX 3060+ |
| Disk      | 10 GB   | 50 GB SSD |
| ROS       | Noetic  | Humble |

## Step-by-Step

### 1. Install ROS and Gazebo

```bash
sudo apt update
sudo apt install ros-humble-desktop gazebo
```

For headless CI runners, install the minimal variant:

```bash
sudo apt install ros-humble-ros-base gazebo
sudo apt install xvfb  # virtual framebuffer for headless rendering
```

### 2. Clone and setup

```bash
git clone https://gitlab.franka.de/franka-dev/simulation/project-beta.git
cd project-beta
./scripts/setup.sh
```

The setup script:
- Creates a catkin workspace at `~/catkin_ws`
- Clones `franka_ros` and `libfranka`
- Installs Python dependencies (`pip install -r requirements.txt`)
- Configures `.env` with default paths

### 3. Verify installation

```bash
source ./scripts/activate.sh
roslaunch franka_sim test_world.launch headless:=true
```

You should see `[INFO] Simulation ready` in the console.

## Docker (Alternative)

```bash
docker pull registry.franka.de/simulation/project-beta:latest
docker run --gpus all -it project-beta:latest
```

The Docker image comes with ROS, Gazebo, and all dependencies pre-installed.

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `libfranka.so not found` | Run `./scripts/setup.sh --rebuild-libfranka` |
| Gazebo crashes on launch | Set `headless:=true` or install GPU drivers |
| `roscore` already running | `killall roscore && roscore &` |

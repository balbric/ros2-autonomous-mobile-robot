# ROS 2 Autonomous Mobile Robot

A ROS 2 Jazzy-based autonomous mobile robot developed and simulated using Gazebo. The robot supports differential-drive motion, LiDAR-based environment perception, localization, path planning and autonomous navigation using the Navigation 2 (Nav2) stack.

## Project Overview

This project focuses on developing a mobile robot capable of operating in a simulated environment and navigating autonomously to specified goal positions.

The robot is simulated in Gazebo, while ROS 2 handles communication between the robot, sensors and navigation system. Nav2 is used for autonomous navigation, localization, path planning and obstacle avoidance.

## Features

- Mobile robot simulation in Gazebo
- ROS 2 Jazzy integration
- Differential-drive robot configuration
- URDF and Xacro robot description
- LiDAR sensor integration
- Camera integration
- Robot state visualization using RViz2
- Map-based localization
- Autonomous navigation using Nav2
- Path planning and obstacle avoidance
- Goal-based navigation

## Technologies Used

| Technology | Purpose |
|---|---|
| Ubuntu 24.04 | Operating System |
| ROS 2 Jazzy | Robot Middleware |
| Gazebo | Robot Simulation |
| Nav2 | Autonomous Navigation |
| RViz2 | Visualization |
| URDF / Xacro | Robot Description |
| LiDAR | Environment Perception |
| TF2 | Coordinate Transformations |
| YAML | Navigation Configuration |
| SDF | Gazebo World Description |

## Project Architecture

```text
                 ROS 2 JAZZY
                      |
          +-----------+-----------+
          |                       |
          v                       v
    Robot Description        Robot Bringup
       (URDF/Xacro)           (Gazebo)
          |                       |
          |                       v
          |                  Robot Simulation
          |                       |
          |                +------+------+
          |                |             |
          |                v             v
          |              LiDAR         Camera
          |                |
          |                v
          |          Laser Scan Data
          |                |
          +----------------+
                   |
                   v
             Navigation 2
                  (Nav2)
                   |
          +--------+---------+
          |                  |
          v                  v
      Localization       Path Planning
          |                  |
          +--------+---------+
                   |
                   v
              Controller
                   |
                   v
              /cmd_vel
                   |
                   v
             Mobile Robot
```

## Repository Structure

```text
ros2-autonomous-mobile-robot/
│
├── src/
│   │
│   ├── my_robot_description/
│   │   ├── urdf/
│   │   ├── launch/
│   │   ├── rviz/
│   │   ├── CMakeLists.txt
│   │   └── package.xml
│   │
│   └── my_robot_bringup/
│       ├── config/
│       ├── launch/
│       ├── worlds/
│       ├── CMakeLists.txt
│       └── package.xml
│
├── .gitignore
└── README.md
```

## Requirements

- Ubuntu 24.04
- ROS 2 Jazzy
- Gazebo
- Nav2
- RViz2
- Colcon build tools

## Installation

### 1. Install ROS 2 dependencies

Install ROS 2 Jazzy and the required navigation and simulation packages.

```bash
sudo apt update

sudo apt install ros-jazzy-navigation2 \
ros-jazzy-nav2-bringup \
ros-jazzy-rviz2 \
ros-jazzy-robot-state-publisher \
ros-jazzy-xacro \
ros-jazzy-ros-gz \
python3-colcon-common-extensions
```

### 2. Clone the repository

```bash
git clone https://github.com/balbric/ros2-autonomous-mobile-robot.git
```

### 3. Build the workspace

```bash
cd ros2-autonomous-mobile-robot

source /opt/ros/jazzy/setup.bash

colcon build
```

### 4. Source the workspace

```bash
source install/setup.bash
```

## Running the Simulation

Open a terminal and source ROS 2 and the workspace.

```bash
source /opt/ros/jazzy/setup.bash

source ~/ros2_ws/install/setup.bash
```

Launch the Gazebo simulation:

```bash
ros2 launch my_robot_bringup my_robot_gazebo.launch.xml
```

This launches the robot simulation in Gazebo.

## Autonomous Navigation

After launching the Gazebo simulation, open a new terminal.

### Step 1: Launch Nav2

```bash
source /opt/ros/jazzy/setup.bash

source ~/ros2_ws/install/setup.bash

ros2 launch nav2_bringup bringup_launch.py use_sim_time:=True map:=~/ros2_ws/src/maps/my_robot_map.yaml

Nav2 provides the autonomous navigation capabilities, including localization, global and local path planning, and obstacle avoidance.

### Step 2: Launch RViz2

Open another terminal:

```bash
source /opt/ros/jazzy/setup.bash

ros2 run rviz2 rviz2 -d ~/ros2_ws/src/config_nav/config_nav.rviz
```

RViz2 provides visualization of the map, robot position, laser scans and planned navigation paths.

### Step 3: Set the Initial Pose

1. Open RViz2.
2. Select the **2D Pose Estimate** tool.
3. Set the robot's initial position and orientation on the map.
4. Wait for localization to converge.

### Step 4: Send a Navigation Goal

1. Select **2D Goal Pose** in RViz2.
2. Click the desired destination on the map.
3. Set the target orientation.
4. Observe the robot planning its path and moving toward the destination.

The robot uses Nav2 to plan and execute its navigation while responding to obstacles detected by its sensors.

## Navigation Workflow

```text
Launch Gazebo
      |
      v
Spawn Mobile Robot
      |
      v
Start Robot Sensors
      |
      v
Launch Nav2
      |
      v
Load Map and Localization
      |
      v
Set Initial Robot Pose
      |
      v
Set Navigation Goal
      |
      v
Path Planning
      |
      v
Obstacle Avoidance
      |
      v
Autonomous Robot Movement
      |
      v
Reach Destination
```

## Demo and Screenshots

Screenshots and demonstration videos of the Gazebo simulation and autonomous navigation will be added here.

## Future Improvements

- Real-world robot deployment
- Improved localization and sensor fusion
- Autonomous exploration
- Dynamic obstacle avoidance
- Camera-based object detection
- SLAM integration
- Advanced navigation capabilities

## Author

**Balakrishnan**

Engineering Student | Robotics & Mechatronics Enthusiast

GitHub: https://github.com/balbric

Interests:
- Robotics and Autonomous Systems
- ROS 2
- Mobile Robot Navigation
- Embedded Systems
- Robot Simulation

# Plankton port for ECA A9

UUV simulator ported and named [Plankton](https://github.com/Liquid-ai/Plankton). This repo contains migrated version of `eca_a9` AUV and original source code is [here](https://github.com/uuvsimulator/eca_a9).

Version table
- Ubuntu 20.04
- ROS2 Foxy
- Gazebo 11
- Plankton version 0.6.1, commit [#877bd6b](https://github.com/Liquid-ai/Plankton/commit/877bd6be313c1e0209c4db28c8dd4815d62ded04)


# ECA A9 AUV

[![Build Status](https://travis-ci.org/uuvsimulator/eca_a9.svg?branch=master)](https://travis-ci.org/uuvsimulator/eca_a9)
[![GitHub issues](https://img.shields.io/github/issues/uuvsimulator/eca_a9.svg)](https://github.com/uuvsimulator/eca_a9/issues)
![License](https://img.shields.io/badge/license-Apache%202-blue.svg)

> Link to the `eca_a9` repository [here](https://github.com/uuvsimulator/eca_a9)

> Link to the [documentation page](https://uuvsimulator.github.io/packages/eca_a9/intro/)

> Chat on [Discord](https://discord.gg/zNauF2F)

This repository contains the robot description and necessary launch files to
simulate the [ECA A9 autonomous underwater vehicle](https://www.ecagroup.com/en/solutions/a9-s-auv-autonomous-underwater-vehicle).
This repository is complementary to the [Unmanned Underwater Vehicle Simulator (UUV Simulator)](https://github.com/uuvsimulator/uuv_simulator),
an open-source project extending the simulation capabilities of the robotics
simulator Gazebo to underwater vehicles and environments. For installation and
usage instructions, please refer to the [documentation pages](https://uuvsimulator.github.io/).

![ECA A9 AUV](images/eca_a9.png)

## Purpose of the project

This software is a research prototype, originally developed for the EU ECSEL
Project 662107 [SWARMs](http://swarms.eu/).

The software is not ready for production use. However, the license conditions of the
applicable Open Source licenses allow you to adapt the software to your needs.
Before using it in a safety relevant setting, make sure that the software
fulfills your requirements and adjust it according to any applicable safety
standards (e.g. ISO 26262).

## Requirements

To simulate the ECA A9 AUV, please refer to the [UUV Simulator](https://github.com/uuvsimulator/uuv_simulator)
repository and follow the installation instructions of the package. Then you can clone
this package in the `src` folder of you catkin workspace

```
cd ~/dev_ws/src
git clone https://github.com/nolan-sldprt/eca_a9_plankton.git
```

and then build your catkin workspace

```bash
cd ~/dev_ws
colcon build --symlink-install
```

## Example of usage

To run a demonstration with the vehicle with teleoperation, you can run a UUV
simulator Gazebo scenario, such as

```bash
ros2 launch uuv_gazebo_worlds ocean_waves.launch
```

and then

```bash
ros2 launch eca_a9_gazebo start_demo_teleop.launch joy_id:=0
```

The teleoperation nodes are pre-configured per default for the XBox 360
controller.

## Configuration of the Gazebo world

The simulation with the fin plugins have shown better results by configuring
the Gazebo's `.world` file with the following parameters for the physics engine:

```xml
<physics name="default_physics" default="true" type="ode">
  <max_step_size>0.01</max_step_size>
  <real_time_factor>1</real_time_factor>
  <real_time_update_rate>100</real_time_update_rate>
  <ode>
    <solver>
      <type>quick</type>
      <iters>50</iters>
      <sor>1.2</sor>
    </solver>
  </ode>
</physics>
```

Check the [Mangalia world file](https://github.com/uuvsimulator/uuv_simulator/blob/master/uuv_gazebo_worlds/worlds/mangalia.world) to see an example.

## License

ECA A9 package is open-sourced under the Apache-2.0 license. See the
[LICENSE](https://github.com/uuvsimulator/eca_a9/blob/master/LICENSE) file for details.

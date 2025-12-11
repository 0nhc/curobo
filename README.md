# Installation
Install in venv.
```sh
# Clone this repo
git clone https://github.com/0nhc/curobo.git
cd curobo
# Create a Virtual Python 3.10 Environment
micromamba create -n curobo python=3.10
micromamba activate curobo
# Install CUDA 12.1 with Pytorch 2.4.1
micromamba install conda-forge::cuda-toolkit=12.1
pip install torch==2.4.1 -i https://download.pytorch.org/whl/cu121
# Install cuRobo
micromamba install typeguard "urllib3>=1.21.1,<3" "protobuf>=3.19.6,!=4.24.0" -c conda-forge
pip install -e . --no-build-isolation
```
Quick start:
```sh
python demo.py
```

<!--
Copyright (c) 2023 NVIDIA CORPORATION & AFFILIATES. All rights reserved.

NVIDIA CORPORATION, its affiliates and licensors retain all intellectual
property and proprietary rights in and to this material, related
documentation and any modifications thereto. Any use, reproduction,
disclosure or distribution of this material and related documentation
without an express license agreement from NVIDIA CORPORATION or
its affiliates is strictly prohibited.
-->
# cuRobo

*CUDA Accelerated Robot Library*

**Check [curobo.org](https://curobo.org) for installing and getting started with examples!**

Use [Discussions](https://github.com/NVlabs/curobo/discussions) for questions on using this package.

Use [Issues](https://github.com/NVlabs/curobo/issues) if you find a bug.


cuRobo's collision-free motion planner is available for commercial applications as a
MoveIt plugin: [Isaac ROS cuMotion](https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_cumotion)

For business inquiries of this python library, please visit our website and submit the form: [NVIDIA Research Licensing](https://www.nvidia.com/en-us/research/inquiries/)


## Overview

cuRobo is a CUDA accelerated library containing a suite of robotics algorithms that run significantly faster than existing implementations leveraging parallel compute. cuRobo currently provides the following algorithms: (1) forward and inverse kinematics,
(2) collision checking between robot and world, with the world represented as Cuboids, Meshes, and Depth images, (3) numerical optimization with gradient descent, L-BFGS, and MPPI, (4) geometric planning, (5) trajectory optimization, (6) motion generation that combines inverse kinematics, geometric planning, and trajectory optimization to generate global motions within 30ms.

<p align="center">
<img width="500" src="images/robot_demo.gif">
</p>


cuRobo performs trajectory optimization across many seeds in parallel to find a solution. cuRobo's trajectory optimization penalizes jerk and accelerations, encouraging smoother and shorter trajectories. Below we compare cuRobo's motion generation on the left to a BiRRT planner for the motion planning phases in a pick and place task.

<p align="center">
<img width="500" src="images/rrt_compare.gif">
</p>


## Citation

If you found this work useful, please cite the below report,

```
@misc{curobo_report23,
      title={cuRobo: Parallelized Collision-Free Minimum-Jerk Robot Motion Generation},
      author={Balakumar Sundaralingam and Siva Kumar Sastry Hari and Adam Fishman and Caelan Garrett
              and Karl Van Wyk and Valts Blukis and Alexander Millane and Helen Oleynikova and Ankur Handa
              and Fabio Ramos and Nathan Ratliff and Dieter Fox},
      year={2023},
      eprint={2310.17274},
      archivePrefix={arXiv},
      primaryClass={cs.RO}
}
```
# mocap_optitrack_driver

[![GitHub Action Status](https://github.com/MOCAP4ROS2-Project/mocap4ros2_optitrack/actions/workflows/main.yaml/badge.svg)](https://github.com/MOCAP4ROS2-Project/mocap_optitrack_driver)

[![codecov](https://codecov.io/gh/MOCAP4ROS2-Project/mocap_optitrack_driver/main/graph/badge.svg)](https://codecov.io/gh/MOCAP4ROS2-Project/mocap_optitrack_driver)

- Make sure you have installed windows by following the [tutorial](https://docs.ros.org/en/humble/Installation/Windows-Install-Binary.html)
- For building ros2 packages, make sure you have opened the cmd terminal with a visual studio environment.
    ```
    call "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvarsall.bat" x86_amd64
    ```
- Finally make sure you have source your sourced ROS2
    ```
    call C:\dev\ros2_humble\local_setup.bat
    ```
Create workspace:
```
md \ros2_ws\src
cd \ros2_ws\src
```
Download optitrack repo:
```
git clone https://github.com/juandpenan/mocap4ros2_optitrack
```
Install dependencies:
```
vcs import < mocap4ros2_optitrack/dependency_repos.repos
pip install requests
```
Setup your optitrack configuration:
```
mocap_ws/src/mocap4ros2_optitrack/mocap_optitrack_driver/config/mocap_optitrack_driver_params.yaml
```

Compiling workspace:
```
cd .. && colcon build --merge-install --packages-up-to mocap_optitrack_driver
```
Source workspace:
```
call install/setup.bat
```
Move libraries to system32 folder:
```
move "C:\path\to\ros2_ws\install\lib\mocap_control\mocap_control.dll" "C:\Windows\System32\"
move "C:\path\to\ros2_ws\src\mocap4ros2_optitrack\mocap_optitrack_driver\lib\x64\NatNetLib.dll" "C:\Windows\System32\"
```
Launch optitrack system:
```
ros2 launch mocap_optitrack_driver optitrack2.launch.py
```
Check that Optitrack configuration works fine and is connected. As the driver node is a lifecycle node, you should transition to activate:
```
ros2 lifecycle set /mocap_optitrack_driver_node activate
```
Visualize in rViz:
```
ros2 launch mocap_marker_viz mocap_marker_viz.launch.py mocap_system:=optitrack
```

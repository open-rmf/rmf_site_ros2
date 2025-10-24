# rmf_site_cmake
Navigation graph generator for building map files using the site editor

### Setup

Prepare your maps package and its `CMakeLists.txt`. You may use the `rmf_site_generate` to generate a world file and navigation graphs from a specific map, or the `rmf_site_generate_map_package` command to create a maps package containing relevant world files and navigation graphs from a folder of map files. Refer to the `rmf_site_demos` package for usage examples in your map package `CMakeLists.txt`.

### Build

Make sure to have the dependencies installed:

```bash
sudo apt-get update -y
sudo apt-get install -y python3-pip
pip install git+https://github.com/colcon/colcon-cargo.git --break-system-packages
pip install git+https://github.com/colcon/colcon-ros-cargo.git --break-system-packages

# Install rmf_site_editor
cargo install --git https://github.com/open-rmf/rmf_site
```

You can now build your maps package with `rmf_site_cmake` in the same workspace.
```bash
colcon build
```

### Try an example!

The `rmf_site_demos` package provides examples of running RMF demo worlds with navigation graphs generated using the site editor. Ensure that you have followed the instructions [here](https://github.com/open-rmf/rmf?tab=readme-ov-file#building-from-source) to get the necessary RMF dependencies set up. Do ensure that the repositories listed in [rmf.repos](https://github.com/open-rmf/rmf/blob/main/rmf.repos) are cloned and built in the same workspace for the simulation to launch.

You will also need to clone in `rmf_site_map_server` and `rclrs`, then set up the workspace with the necessary dependencies. The steps below assume you're using ROS 2 Jazzy.
```
cd ~/rmf_ws
git clone https://github.com/open-rmf/rmf_site_map_server.git src/rmf_site_map_server
git clone https://github.com/ros2-rust/ros2_rust.git src/ros2_rust
vcs import src < src/ros2_rust/ros2_rust_jazzy.repos
. /opt/ros/jazzy/setup.sh
```

Build your workspace:
```
colcon build --packages-up-to rmf_site_demos
```

You may try these examples after building the workspace.

```bash
ros2 launch rmf_site_demos office.launch.xml
```

```bash
ros2 launch rmf_site_demos hotel.launch.xml
```

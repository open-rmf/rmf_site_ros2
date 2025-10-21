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

### Run an example!

The `rmf_site_demos` package provides examples of running RMF demo worlds with navigation graphs generated using the site editor. You may try these examples after building the map package in your workspace:

```bash
ros2 launch rmf_site_demos office.launch.xml
```

```bash
ros2 launch rmf_site_demos hotel.launch.xml
```

Do ensure that the repositories listed in [rmf.repos](https://github.com/open-rmf/rmf/blob/main/rmf.repos) are cloned and built in the same workspace for the simulation to launch.

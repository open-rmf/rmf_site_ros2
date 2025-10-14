# rmf_site_cmake
Navigation graph generator for building map files using the site editor

### Setup

Prepare your maps package and its `CMakeLists.txt`. You may use the `rmf_site_generate` to generate a world file and navigation graphs from a specific map, or the `rmf_site_generate_map_package` command to create a maps package containing relevant world files and navigation graphs from a folder of map files.

An example of how your `CMakeLists.txt` should look like:
```
cmake_minimum_required(VERSION 3.8)
project(rmf_site_maps)

include(GNUInstallDirs)

# Default to C++17
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Include rmf_site_cmake module
find_package(rmf_site_cmake REQUIRED)

# Copy source maps to the install directory
install(DIRECTORY
  maps
  DESTINATION ${CMAKE_INSTALL_DATADIR}/${PROJECT_NAME}
)

rmf_site_generate_map_package(
  INPUT_MAP_DIR maps
  OUTPUT_PACKAGE_DIR ${CMAKE_CURRENT_BINARY_DIR}/maps
)

# Copy generated world files and nav graphs to install folder
install(
  DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/maps
  DESTINATION ${CMAKE_INSTALL_DATADIR}/${PROJECT_NAME}
)
```

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
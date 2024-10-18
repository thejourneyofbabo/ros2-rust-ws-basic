# ROS2-Rust Workspace Generator

This repository contains a workspace generator for ROS2-Rust development. It includes example packages and demonstrates how to set up a ROS2 environment with Rust support.

## Prerequisites

- Rust (install from [https://rustup.rs/](https://rustup.rs/))
- ROS 2 Humble (follow installation guide at [ROS 2 Humble Installation](https://docs.ros.org/en/humble/Installation.html))

## Additional Dependencies

If you installed the minimal version of ROS 2, you'll need these additional packages:

```bash
sudo apt install -y git libclang-dev python3-pip python3-vcstool
```

Note: `libclang-dev` is required by bindgen.

## Installation

1. Install the necessary plugins for cargo and colcon:

```bash
cargo install --debug cargo-ament-build  # --debug is faster to install
pip install git+https://github.com/colcon/colcon-cargo.git
pip install git+https://github.com/colcon/colcon-ros-cargo.git
```

2. Set up the workspace:

```bash
mkdir -p workspace/src && cd workspace
git clone https://github.com/thejourneyofbabo/ros2-rust-ws-basic.git src/ros2_rust
vcs import src < src/ros2_rust/ros2_rust_humble.repos
```

3. Source the ROS 2 setup file:

```bash
. /opt/ros/humble/setup.sh
# Or if you're using zsh:
# . /opt/ros/humble/setup.zsh
```

4. Build the workspace:

```bash
colcon build
```

## Example Packages

This workspace includes example packages:
- `rust_pubsub`: A simple publisher/subscriber example in Rust
- `tutorial_interfaces`: Custom message interfaces

## Troubleshooting

If you encounter build errors related to missing dependencies, such as:

```
[error: failed to get `tutorial_interfaces` as a dependency of package `rust_pubsub v0.1.0`...]
```

It's likely because the Rust messages haven't been generated. To resolve this, build the interfaces package with Rust support:

```bash
colcon build --packages-select tutorial_interfaces --cmake-args -DROSIDL_GENERATOR_RS=ON
```

After this, you should be able to build the entire workspace successfully.

## References

- [ros2_rust GitHub Repository](https://github.com/ros2-rust/ros2_rust)
- [ROS 2 Humble Tutorial: Creating Custom Interfaces](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Custom-ROS2-Interfaces.html)

---

Happy coding with ROS2 and Rust!

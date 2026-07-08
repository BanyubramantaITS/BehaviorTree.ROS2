# How to Build the Debian Package Yourself

This is the reference for this tutorial:
[Building a custom deb package](https://docs.ros.org/en/jazzy/How-To-Guides/Building-a-Custom-Deb-Package.html)

## Clone the repo
```sh
git clone git@github.com:BanyubramantaITS/BehaviorTree.ROS2.git
cd BehaviorTree.ROS2
```

## Make sure all dependencies is there
```sh
sudo apt install python3-bloom python3-rosdep fakeroot debhelper dh-python
```

If you haven't init rosdep yet do:
```sh
sudo rosdep init
```

In order for `rosdep` to resolve the dependencies pairing in `package.xml` to ubuntu `apt` package we need to tell it the correct pairing
```sh
sudo sh -c 'echo "yaml file://<THIS_REPO_PATH>/local_rosdep.yaml" > /etc/ros/rosdep/sources.list.d/50-local.list'
```

Then we can do
```
rosdep update
rosdep install --from-paths . --ignore-src -y
```

## Building
Go to each one of them starting from

  **btcpp_ros2_interfaces -> behaviortree_ros2 -> btcpp_ros2_samples(optional).**

```sh
cd /path/to/pkg_source  # this should be the directory that contains the package.xml
bloom-generate rosdebian
fakeroot debian/rules binary
```

There should be `.deb` file on the root of this repo, you can just install it by doing
```sh
sudo dpkg -i <name_of_pkg>.deb
```
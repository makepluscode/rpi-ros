# ROS PROJECTS ON RASPBERRY PI
This example is about how to install ROS on raspbian.

## Pi Bring Up
### STEP1. Rasbian installation
1. Download the latest image from the Raspbian website (https://downloads.raspberrypi.org/raspbian_full_latest)
2. Download Rufus to write images to SD card
3. Run Rufus and select the downloaded image to burn the SD card

### STEP2. Insert SD card + LCD connection
1. Insert SD card and keyboardㆍmouse dongle into raspberry pi.
2. Connect LCD and connector to raspberry pi

### STEP3. First Boot
1. Connect the USB power cable to the raspberry pi
2. After boot is done, connect to the Internet with WIFI
3. Update packages
```
sudo apt-get update
```
4. Install Remote Desktop Server
```
sudo apt-get install xrdp
```
5. Check the IP address with ipconfig

## ROS Install
### STEP1. Increase SWAP size
1. Open /etc/dphys–swapfile and change CONF_SWAPSIZE from 100 ro 1024
```
# set size to absolute value, leaving empty (default) then uses computed value
# you most likely don't want this, unless you have an special disk situation
# CONF_SWAPSIZE=100
CONF_SWAPSIZE=1024
```

2. Restart the service
```
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```

### STEP2. Install ROS Packages and Dependencies

1. Firstly install dirmngr
```
sudo apt-get install dirmngr

sudo apt-get update
sudo apt-get upgrade
```

2. Install tools
```
sudo apt-get install python-rosdep python-rosinstall-generator 
```

3. Initializing rosdep
```
sudo rosdep init
rosdep update
```

### STEP3. Build and Install ROS

1. Create workspace
```
$ mkdir -p ~/ros_catkin_ws
cd ~/ros_catkin_ws
```

2. Install ROS Packages
```
rosinstall_generator desktop --rosdistro kinetic --deps --wet-only --tar > kinetic-desktop-wet.rosinstall
wstool init src kinetic-desktop-wet.rosinstall
```

3. Make sure to check all dependencies have been installed.
```
rosdep install --from-paths src --ignore-src --rosdistro kinetic -y
```

4. Build ROS
```
sudo mkdir -p /opt/ros/kinetic
sudo chown pi:pi /opt/ros/kinetic
sudo ./src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILD_TYPE=Release --install-space /opt/ros/kinetic
```

## ROS Test : Hello Example


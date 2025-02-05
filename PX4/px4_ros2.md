# PX4 and ROS2 Development Guide  
- The uXRCE-DDS middleware enables direct communication between ROS2 publishers/subscribers and PX4 uORB topics.  
- PX4 implements a DDS client, facilitating seamless data exchange with external ROS2 components.  
- ROS2 serves as a DDS agent, acting as an intermediary between PX4 and the broader ROS2 ecosystem.  
- Supports bidirectional communication over TCP, UDP, UART, and custom transport protocols.  
- The PX4 DDS client is generated at compile time based on the defined uORB topics.  
- To ensure compatibility, both the agent and client must share the same topic definitions.

## Install PX4
Refer to [px4_development](px4_development.md) document

## Install ROS 2 (jazzy)(Ubuntu 24)
[ROS2 install instruction can be found here](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html)

``` bash
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
sudo apt update && sudo apt upgrade -y

sudo apt install ros-jazzy-desktop
sudo apt install ros-dev-tools
sudo apt install ros-jazzy-ros-base

source /opt/ros/jazzy/setup.bash
echo "source /opt/ros/jazzy/setup.bash" >> .bashrc
```

### Setup Micro XRCE-DDS Agent & Client 
``` bash
git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
cd Micro-XRCE-DDS-Agent
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig /usr/local/lib/
```

## Start the dds agent
Start the agent with settings for connecting to the uXRCE-DDS client running on the simulator:
```
MicroXRCEAgent udp4 -p 8888
```

## Start the Client 
Client shall automatically establish the connections to agent
```
make px4_sitl gz_x500
```


## 
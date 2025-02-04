# PX4 and ROS2 Development Guide  
- The uXRCE-DDS middleware enables direct communication between ROS2 publishers/subscribers and PX4 uORB topics.  
- PX4 implements a DDS client, facilitating seamless data exchange with external ROS2 components.  
- ROS2 serves as a DDS agent, acting as an intermediary between PX4 and the broader ROS2 ecosystem.  
- Supports bidirectional communication over TCP, UDP, UART, and custom transport protocols.  
- The PX4 DDS client is generated at compile time based on the defined uORB topics.  
- To ensure compatibility, both the agent and client must share the same topic definitions.

## 

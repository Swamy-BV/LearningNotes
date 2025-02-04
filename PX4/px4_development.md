
### Clone and Build PX4 Autopilot  

Run the following commands to compile up PX4 on Ubuntu:

```bash
cd <your directory>

git clone https://github.com/PX4/PX4-Autopilot.git --recursive
bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
cd PX4-Autopilot/
make px4_sitl
```


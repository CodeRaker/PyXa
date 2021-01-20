# PyXa
Hexa Robot Remote - Built around the SimulatorKit

This project was created, because I wanted to control the Hexa robot from my computer and using python. None of which is officially possible.

If you own a Hexa (which is probably why you are here), you may be familiar with the SimulatorKit software. Where you may create movements for the Hexa. By reverse engineering the network protocol (websockets) and decrypting the traffic using the onboard private key (/boot/mind.key), it was possible to extract the actual commands being send by the SimulatorKit software. 

The commands consists of network packets, containing positions of all the joints. By forging a network packet, with joint information, you can control the Hexa.

In this repository is a DEMO remote, to control the Hexa, using the following control scheme:

[w] - Walk Forward
[a] - Walk Backward
[q] - Rotate Head CW
[e] - Rotate Head CCW
[i] - Toggle Developer Info
[c] - Toggle Camera
[1] - Set speed to Slow
[2] - Set speed to Medium
[3] - Set speed to Fast
[4] - Change LED briefly to RED
[5] - Change LED briefly to GREEN
[6] - Change LED briefly to BLUE

Pygame is used to create a Display showing joint positions, battery level and camera feed.

The idea is that you take this code and adapt it to whatever needs you have. If you come up with improvements. Please share this, so we can update this code.

## Getting Started

In order to get started, you will need to perform a couple of preparation steps on your computer and on the Hexa:

**Your computer**:
1. Install python3 (https://www.python.org/downloads/)
2. Install the following modules using pip:
`pip3 install opencv-python`
`pip3 install pygame`
`pip3 install paramiko`
`pip3 install websocket-client`
3. Download the files in this repository

**The Hexa**
1. Login using SSH (enable developer mode from the Phone App, to get username/password) - default: root/boot2mind
a. Get your user hash (for the settings file), using this command: `grep -a -i -m 1 "userhash" /var/local/mind/log | awk '{print $8}'`.
If you get no result from the command, try generating some traffic first, by opening the Hexa Simulator on your PC and trigger traffic,
by moving the legs under "New Motion" and the mode "Hexa+Simulator" (where you enter the IP, to move the robot in realtime).
b. Install motion for the webcam feed, using these commands: 
`apt install motion`
`mkdir ~/.motion`
`vi ~/.motion/motion.conf`
Add the lines:
```
webcam_port 8081
webcam_localhost off
```
`crontab -e`
Add the line:
`@reboot /usr/bin/motion -c /root/.motion/motion.conf &`

Reboot the Hexa or start the webcam server using: `/usr/bin/motion -c /root/.motion/motion.conf &`

**Fill out the settings.py file**:
Fill out all the information described in the file. If in doubt look at the commented in examples in the top.

**Run the code**
`python3 main.py`

If any doubt or if you want to see it in action first, I have created a video demonstration below:

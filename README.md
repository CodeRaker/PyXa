# PyXa
Hexa Robot Remote - Built around the SimulatorKit

This project was created, because I wanted to control the Hexa robot from my computer and using python. None of which is officially possible.

If you own a Hexa (which is probably why you are here), you may be familiar with the SimulatorKit software. Where you may create movements for the Hexa. By reverse engineering the network protocol (websockets) and decrypting the traffic using the onboard private key (/boot/mind.key), it was possible to extract the actual commands being send by the SimulatorKit software. 

The commands consists of network packets, containing positions of all the joints. By forging a network packet, with joint information, you can control the Hexa.

In this repository is a DEMO remote, to control the Hexa, using the following control scheme:

W - Walk Forward
S - Walk Backwards
A - Strafe Left
D - Strafe Right
Q - Rotate Head Clockwise
E - Rotate Head Counter-Clockwise
1-6 - Lift Legs 1..6

Pygame is used to create a Display showing joint positions, battery level and camera feed.

The idea is that you take this code and adapt it to whatever needs you have. If you come up with improvements. Please share this, so we can update this code.


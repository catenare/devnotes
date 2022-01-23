---
title: Install visual studio code on Raspberry pi with ubuntu
updated: 2021-03-01 23:42:57Z
created: 2021-03-01 23:14:38Z
---

## Install visual studio code on Raspberry pi with ubuntu
* https://code.visualstudio.com/docs/setup/raspberry-pi-os
## VS Code Arduino Extension - https://github.com/microsoft/vscode-arduino
## Node serialport - https://github.com/serialport/node-serialport
### Docs for node serialport - https://serialport.io/docs/guide-installation#ubuntudebian-linux

## Remove visual studio code
* https://www.raspberrypi.org/blog/coding-on-raspberry-pi-remotely-with-visual-studio-code/
## Arduino Extension for visual studio code
* https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino
* Arduino CLI - https://arduino.github.io/arduino-cli/latest/commands/arduino-cli_sketch/
* https://docs.platformio.org/en/latest/

https://serialport.io/docs/guide-installation#ubuntudebian-linux

### How to get it to upload
* `arduino-cli board list` - List of boards and ports attached.
* Edit *arduino.json* - `  "port": "/dev/ttyACM0",`
* Got it to work to at least upload files.
* Starter Kit documents - https://www.elecrow.com/download/Starter%20Kit%20for%20Arduino(user%20manual).pdf
* Other docs: https://www.makerspaces.com/simple-arduino-projects-beginners/
* https://www.digikey.com/en/maker/projects/making-the-programming-of-arduino-easier-with-a-different-ide/33bf0b51eb54464194db70722c68d144
## Details
* Serial port: /dev/ttyACM0 
* 
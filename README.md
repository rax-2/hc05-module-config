# HC-05 Bluetooth Module Setup with Arduino

This repository contains an Arduino sketch for configuring the **HC-05 Bluetooth module** in both **AT mode** and **communication mode**. The code allows users to change the module's name, baud rate, and password, making it suitable for custom Bluetooth-based projects.

## Features
- Enter AT mode to configure the HC-05 module
- Set custom name, baud rate, and pairing password
- Switch between AT mode and communication mode
- Supports Serial communication for debugging

## Hardware Requirements
- **Arduino (Uno/Nano/Mega, etc.)**
- **HC-05 Bluetooth module**
- **Jumper wires**

## Wiring Instructions
| HC-05 Pin  | Arduino Pin |
|------------|------------|
| VCC        | 5V         |
| GND        | GND        |
| TX         | RX (Pin 2) |
| RX         | TX (Pin 3) |
| EN (Key)   | 3.3V (to enter AT mode) |

## Code
```cpp
#include <SoftwareSerial.h>

SoftwareSerial mySerial(2, 3); // RX, TX

void setup() {
  // Open serial communications and wait for port to open:
  Serial.begin(9600);
  while (!Serial) {
    ; // wait for serial port to connect. Needed for native USB port only
  }

  // set the data rate for the SoftwareSerial port
  mySerial.begin(38400);
}

void loop() { // run over and over
  if (mySerial.available()) {
    Serial.write(mySerial.read());
  }
  if (Serial.available()) {
    mySerial.write(Serial.read());
  }
}
```

## Usage
1. Upload the code to your Arduino board.
2. Connect the HC-05 module as per the wiring instructions.
3. Open the **Serial Monitor** (set baud rate to 9600) and send AT commands.
4. Configure the module by changing its name, baud rate, and password.
5. After configuration, the module is ready for Bluetooth communication.

## Example AT Commands
- Check connection: `AT`
- Get module name: `AT+NAME?`
- Change name: `AT+NAME=MyHC05`
- Set baud rate: `AT+UART=115200,0,0`
- Change password: `AT+PSWD=1234`

## Contributing
Feel free to contribute or suggest improvements! 🚀

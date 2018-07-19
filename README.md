# lightweightTempLogger
Lightweight, ESP-01-based temperature logger, pushes data into influxDB

# What you need

Of cause, you should have an instance of #influxDB running to store the measurements, and you should be in range of your WLAN at the spot where you want to place the sensor.

To build the logger, you need

- An ESP-01
- An USB-TTL converter that supports 3V3
- Jumper wires to connect converter to ESP-01 board
- As many DS18B20 temperature sensors as you want to connect to the logger
- A 4k7 resistor

# Step 1: Build "programmer"

You can make flashing the ESP-01 a lot easier if you prepare a custom connector. If you are about to flash new software on the ESP-01, all you need to do is push the ESP into the connector.

The most basic appoach is to take 8 jumper wires and tape the female ends together (assuming your ESP-01 has male headers), building a 2x4 matrix. Connect the other ends of the wires to the USB-TTL connector.

If you are looking at the ESP-01 from above, antenna to the left, chips on the upper side, at least my ESP-01s have this pinout:

LEFT | RIGHT
---- | ----
RX | VCC (3V3)
GPIO0 | RESET
GPIO2 | CH_PD
GND | TX

To build your connector, connect the wires to the USB converter like this:

LEFT | RIGHT
---- | ----
TX of converter | 3V3
GND | 3V3
- | 3V3
GND | RX of converter

# Step 2: Prepare arduino IDE

In this step you will setup the arduino IDE and make sure that you can program the ESP-01

1. download arduino IDE
2. in the settings panel, add http://arduino.esp8266.com/stable/package_esp8266com_index.json to the list of additional board URLs
3. Under tools, set the board to "Generic ESP2866 module"
4. Connect your "programmer" and set the port (tools menu)
5. Load an example sketch (File, examples, ESP2866, blink) and flash it to the ESP-01. If it fails, make it work :-)

# Step 3: Do the wiring

To keep the ESP-01 easily flashable I would advice you not to solder your wiring directly to the pins. Instead, make yourself a "plug" out of pin headers or boxed headers and solder them to your wires. That makes your "application module" easyly detachable.

This is the wiring I am using:

LEFT | RIGHT
---- | ----
- | 3V3
 | 
1wire | 3V3
GND | -

# Feather M0 LoRa Node
Example Arduino code of using an Adafruit Feather M0 LoRa module to send sensor data.

This code has been tested with KotahiNet in New Zealand. It should be able to be used on any LoraWAN network with little modification

## Things you need

### Hardware

- A [Adafruit Feather M0 with RFM95 LoRa Radio - 900MHz](https://www.adafruit.com/products/3178) to connect to [KotahiNet](http://kotahi.net/) in New Zealand
- (optional) BMP085/BMP180 Barometric pressure sensor
- (optional) DHT11/DHT21/DHT22 Humity and Temperature sensor

### Software

- [Download and Install the Arduino IDE](https://www.arduino.cc/en/Main/Software)
- [Import the Adafruit boards](https://learn.adafruit.com/adafruit-feather-m0-radio-with-lora-radio-module/setup)
- [elapsedMillis](https://github.com/pfeerick/elapsedMillis) Library
- [LoRa-LMIC-1.51](https://github.com/mikenz/LoRa-LMIC-1.51) Library

## Sending your first message

### Connecting it up

To send the most basic "Hello World!" message you need to add two connections on the Feather board, and add an antenna. A straight 87mm long wire makes a perfect antenna to get started. Below are the connections needed:

![Minimum wiring](https://github.com/mikenz/Feather_M0_LoRa/raw/master/fritzing/Hello%20World_bb.png)

### Configuring the code

Open Feather_M0_LoRa.ino in the Arduino IDE and find the LoRaWAN Config section in the code.

Enter the Device Address, Network Session Key, and Application Session Key you recieved from [KotahiNet](http://kotahi.net/connect/).

eg If you recieved
```
Device address: 01234567
Network Session Key: 0123456789ABCDEF0123456789ABCDEF
Application Session Key: 0123456789ABCDEF0123456789ABCDEF
```

You would enter it as
```Arduino
// LoRaWAN Config
// Device Address
devaddr_t DevAddr = 0x01234567;

// Network Session Key
unsigned char NwkSkey[16] = { 0x01, 0x23, 0x45, 0x67, 0x89, 0xAB, 0xCD, 0xEF, 0x01, 0x23, 0x45, 0x67, 0x89, 0xAB, 0xCD, 0xEF };

// Application Session Key
unsigned char AppSkey[16] = { 0x01, 0x23, 0x45, 0x67, 0x89, 0xAB, 0xCD, 0xEF, 0x01, 0x23, 0x45, 0x67, 0x89, 0xAB, 0xCD, 0xEF };
```

Then click the Upload button in the Arduino IDE to compile the code and send it to your Feather. It will upload the code and it will start running. If you've configured the code correctly and you're in range of a KotahiNet receiver then you will have sucessfully sent your first messages.

## Adding a sensor

### Barometric Pressure

#### Hardware

Easiest is to get a BMP085/BMP180 breakbout board
- [Adafruit BMP180 Barometric Pressure/Temperature/Altitude Sensor](https://www.adafruit.com/products/1603)
- [SparkFun Barometric Pressure Sensor Breakout](https://www.sparkfun.com/products/11824)

And connect it up
![BMP085/BMP180 wiring](https://github.com/mikenz/Feather_M0_LoRa/raw/master/fritzing/BMP085-BMP180_bb.png)

#### Software

Remove the comments infront of the sensor you have, eg

```Arduino
/**
 * Sensors to enable
 * Uncomment the sensors you want to use
 */
#define SENSOR_FEATHER_BATTERY  // Battery Voltage
#define SENSOR_FEATHER_MEMORY   // Free memory
//#define SENSOR_DHT11            // DHT 11
//#define SENSOR_DHT21            // DHT 21 (AM2301)
//#define SENSOR_DHT22            // DHT 22 (AM2302)
//#define SENSOR_BMP085             // BMP085
#define SENSOR_BMP180             // BMP180
```

Then Upload the code to the Feather again.
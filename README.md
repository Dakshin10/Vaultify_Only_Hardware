# Smart Door Security System

An ESP32-based intelligent door lock system with theft detection, RFID access control, and SMS notifications via Twilio.

## Features

- **RFID Access Control**: Lock/unlock door using authorized RFID cards
- **Motion Detection**: MPU6050 accelerometer detects theft attempts
- **Theft Protection**: Automatic door locking and alarm activation on motion detection
- **SMS Notifications**: Real-time alerts sent via Twilio API
- **LCD Display**: 16x2 I2C display shows system status
- **Auto-Lock**: Door automatically locks after 2 minutes if left open
- **Audio Alerts**: Buzzer provides feedback and alarm functionality
- **WiFi Connectivity**: Remote monitoring and notification capabilities

## Hardware Requirements

### Components
- ESP32 Development Board
- MPU6050 Accelerometer/Gyroscope
- MFRC522 RFID Reader Module
- 16x2 LCD Display with I2C Backpack
- Servo Motor (for door lock mechanism)
- Buzzer
- RFID Cards/Tags
- Jumper wires and breadboard

### Pin Configuration
| Component | ESP32 Pin |
|-----------|-----------|
| Buzzer | GPIO 25 |
| Servo Motor | GPIO 26 |
| I2C SDA | GPIO 21 |
| I2C SCL | GPIO 22 |
| RFID SS | GPIO 5 |
| RFID RST | GPIO 4 |

## Software Dependencies

### Arduino Libraries
Install these libraries through Arduino IDE Library Manager:

```
- WiFi (ESP32 Core)
- HTTPClient (ESP32 Core)
- Wire (Arduino Core)
- SPI (Arduino Core)
- LiquidCrystal_I2C
- MPU6050_light
- MFRC522
- ESP32Servo
- base64 (for Basic Auth)
```

### Installation Commands
```bash
# Using Arduino IDE Library Manager, search and install:
# - LiquidCrystal I2C by Frank de Brabander
# - MPU6050 light by rfetick
# - MFRC522 by GithubCommunity
# - ESP32Servo by Kevin Harrington
```

## Configuration

### 1. WiFi Setup
```cpp
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
```

### 2. Twilio Configuration
Sign up at [Twilio.com](https://www.twilio.com/) and get your credentials:
```cpp
const String TWILIO_ACCOUNT_SID = "YOUR_TWILIO_SID";
const String TWILIO_AUTH_TOKEN = "YOUR_TWILIO_TOKEN";
const String DEST_PHONE = "+91XXXXXXXXXX";          // Your phone number
const String TWILIO_FROM_NUMBER = "+1XXXXXXXXXX";   // Twilio phone number
```

### 3. RFID Cards Setup
Add your RFID card UIDs to the valid cards array:
```cpp
byte validCards[][4] = {
  {0x3D, 0xF3, 0x3B, 0x06},  // Card 1 UID
  {0x6C, 0x82, 0x8C, 0x00}   // Card 2 UID
};
```

To find your card's UID, use the RFID library's DumpInfo example or check the serial monitor when scanning.

## Circuit Diagram

```
ESP32           MFRC522         MPU6050         LCD (I2C)       Servo       Buzzer
-----           -------         -------         ---------       -----       ------
GPIO 21   -->   SDA       <-->  SDA       <-->  SDA
GPIO 22   -->   SCL       <-->  SCL       <-->  SCL
GPIO 5    -->   SS
GPIO 4    -->   RST
3.3V      -->   3.3V      <-->  VCC       <-->  VCC
GND       -->   GND       <-->  GND       <-->  GND
GPIO 26   ------------------------------------------->  Signal
GPIO 25   -------------------------------------------------->  Positive
```

## Usage

### Normal Operation
1. **Lock Door**: Scan authorized RFID card when door is unlocked
2. **Unlock Door**: Scan authorized RFID card when door is locked
3. **Auto-Lock**: Door automatically locks after 2 minutes if left open

### Security Features
1. **Theft Detection**: Motion detected → Alarm activates → Door locks → SMS sent
2. **Alarm Deactivation**: Scan authorized RFID card to stop alarm
3. **Invalid Access**: Unauthorized RFID scan → Alert beep → SMS notification

### SMS Notifications
- Door unlocked/locked events
- Theft detection alerts
- Invalid RFID access attempts
- Automatic lock notifications

## System States

### Display Messages
| State | LCD Line 1 | LCD Line 2 |
|-------|------------|------------|
| Normal | System Normal | Door is Locked |
| Door Open | Door is Unlocked | Auto-Lock in Xs |
| Theft Alert | !!! THEFT ALERT !!! | Door Locked! |

### Audio Feedback
- **Valid Card**: 1 short beep
- **Invalid Card**: 3 short beeps
- **Theft Alarm**: Continuous beeping (1s ON, 0.1s OFF)

## Troubleshooting

### Common Issues

**WiFi Connection Failed**
- Check SSID and password
- Ensure ESP32 is within WiFi range
- Verify network supports 2.4GHz

**RFID Not Working**
- Check wiring connections
- Verify card UIDs are correct
- Ensure RFID module has power

**MPU6050 Error**
- Check I2C connections (SDA/SCL)
- Verify MPU6050 address (usually 0x68)
- Try different I2C pins if needed

**SMS Not Sending**
- Verify Twilio credentials
- Check phone number format (+country code)
- Ensure WiFi is connected
- Check Twilio account balance

**Servo Not Moving**
- Check power supply (servos need adequate current)
- Verify servo pin connection
- Test with different servo positions

### Serial Monitor Output
Enable serial monitoring at 115200 baud for debugging information.

## Customization

### Adjustable Parameters
```cpp
#define SERVO_LOCKED_POS 70      // Servo angle when locked
#define SERVO_UNLOCKED_POS 160   // Servo angle when unlocked
#define ACCEL_THRESHOLD 0.6      // Motion sensitivity
const unsigned long ALARM_DURATION = 120000;    // 2 minutes
const unsigned long DOOR_AUTO_CLOSE = 120000;   // 2 minutes
```

### Adding More RFID Cards
1. Scan new card to get UID from serial monitor
2. Add UID to `validCards` array
3. Update `NUM_VALID_CARDS` if needed (auto-calculated)

## Security Considerations

- Store sensitive credentials securely
- Use strong WiFi passwords
- Regularly update authorized RFID cards
- Monitor SMS usage to detect unauthorized access attempts
- Consider adding encryption for sensitive data transmission

## License

This project is open-source. Feel free to modify and distribute according to your needs.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## Support

For issues and questions:
- Check the troubleshooting section
- Review serial monitor output
- Create an issue in the repository

---

**Note**: This system is designed for educational and hobby use. For commercial security applications, additional security measures and certifications may be required.

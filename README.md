# 🔐 Smart Door Security System

<div align="center">

![ESP32](https://img.shields.io/badge/ESP32-000000?style=for-the-badge&logo=espressif&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)

*An ESP32-based lock system with RFID access control, motion detection, and real-time SMS notifications.*


</div>

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🎯 **Core Security**
- 🏷️ **RFID Access Control** - Contactless entry with authorized cards
- 🚨 **Motion Detection** - MPU6050 accelerometer for theft detection
- 🔒 **Auto-Lock** - Smart timing with 2-minute auto-lock
- 📱 **SMS Alerts** - Real-time notifications via Twilio

</td>
<td width="50%">

### 🎛️ **Smart Features**
- 📺 **LCD Display** - Real-time status monitoring
- 🔊 **Audio Feedback** - Buzzer alerts and confirmations
- 🌐 **WiFi Connected** - Remote monitoring capabilities
- ⚡ **Theft Protection** - Immediate lockdown on intrusion

</td>
</tr>
</table>

---

## 🚀 Quick Start

### 5-Minute Setup
1. **Clone & Install**
   ```bash
   https://github.com/SH-Nihil-Mukkesh-25/Vaultify.git
   cd Vaultify
   ```

2. **Configure Credentials**
   ```cpp
   // WiFi Configuration
   const char* ssid = "Your_WiFi_Name";
   const char* password = "Your_WiFi_Password";
   
   // Twilio SMS Setup
   const String TWILIO_ACCOUNT_SID = "ACxxxxxxxxxxxxxxx";
   const String TWILIO_AUTH_TOKEN = "your_auth_token";
   ```

3. **Upload & Run** 🎉

---

## 🛠️ Hardware Setup

### 📦 Materials needed

| Component | Quantity | Purpose | 
|-----------|----------|---------|
| ESP32 DevKit | 1x | Main Controller | 
| MPU6050 | 1x | Motion Detection |
| MFRC522 RFID | 1x | Access Control |
| 16x2 I2C LCD | 1x | Status Display | 
| SG90 Servo | 1x | Lock Mechanism | 
| Buzzer | 1x | Audio Alerts | 
| RFID Cards | 2-5x | Access Keys | 

### 🔌 Pin Configuration

<div align="">

| 🎛️ **Component** | 📍 **ESP32 Pin** | 🔗 **Connection** |
|:---------------:|:----------------:|:-----------------:|
| 🔊 Buzzer | `GPIO 25` | Digital Output |
| ⚙️ Servo Motor | `GPIO 26` | PWM Signal |
| 📺 LCD (SDA) | `GPIO 21` | I2C Data |
| 📺 LCD (SCL) | `GPIO 22` | I2C Clock |
| 🏷️ RFID (SS) | `GPIO 5` | SPI Select |
| 🏷️ RFID (RST) | `GPIO 4` | Reset |
| 📊 MPU6050 | `I2C Bus` | Motion Sensor |

</div>


---

## 💻 Installation

### 1️⃣ **Arduino IDE Setup**

```bash
# Install ESP32 Board Package
# File → Preferences → Additional Board Manager URLs:
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
```

### 2️⃣ **Required Libraries**

| Library | Version | Installation |
|---------|---------|-------------|
| `LiquidCrystal_I2C` | Latest | Library Manager |
| `MPU6050_light` | Latest | Library Manager |
| `MFRC522` | Latest | Library Manager |
| `ESP32Servo` | Latest | Library Manager |

**Quick Install:**
```cpp
// In Arduino IDE: Tools → Manage Libraries → Search & Install:
LiquidCrystal I2C by Frank de Brabander
MPU6050 light by rfetick  
MFRC522 by GithubCommunity
ESP32Servo by Kevin Harrington
```

### 3️⃣ **Twilio Configuration**

1. Sign up at [Twilio.com](https://www.twilio.com/) 
2. Get a free phone number
3. Copy your Account SID & Auth Token
4. Update configuration:

```cpp
const String TWILIO_ACCOUNT_SID = "ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const String TWILIO_AUTH_TOKEN = "your_32_character_auth_token";
const String DEST_PHONE = "+1234567890";           // Your phone
const String TWILIO_FROM_NUMBER = "+1987654321";   // Twilio number
```

---

## Usage Guide

### 🔓 **Normal Operation**

<table>
<tr>
<td width="30%">

**🏷️ Unlock Door**
```
1. Hold RFID card near reader
2. Green beep confirms
3. Servo unlocks door
4. SMS: "Door unlocked"
```

</td>
<td width="30%">

**🔒 Lock Door**
```
1. Scan RFID again
2. Servo locks door
3. Display: "Door Locked"
4. SMS: "Door locked"
```

</td>
<td width="40%">

**⏰ Auto-Lock**
```
1. Door unlocked for 2 minutes
2. Warning countdown on LCD
3. Automatic lock activation
4. SMS: "Door auto-locked"
```

</td>
</tr>
</table>

---

## 🚨 **Security Modes**



<div align="center">

#### 🏃‍♂️ Motion Detection Flow



<table>
<tr>
<td width="16%" align="center">
<strong>🔍 Motion<br>Detected</strong>
</td>
<td width="4%" align="center">→</td>
<td width="16%" align="center">
<strong>🚨 Alarm<br>Activated</strong>
</td>
<td width="4%" align="center">→</td>
<td width="16%" align="center">
<strong>🔒 Door<br>Locks</strong>
</td>
<td width="4%" align="center">→</td>
<td width="16%" align="center">
<strong>📱 SMS<br>Alert</strong>
</td>
<td width="4%" align="center">→</td>
<td width="20%" align="center">
<strong>🔊 Continuous<br>Beeping</strong><br>
<em>(Until RFID scan)</em>
</td>
</tr>
</table>
</div>

<div align="center">

#### ❌ Unauthorized Access Response



<table>
<tr>
<td width="33%" align="center">
<h4>🔊 Audio Alert</h4>
<strong>3 Rapid Beeps</strong><br>
<code>BEEP! BEEP! BEEP!</code><br>
<em>150ms each</em>
</td>
<td width="33%" align="center">
<h4>📺 Visual Alert</h4>
<strong>LCD Display</strong><br>
<code>"Access Denied!"</code><br>
<em>2 seconds duration</em>
</td>
<td width="34%" align="center">
<h4>📱 Remote Alert</h4>
<strong>SMS Notification</strong><br>
<code>"Invalid RFID attempt!"</code><br>
<em>Sent immediately</em>
</td>
</tr>
</table>

</div>

<div align="center">

#### 🛡️ Security Status Overview

| 🟢 **Normal Mode** | 🟡 **Alert Mode** | 🔴 **Lockdown Mode** |
|:------------------:|:------------------:|:--------------------:|
| System monitoring | Invalid access detected | Theft attempt detected |
| RFID access enabled | Audio/visual warnings | All access disabled |
| Auto-lock timer active | SMS notifications sent | Continuous alarm |
| Standard operation | Heightened security | Emergency lockdown |

</div>

---

## 📊 System Status

### 📺 **LCD Display States**

<div align="center">

| 🟢 **Normal** | 🟡 **Door Open** | 🔴 **Theft Alert** |
|:-------------:|:----------------:|:-------------------:|
| System Normal | Door is Unlocked | !!! THEFT ALERT !!! |
| Door is Locked | Auto-Lock in 45s | Door Locked! |

</div>

### 🔊 **Audio Feedback**

<div align="center">

| Event | Pattern | Duration |
|-------|---------|----------|
| ✅ Valid Card | 1 short beep | 150ms |
| ❌ Invalid Card | 3 rapid beeps | 150ms × 3 |
| 🚨 Theft Alarm | Continuous cycle | 1s ON, 0.1s OFF |

</div>

---

## ⚙️ Customization

### 🎛️ **Adjustable Parameters**

```cpp
// Servo Positions
#define SERVO_LOCKED_POS 70      // Adjust for your lock mechanism
#define SERVO_UNLOCKED_POS 160   // Fine-tune door opening angle

// Security Settings  
#define ACCEL_THRESHOLD 0.6      // Motion sensitivity (lower = more sensitive)
const unsigned long ALARM_DURATION = 120000;    // 2 minutes alarm duration
const unsigned long DOOR_AUTO_CLOSE = 120000;   // 2 minutes auto-lock timer
```

### 🏷️ **Adding RFID Cards**

1. **Scan Unknown Card** (check Serial Monitor):
   ```
   New card detected: A1 B2 C3 D4
   ```

2. **Add to Valid Cards Array**:
   ```cpp
   byte validCards[][4] = {
     {0x3D, 0xF3, 0x3B, 0x06},  // Existing card
     {0xA1, 0xB2, 0xC3, 0xD4},  // New card ✨
   };
   ```

---

## 🔧 Troubleshooting

### 🌐 **WiFi Issues**
<details>
<summary>Click to expand solutions</summary>

```cpp
// Debug WiFi connection
Serial.println("WiFi Status: " + String(WiFi.status()));
Serial.println("SSID: " + String(WiFi.SSID()));
Serial.println("Signal Strength: " + String(WiFi.RSSI()) + " dBm");
```

**Common Fixes:**
- ✅ Verify 2.4GHz network (ESP32 doesn't support 5GHz)
- ✅ Check password accuracy  
- ✅ Ensure router is within range
- ✅ Restart router if needed
</details>

### 📱 **SMS Not Sending**
<details>
<summary>Click to expand solutions</summary>

**Checklist:**
- ✅ Twilio account has credit balance
- ✅ Phone numbers include country codes (+1, +91, etc.)
- ✅ Account SID and Auth Token are correct
- ✅ WiFi connection is stable

**Debug Code:**
```cpp
void debugTwilio() {
  Serial.println("Account SID: " + TWILIO_ACCOUNT_SID.substring(0, 8) + "...");
  Serial.println("Destination: " + DEST_PHONE);
  Serial.println("WiFi Connected: " + String(WiFi.status() == WL_CONNECTED));
}
```
</details>

### 🏷️ **RFID Problems**
<details>
<summary>Click to expand solutions</summary>

**Connection Test:**
```cpp
void setup() {
  // Add this to setup()
  if (!rfid.PCD_Init()) {
    Serial.println("❌ RFID initialization failed!");
  } else {
    Serial.println("✅ RFID ready");
  }
}
```

**Common Issues:**
- ✅ Check SPI connections (MISO, MOSI, SCK)
- ✅ Verify 3.3V power supply
- ✅ Try different RFID cards
- ✅ Clean card and reader surface
</details>

---


## 🤝 Contributors
| Contributor |
|-------------|
| [SH Nihil Mukkesh](https://github.com/SH-Nihil-Mukkesh-25) |
| [Dakshin Raj P](https://github.com/Dakshin10) |
| [Pravin Aditya] |
| [Sharvesh C] |



---

## 📜 License

<div align="center">

**MIT License** - See [LICENSE](LICENSE) file for details

*This project is open-source and free to use for educational and personal purposes.*

</div>

---


<div align="center">

### ⭐ **Star this repo if it helped you!**

**Made with ❤️ for the esp32 community**

*Secure your space, one line of code at a time* 🔐

---

</div>

# IOT-Group-Project


👥 Group Members
| 	Student Name	 | 	Student Number	 | 	Role/Responsibility	 | 
| 	:-----:	 | 	:-----:	 | 	:-----:	 | 
| 	Sisonke Mhlana	| 	221805486	| 	Value3	 | 
| 	Emmanuel Posholi	| 	222144408	| 	Value3	 | 
| 	Minathi Shezi	| 	222353775	| 	Value3	 | 

---

# 💡 Project Idea & Problem Statement
## Problem Statement
Many universities currently use RFID-based door access systems to manage entry into facilities such as lecture halls, laboratories, libraries, and student residences. However, these systems face several challenges, including weak security encryption, dependence on physical cards that can be lost or shared, limited real-time monitoring, and poor integration with modern technologies. In some cases, unauthorized individuals may gain access using stolen or duplicated RFID cards, which compromises campus security. Additionally, managing and updating access permissions across multiple buildings can become inefficient and time-consuming for university administrators.

## Proposed Solution
To solve these challenges, this project proposes upgrading the existing RFID system to an NFC-based door lock system. The new system will use NFC-enabled student cards and smartphones to provide faster, more secure, and more convenient authentication. NFC technology offers stronger encryption and better compatibility with modern mobile devices, reducing the risks associated with lost or duplicated cards. The system will also include centralized access management, real-time monitoring, and digital logging of entry and exit records. This solution will improve campus security, simplify access control management, and support the university’s move toward smarter and more modern technology systems. Due to component limitations, our prototype uses a physical student card or tag instead of a phone. However, the working system proves the concept. Future implementation with the university app would eliminate physical cards entirely.

---
# 🔧 Hardware Components
|  Component  |  Description  |	Quantity  |	Purpose  |
|  :-----:  |  :-----:  |  :-----  |  :-----  |
|  Arduino Uno  |  A microcontroller development board used to control electronic components and execute programmed instructions.  |  1  |  Acts as the main controller of the RFID/NFC door lock system by processing input from sensors and controlling the lock mechanism.  |
|  Relay Moddule  |  An electrically operated switch that allows low-voltage devices to control high-voltage components safely.  |  2  |  Used to switch the 12V solenoid lock ON or OFF based on authorization from the Arduino Uno.  |
|  12V Solenoid lock  |  An electronic locking device that uses electromagnetic force to lock or unlock a door.  |  1  |  It locks and unlocks the door physically when access is granted or denied.  |
|  IR sensor  |  Used to detect the presence or movement of objects.  |  1  |  Detects whether the door is open or closed, or senses motion near the door for security and automation purposes.  |
|  Bread board  |  A reusable board used for prototyping electronic circuits.  |  1  |  To allow easy connection and testing of components during system development.  |
|  RFID-RC522  |  module used to read RFID cards and tags.  |  1  |  To read and verifies RFID/NFC cards or tags to authenticate authorized users.  |
|  Buzzer  |  An audio signaling device that produces sound alerts or notifications.  |  1  |  Provides sound feedback for successful or failed access attempts.  |
|  LED light  |  A light-emitting diode used as a visual indicator in electronic systems.  |  2  |  Indicates system status, such as access granted (green LED) or access denied (red LED).  |
|  DSTV power Supply  |  A power adapter commonly used in electronic setups to provide stable DC voltage.   |  1  |  To act as the main power supply that supply the whole system with power, ensuring a stable operation of the Arduino, Relay and solenoid lock.  |

---

# 💻 Software & Technologies
| Platform	| Purpose |
| :-----: | :-----: |
| Arduino IDE | Used to write, compile, and upload code to the Arduino Uno for controlling the RFID/NFC door lock system. |

---

# 🖥️ Code Documentation
C++
```
#include <SPI.h>
#include <MFRC522.h>

#define RST_PIN 9
#define SS_PIN 10

MFRC522 mfrc522(SS_PIN, RST_PIN);

void setup() {
    Serial.begin(9600);
    SPI.begin();
    mfrc522.PCD_Init();
    mfrc522.PCD_SetAntennaGain(MFRC522::RxGain_max);
    Serial.println("RFID Test - Hold card on reader");
    Serial.println("Keep card still for 1-2 seconds");
}

void loop() {
    if (mfrc522.PICC_IsNewCardPresent()) {
        if (mfrc522.PICC_ReadCardSerial()) {
            Serial.print("✓ Card detected! UID: ");
            for (byte i = 0; i < mfrc522.uid.size; i++) {
                Serial.print(mfrc522.uid.uidByte[i], HEX);
                Serial.print(" ");
            }
            Serial.println();
            mfrc522.PICC_HaltA();
            delay(1000);
        } else {
            Serial.println("Card detected but read failed - try again");
        }
    } else {
        Serial.println("No card - waiting...");
    }
    delay(500);
} 
```
# Key Functions
| Function Name             | Description                                                                                |
| ------------------------- | ------------------------------------------------------------------------------------------ |
|  setup()                  | Initializes hardware peripherals, SPI communication, RFID reader, and serial communication |
|  loop()                   | Continuously checks for RFID cards and reads/display the card UID                          |
|  PICC_IsNewCardPresent()  | Detects whether a new RFID card is near the reader                                         |
|  PICC_ReadCardSerial()    | Reads the UID (serial number) of the detected RFID card                                    |
|  PCD_Init()               | Initializes the MFRC522 RFID reader module                                                 |
|  PCD_SetAntennaGain()     | Sets the RFID antenna signal strength to maximum                                           |
|  PICC_HaltA()             | Stops communication with the RFID card after reading                                       |
|  SPI.begin()              | Starts SPI communication between the Arduino and RFID module                               |
|  Serial.begin()           | Starts serial communication with the computer                                              |
| delay()                   | Pauses the program for a specified amount of time                                          |



<p align="center">
  <img src="http://i.imgur.com/rOqMdwp.png" alt="msfpc logo"/>
</p>

[![Version](https://img.shields.io/badge/VENOM-1.0.17-brightgreen.svg?maxAge=259200)]()
[![Stage](https://img.shields.io/badge/Release-Stable-brightgreen.svg)]()
![licence](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)

[![Arduino Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-alpine.svg?left_text=Alpine%20Linux%20Build)](##Link##)
[![Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-kali.svg?left_text=Kali%20Linux%20Build)](##Link##)
[![Armel Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-armel.svg?left_text=Armel%20Kali%20Linux%20Build)](##Link##)
[![Armhf Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-armhf.svg?left_text=Armhf%20Kali%20Linux%20Build)](##Link##)
[![DragonFly BSD Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-dfly.svg?left_text=DragonFly%20Build)](##Link##)
[![FreeBSD 11 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-fbsd-11.svg?left_text=FreeBSD%2011%20Build)](##Link##)
[![FreeBSD 12 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-fbsd-12.svg?left_text=FreeBSD%2012%20Build)](##Link##)
[![OpenBSD 6 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-obsd.svg?left_text=OpenBSD%20Build)](##Link##)
[![NetBSD 8.1 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-netbsd81.svg?left_text=NetBSD%20Build)](##Link##)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/aircrack-ng/badge.svg)](##Link##)

# Program-RFID-Arduino


## Contributors:

To keep this collection up-to-date need contributors who can add more Program Arduino scripts and github repo here at one place.  
||
|--------------|
|:octocat: [arthasa28](https://github.com/arthasa28)
|:octocat: [Dickybulin26](https://github.com/Dickybulin26)
|:octocat: [robotika-smkn1](https://github.com/robotika-smkn1)

# Source Code

```bash
/*
 * 
 * All the resources for this project: smkn1kotabekasi.sch.id
 * Modified by Robotika smkn1 kotabekasi
 * 
 * Created by Robotika smkn1 kotabekasi
 * 
 */
 
#include <SPI.h>
#include <MFRC522.h>
 
#define SS_PIN 10
#define RST_PIN 9
MFRC522 mfrc522(SS_PIN, RST_PIN);   // Create MFRC522 instance.
 
void setup() 
{
  Serial.begin(9600);   // Initiate a serial communication
  SPI.begin();      // Initiate  SPI bus
  mfrc522.PCD_Init();   // Initiate MFRC522
  Serial.println("Approximate your card to the reader...");
  Serial.println();

}
void loop() 
{
  // Look for new cards
  if ( ! mfrc522.PICC_IsNewCardPresent()) 
  {
    return;
  }
  // Select one of the cards
  if ( ! mfrc522.PICC_ReadCardSerial()) 
  {
    return;
  }
  //Show UID on serial monitor
  Serial.print("UID tag :");
  String content= "";
  byte letter;
  for (byte i = 0; i < mfrc522.uid.size; i++) 
  {
     Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
     Serial.print(mfrc522.uid.uidByte[i], HEX);
     content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
     content.concat(String(mfrc522.uid.uidByte[i], HEX));
  }
  Serial.println();
  Serial.print("Message : ");
  content.toUpperCase();
  if (content.substring(1) == "08 8E 73 A0") //change here the UID of the card/cards that you want to give access
    {
    Serial.println("Authorized access");
    Serial.println();
    delay(3000);
  }
 
 else   {
    Serial.println(" Access denied");
    delay(3000);
  }
} 
```

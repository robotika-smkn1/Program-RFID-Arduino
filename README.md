# Program-RFID-Arduino

[![Alpine Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-alpine.svg?left_text=Alpine%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-kali.svg?left_text=Kali%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![Armel Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-armel.svg?left_text=Armel%20Kali%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![Armhf Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-armhf.svg?left_text=Armhf%20Kali%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![DragonFly BSD Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-dfly.svg?left_text=DragonFly%20Build)](https://buildbot.aircrack-ng.org/)
[![FreeBSD 11 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-fbsd-11.svg?left_text=FreeBSD%2011%20Build)](https://buildbot.aircrack-ng.org/)
[![FreeBSD 12 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-fbsd-12.svg?left_text=FreeBSD%2012%20Build)](https://buildbot.aircrack-ng.org/)
[![OpenBSD 6 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-obsd.svg?left_text=OpenBSD%20Build)](https://buildbot.aircrack-ng.org/)
[![NetBSD 8.1 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-netbsd81.svg?left_text=NetBSD%20Build)](https://buildbot.aircrack-ng.org/)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/aircrack-ng/badge.svg)](https://scan.coverity.com/projects/aircrack-ng)
[![PackageCloud DEB](https://img.shields.io/badge/deb-packagecloud.io-844fec.svg)](https://packagecloud.io/aircrack-ng/git/install#bash-deb)
[![PackageCloud RPM](https://img.shields.io/badge/rpm-packagecloud.io-844fec.svg)](https://packagecloud.io/aircrack-ng/git/install#bash-rpm)

#Source Code

```
/*
 * 
 * All the resources for this project: https://randomnerdtutorials.com/
 * Modified by Rui Santos
 * 
 * Created by FILIPEFLOP
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

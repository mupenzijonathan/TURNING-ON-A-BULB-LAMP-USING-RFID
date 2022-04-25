# TURNING-ON-A-BULB-LAMP-USING-RFID

# ABSTRACT

Radio Frequency Identification (RFID) is low cost sensor, begun to be used since 1945s in WW II by the organization of pioneers of USSR (Soviet Union) trapped the USA ambassador by activating a radio waves that could give signals of private information directly from US embassy to Soviet.[1] It continued to be used until 1970s, where the RFID tags started to be used in rail ways monitoring carriages but conventionally was invented in 1983s by Charles Walton to be used in different sector including bulb lighting[1]. 
RFID enables many Human-computer interaction (HCI) applications include control lighting system; the control of lighting system is made normally with famous way of showing rfid tag or rfid card to an rfid reader (module).[2]  The rfid module hold information related to rfid tags and rfid cards, only authorized tags and cards would be able to access to the system wirelessly by putting the rfid tag or card near to rfid reader to avoid disturbance or unwanted switching and It needs the Arduino to be programmed.[2] Lighting bulb lamp require high voltage than one used by Arduino that’s why we include the relay to switch ON or OFF the bulb lamp.
This project has both electrical and electronics purpose and lighting is one of the most used resources take place in human infrastructures.[1] In this work we tried to make the source code and use some software like Proteus and Fritzing to run the system before implementation.

# Problem statement
 
Actually, the lighting is good thing in our daily life but when it comes on switching in unwanted condition, which leads to high paying electricity bills. 
	High security 
	Reduction of power consumption by avoiding unwanted lighting 
	 Low electricity paying bill due to reduction of power consumption 
These are the some of problem statement we have tried to focus on during implementation of this circuit.	
# HOW THE INTERFACE OF RFID TO ARDUINO UNO IS DONE?
![image](https://user-images.githubusercontent.com/104397477/165186478-ba6e77d7-ccc1-4817-9a39-69445964e4e5.png)
![image](https://user-images.githubusercontent.com/104397477/165186513-e2dddd8e-462b-480f-aeb3-c5a186bdda1c.png)


Fig. 1 Interface of rfid to Arduino UNO board  
                                                                                 
# Circuit diagram in proteus
![image](https://user-images.githubusercontent.com/104397477/165186531-5505977f-1e36-46fb-958f-b71c4542fb8c.png)

 
Fig.2 Simulation Image in proteus

While using proteus software the virtual terminals will act as an rfid reader, where their connection made oppositely; I.e. RXD of virtual terminal will be connected to TXD of Arduino UNO board and vice versa.

# CIRCUIT DIGRAM DRAWN IN FRITZING
![image](https://user-images.githubusercontent.com/104397477/165186583-87d868e5-0967-4f63-b778-7bb418d86805.png)



 # CIRCUIT DESCRIPTION
 
	ARDUINO UNO BOARD  and A to B USB cable

	BREADBORD 

	RELAY

	DIODE

	TRANSISTOR

	RESISTOR

	LAMPS

	AC Source

	RFID Module

	RFID tag

	RFID card

	Connection wires

 # The source Code of RFID controlling lamp
 
#include <SPI.h>

 #include <MFRC522.h>
 
 #define SS_PIN 10
 
 #define RST_PIN 9
 
 #define RELAY 4 
 
  MFRC522 mfrc522(SS_PIN, RST_PIN);
  
 void setup()  
 
 {  Serial.begin(9600);
 
  SPI.begin();   
  
 mfrc522.PCD_Init(); 
 
  pinMode(4, OUTPUT); 
  
 Serial.println("put your to the reader ...");  
 
 Serial.println(); }  
 
void loop()  
{  
  if ( ! mfrc522.PICC_IsNewCardPresent())
  
 {  
return;  

  }  
  if ( ! mfrc522.PICC_ReadCardSerial())
  
  {  
   return;  
  } 
  
  Serial.print("UID tag :");  
  
  String content = ""; 
  
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
  
  if (content.substring(1) == "54 0D 70 23") //change here the UID of the card/cards that you want to give access 
  
  {  
   Serial.println("VALID UID"); 
   
   Serial.println(); 
   
   delay(500);  
   
   digitalWrite(4, HIGH);
   
   delay(2000);  
   
   digitalWrite(4, LOW);  
   
   delay(2000);
   
  }  
  else if (content.substring(1) == "E9 49 FD B9") //change here the UID of the card/cards that you want to give access 
  
  {  
   Serial.println("VALID UID");
   
   Serial.println(); 
   
   delay(500); 
   
   digitalWrite(4, HIGH);
   
   delay(2000); 
   
   digitalWrite(4, LOW);
   
   delay(2000); }
   
  else  
  
  {  Serial.println(" INVALID UID");
  
   digitalWrite(4, LOW);   }  }
   
# CONCLUSION 

RFID gives reliable track and trace in any environmental condition. This technology provides real time data collection about the card or tag by giving quick response

automatically after sensing the UID. We have focused only to the lighting but the rfid system applied in many sectors like in business of all size, voting and other sectrors.

# REFERENCES
[1]	R. F. Identification, “RFID Privacy : An Overview,” 2005.

[2]	J. Gummeson, J. Mccann, C. J. Yang, D. Ranasinghe, S. Hudson, and A. Sample, “RFID Light Bulb : Enabling Ubiquitous Deployment of Interactive RFID Systems,” vol. 1, no. 2, 2017.

[1]	R. F. Identification, “RFID Privacy : An Overview,” 2005.

[2]	J. Gummeson, J. Mccann, C. J. Yang, D. Ranasinghe, S. Hudson, and A. Sample, “RFID Light Bulb : Enabling Ubiquitous Deployment of Interactive RFID Systems,” vol. 1, no. 2, 2017.

[1]	R. F. Identification, “RFID Privacy : An Overview,” 2005.

[2]	J. Gummeson, J. Mccann, C. J. Yang, D. Ranasinghe, S. Hudson, and A. Sample, “RFID Light Bulb : Enabling Ubiquitous Deployment of Interactive RFID Systems,” vol. 1, no. 2, 2017.



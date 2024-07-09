# CODETECH-INTERNSHIP-IOT-T2

**Name**: GOPINATH V
**Company**: CODETECH IT SOLUTIONS
**ID**: CT08DS1826
**Domain**: Internet of Things
**Duration**: June to July 2024
**Mentor**: Mohammed Muzammil Ahmed

## Overview of the Project
**Project: Home Automation using ESP32 with Light Bulb and RemoteXY**
### Objective
The objective of this project is to create a WiFi-based control system for a light bulb using the RemoteXY platform. The system allows users to control the light bulb's state (ON/OFF) via a graphical user interface on a connected device.

#### Key Activities
- Setup WiFi Connection: - Configure the microcontroller as a WiFi access point with a predefined SSID and password. This setup allows devices to connect to the network and access the control interface.

- Configure RemoteXY Interface: - Define and initialize the RemoteXY interface with a simple GUI that includes a switch to -control the light bulb. This involves setting up the necessary input and output variables.

- Control Light Bulb: - Implement the logic to change the light bulb's state based on user input from the RemoteXY interface. The state change is reflected in real-time by writing to the appropriate GPIO pin.

- Serial Communication: - Use serial communication to debug and monitor the state changes of the light bulb. Print messages to the serial monitor indicating whether the light bulb is ON or OFF, which aids in troubleshooting.

- State Change Detection: - Detect changes in the light bulb's state and update the serial monitor only when a change occurs. This reduces unnecessary serial output and helps identify the exact moment of state transitions.

- RemoteXY Handling: - Continuously handle RemoteXY events and update the control interface. Ensure that the system remains responsive to user inputs and maintains a stable connection.

##### Technologies Used
1. WiFi Library: - Utilizes the WiFi library to establish the microcontroller as a WiFi access point, enabling wireless 2. 2. communication. This library handles network setup, connection management, and data transmission.

3. RemoteXY Library: - Employs the RemoteXY library to create a user-friendly graphical interface for remote control. This library simplifies the creation of GUIs and handles the communication between the control interface and the microcontroller.

4. Serial Communication: - Uses the Serial library for debugging and monitoring purposes. This technology provides a simple way to output messages to the serial monitor, helping developers track the system's behavior.

5. Microcontroller (e.g., ESP32): - The core hardware component that runs the control system, manages WiFi connections, interfaces with the RemoteXY library, and controls the light bulb via GPIO pins.

6.GPIO (General Purpose Input/Output): - Utilizes GPIO pins on the microcontroller to physically control the light bulb. The digitalWrite function sets the pin high or low, turning the light bulb on or off based on the RemoteXY input.

###### Hardware and Software Required
● ESP32
● Light Bulb
● Realy
● Breadboard
● Jumper wires and normal copper wire
● Wire Plug
● Bulb Holder
● USB cable for Programming(ESP32)
● Arduino IDE
● RemoteXY

##### Steps to do this project:
1. Ensure Latest Arduino IDE:

 ● Before starting, make sure you have the latest version of the Arduino IDE installed. If not, uninstall the current version and install the latest one to ensure compatibility.
2. Add ESP32 to Arduino IDE:

● Open Arduino IDE.
● Go to **File > Preferences**.
● In the "Additional Board Manager URLs" field, enter the following URLs: 
  https://dl.espressif.com/dl/package_esp32_index.json, http://arduino.esp8266.com/stable/package_esp8266com_index.json 
● Click **OK**.
3. Install ESP32 Board:

● Open the Boards Manager by navigating to **Tools > Board > Boards Manager**.
● Search for **ESP32**.
● Click the **Install** button for **ESP32 by Espressif Systems**.
4. Install Required Libraries:

● Open the Library Manager by going to **Tools > Manage Libraries**.
● Search for **RemoteXY** and install it.
● Search for **WiFi** and ensure it is installed.
5. Set Up WiFi Connection:

● Define the WiFi settings in your code:

  #define REMOTEXY_MODE__WIFI_POINT 
  #define REMOTEXY_WIFI_SSID "RemoteXY" 
  #define REMOTEXY_WIFI_PASSWORD "12345678" 
  #define REMOTEXY_SERVER_PORT 6377

● Include the necessary libraries:

  #include <WiFi.h> <br>
  #include <RemoteXY.h> <br>
6. Configure RemoteXY Interface:

● Define the GUI configuration:

  uint8_t RemoteXY_CONF[] = { 255,1,0,0,0,29,0,17,0,0,0,164,1,106,200,1,1,1,0,2,31,80,44,22,1,36,26,31,31,79,70,70,0,79,78,0 };
  
● Define the RemoteXY structure:

  struct {
    uint8_t Light_Bulb; // =1 if switch ON and =0 if OFF
    uint8_t connect_flag;  // =1 if wire connected, else =0
  } RemoteXY;
7. Initialize RemoteXY and Set Up GPIO:

● In the **setup()** function, initialize RemoteXY and set the pin mode: 
  
  void setup() {  
    RemoteXY_Init(); 
    pinMode(PIN_LIGHT_BULB, OUTPUT);
    Serial.begin(115200); 
  }
8. Control Light Bulb:

● In the loop() function, handle RemoteXY events and control the light bulb: void loop() {
RemoteXY_Handler();
digitalWrite(PIN_LIGHT_BULB, (RemoteXY.Light_Bulb == 0) ? LOW : HIGH);
}

9. Monitor State Changes:

● Add logic to monitor and print state changes to the Serial monitor: bool lastState = LOW;

 void loop() { 
   RemoteXY_Handler(); 
   bool currentState = (RemoteXY.Light_Bulb == 0) ? LOW : HIGH; 
   if (currentState != lastState) { 
     if (currentState == HIGH) { 
       Serial.println("Light Bulb is OFF"); 
     } else { 
       Serial.println("Light Bulb is On"); 
     } 
     lastState = currentState; 
   } 
 } 
10. Final Touches:

● Avoid using delay() in the loop; use RemoteXY_delay() if needed.
● Ensure the setup and loop functions are correctly defined and free of blocking code.

11. Upload and Test:

● Connect your ESP32 board to the computer.
● Select the correct board and port from the Tools > Board and Tools > Port menus.
● Upload the code to your ESP32.
● Connect to the "RemoteXY" WiFi network using the password "12345678".
● Open the RemoteXY app on your device, connect to the ESP32, and control the light bulb.

##### Circuit Diagram
![alt text](https://private-user-images.githubusercontent.com/167459628/346841338-093401d8-2d15-4e00-b515-2e5cad7874aa.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjA1MTIxMjcsIm5iZiI6MTcyMDUxMTgyNywicGF0aCI6Ii8xNjc0NTk2MjgvMzQ2ODQxMzM4LTA5MzQwMWQ4LTJkMTUtNGUwMC1iNTE1LTJlNWNhZDc4NzRhYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcwOVQwNzU3MDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wZmQyYjgxNzM3OTBlOWQ0MDQwZjBmOWRmYzM0YWM0Zjg3NzkxNzEwNmMzNTM2OTZjYTc0MjA3OWNlY2E4OGQzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.XvRHFV6KtTDMOa7LJi1uJev8kq2XrC-SVodWohMWVLY)

##### Output in Serail Monitor
![alt text](https://private-user-images.githubusercontent.com/167459628/346842032-c23008c7-2123-4d58-8f1d-e6866dbcf20c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjA1MTIxMjcsIm5iZiI6MTcyMDUxMTgyNywicGF0aCI6Ii8xNjc0NTk2MjgvMzQ2ODQyMDMyLWMyMzAwOGM3LTIxMjMtNGQ1OC04ZjFkLWU2ODY2ZGJjZjIwYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcwOVQwNzU3MDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jNmIwYzMzODY4NjdhN2FlYjQ5MjM1NjQ2ODM2MTRkMTdiNGM2MzQ1NjZmZDNhN2I5NTM3NzBmMjU4ZTMyYmZjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.MvjIA63aZmALWkyg_KQ7fVcl9LYX1LR0lxrEEm4Kafs)

##### Graphical Interface in RemoteXY
![alt text](https://private-user-images.githubusercontent.com/167459628/346842370-7c2a3b60-9663-4e75-b815-7ea3ee258cae.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjA1MTIxMjcsIm5iZiI6MTcyMDUxMTgyNywicGF0aCI6Ii8xNjc0NTk2MjgvMzQ2ODQyMzcwLTdjMmEzYjYwLTk2NjMtNGU3NS1iODE1LTdlYTNlZTI1OGNhZS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcwOVQwNzU3MDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xOGM4MmI0YzMyODYyOTgxYzU1Mjk3NzliZjhlZDIyMjc3ZmVhMDQzNTBjZjFlYWI0MDU2ZTIyZDdkYzQ1YWUyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.6KlllQj2L1hCW7mNgGd4rZOYAMN0zs4rTIk2HdNCEww)

###### Output when Light Bulb is OFF
![alt text](https://private-user-images.githubusercontent.com/167459628/346843078-1d7914e6-4330-4318-b735-1192ef3038a8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjA1MTIxMjcsIm5iZiI6MTcyMDUxMTgyNywicGF0aCI6Ii8xNjc0NTk2MjgvMzQ2ODQzMDc4LTFkNzkxNGU2LTQzMzAtNDMxOC1iNzM1LTExOTJlZjMwMzhhOC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcwOVQwNzU3MDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hYmEyOTU0YjBhYjNiNTE4YjIwOGQ0YmQzNmNkZWE0YWM3OTYyMTNlYzcwOTQ3NDYzNjRmOWNmYmIwNTQ2MmU0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.DoSqM3IePXBZEXHO6y15QnStGgUPbz1G6qNIutw0MCM)

###### Output when Light Bulb is ON
![alt text](https://private-user-images.githubusercontent.com/167459628/346843196-2b089455-8bfb-4c07-b6e3-41947b1a0cc0.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjA1MTIxMjcsIm5iZiI6MTcyMDUxMTgyNywicGF0aCI6Ii8xNjc0NTk2MjgvMzQ2ODQzMTk2LTJiMDg5NDU1LThiZmItNGMwNy1iNmUzLTQxOTQ3YjFhMGNjMC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcwOVQwNzU3MDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05Nzc2MGRjZmFkYmEyMTk0MjlkZTNiYmYyZmQxOTFhMTE3MjA5MjI4MDM0YWExNzhmZDhjNjlkNjA4ZjZmYmUxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.L-o-CxP6h3AHP2TglA62RtcvsMUMHKVgHOl4C-3IW10)

##### Conclusion
This project not only demonstrates the basics of remote device control but also lays the groundwork for more advanced IoT applications. Anyone can further expand this project by integrating additional sensors, actuators, or incorporating cloud-based services for data logging and analysis.With this foundational knowledge, you are well-equipped to explore and innovate in the realm of IoT and home automation. Happy tinkering!

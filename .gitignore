// RemoteXY select connection mode and include library 
#define REMOTEXY_MODE__WIFI_POINT

#include <WiFi.h>

// RemoteXY connection settings 
#define REMOTEXY_WIFI_SSID "RemoteXY"
#define REMOTEXY_WIFI_PASSWORD "12345678"
#define REMOTEXY_SERVER_PORT 6377


#include <RemoteXY.h>

// RemoteXY GUI configuration  
#pragma pack(push, 1)  
uint8_t RemoteXY_CONF[] =   // 36 bytes
  { 255,1,0,0,0,29,0,17,0,0,0,164,1,106,200,1,1,1,0,2,
  31,80,44,22,1,36,26,31,31,79,70,70,0,79,78,0 };
  
// this structure defines all the variables and events of your control interface 
struct {

    // input variables
  uint8_t Light_Bulb; // =1 if switch ON and =0 if OFF

    // other variable
  uint8_t connect_flag;  // =1 if wire connected, else =0

} RemoteXY;   
#pragma pack(pop)

#define PIN_LIGHT_BULB 5

bool lastState = LOW;

void setup() 
{
  RemoteXY_Init (); 
  
  pinMode (PIN_LIGHT_BULB, OUTPUT);
  Serial.begin(115200);
}

void loop() 
{ 
  RemoteXY_Handler ();
  
  digitalWrite(PIN_LIGHT_BULB, (RemoteXY.Light_Bulb==0)?LOW:HIGH);
  
  bool currentState = (RemoteXY.Light_Bulb==0)?LOW:HIGH;
  if (currentState != lastState) {
    if (currentState == HIGH) {
      Serial.println("Light Bulb is OFF");
    } else {
      Serial.println("Light Bulb is On");
    }
    lastState = currentState;
  }
  // use the RemoteXY structure for data transfer
  // do not call delay(), use instead RemoteXY_delay() 
}

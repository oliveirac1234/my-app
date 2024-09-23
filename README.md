# my-app
#include <BluetoothSerial.h>
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
BluetoothSerial SerialBT;
String message = "";

void setup() {
  SerialBT.begin("CONTROLE_DA_PRANCHA 💡");  //Bluetooth device name
  Serial.println("oi");
  delay(100);
  Serial.begin(115200);
}

void loop() {
  Serial.println("oi");
  delay(100);
  if (SerialBT.available()) {
    char bt = SerialBT.read();
    if (bt != '\n') {
      message += String(bt);
    } else {
      message = "";
    }
    Serial.write(bt);
    Serial.print("   ____   ");
    Serial.println(message);

    if (message == "tomada") {
      //estado_pin_tomada = !estado_pin_tomada;
    }
    if (message == "estrela") {
      //estado = !estado;
    }
   
  } else {
    message = "";
  }
}

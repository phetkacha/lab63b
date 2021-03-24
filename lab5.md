# การทดลองที่ 5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์
## วัตถุประสงค์

  1.เพื่อทำการทดลองเขียนโปรแกรมเพื่อเชื่อมต่อ wifi และ web server

## แหล่งข้อมูลเพื่อการศึกษา

  วิธีติดตั้งโปรแกรมgit https://www.youtube.com/watch?v=9aF0upI9Gic 
  
  วิธีการทำการทดลอง https://youtu.be/VX-QNQcO-b4
  
## อุปกรณ์ 

  1.อุปกรณ์ต่อUSBเพื่อไปยังSerial

  2.ไมโครคอนโทรเลอร์ (ESP01)

  3.wifi ที่ต้องการเชื่อมกับ microcontroller

  4.CPU

## วิธีทำการทดลอง

  1.เปิดโปรแกรมตัวอย่างโดยการเปิดcommand promptหลังจากติดตั้งโปรแกรมgit โดยการดูที่ตัวอย่างโปรแกรม ที่โฟลเดอร์ pattani

    - โฟล์เดอร์PATANIจะแสดงโปรแกรมตัวอย่าง 9 โปรแกรม ไปที่ตัวอย่างที่5 แล้วพิมพ์ cd 05_Wifi-Web-Sever
  
  2.ดู Source code program โดยจะมีสองส่วนคือ Set up และ Loop
    
    - Set up เป็นส่วนของการเชื่อมต่อ Wifi 
    จะได้ผลดังนี้
    #include <ESP8266WiFi.h>
    //#include <WiFiClient.h>
    #include <ESP8266WebServer.h>

    const char* ssid = "HI_BMFWIFI_2.4G";
    const char* password = "0819110933";

    ESP8266WebServer server(80);

    int cnt = 0;

    void setup(void){
	          Serial.begin(115200);

	          WiFi.mode(WIFI_STA);
	          WiFi.begin(ssid, password);
	          while (WiFi.status() != WL_CONNECTED) {
		                delay(500);
		                Serial.print(".");
	          }
	          Serial.print("\n\nIP address: ");
	          Serial.println(WiFi.localIP());

	          server.onNotFound([]() {
		                server.send(404, "text/plain", "Path Not Found");
	          });

	          server.on("/", []() {
		                cnt++;
		                String msg = "Hello cnt: ";
		                msg += cnt;
		                server.send(200, "text/plain", msg);
	           });

	           server.begin();
	           Serial.println("HTTP server started");
    }

    void loop(void){
      server.handleClient();
    }
  
  3.ใช้คำสั่งอัพโหลด ในการอัพโหลดโปรแกรมเข้าไปในไมโครคอนโทรลเลอร์ โดยทำตามขั้นตอนดังนี้

     - พิมพ์ pio run -t upload

  4.ทำการเสียบไมโครคอนโทรลเลอร์ เข้าที่Serial port ของUSB
  
  5.ในขณะที่ program กำลังรันข้อมูล เพื่อให้ไมโครคอนโทรลเลอร์รับโปรแกรมใหม่เข้าไป ให้กดปุ่มสีแดง เพื่อให้เกิดการ resetแล้วสังเกตผลลัพธ์ที่แสดงผลผ่านคอมพิวเตอร์ จากนั้น

     - พิมพ์ pio device monitor
     - ผลลัพธ์ที่แสดง คือ ip address
     - copy ip adress ไปที่ browser เพื่อทำการทดสอบ
     
## อภิปรายผลการทดลอง

  ในการอัพโหลดข้อมูลจาก 05_Wifi-Web-Sever ไปยังไมโครคอนโทรลเลอร์ ต้องใช้คำสั่ง pio run-t upload เพื่ออัพโหลด และใช้คำสั่ง pio device monitor สำหรับใช้ดูผลลัพท์ของโปรแกรม
  
## คำถามหลังการทดลอง

  ก่อนที่จะทำการอัพโหลด ต้องกดปุ่มใด
  
  ตอบ  กดปุ่ม 0 หรือ port

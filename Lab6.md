# การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)
## วัตถุประสงค์

  1. เพื่อทำการเขียนโปรแกรมที่จะสร้าง Wifi Access Point ขึ้นมาเอง
  
  2. เพื่อนโปรแกรมไปใช้ในการเชื่อมต่อ wifi ของตัวเองเข้ากับอุปกรณ์ตัวอื่นๆ

## แหล่งข้อมูลเพื่อการศึกษา

  วิธีติดตั้งโปรแกรมgit https://www.youtube.com/watch?v=9aF0upI9Gic
  
  วิธีทำการทดลอง https://youtu.be/T26DVHePlTs
  
## อุปกรณ์

  1.ไมโครคอนโทรเลอร์ (ESP01)

  2.อุปกรณ์ต่อUSBเพื่อไปยังSerial

  3.CPU

## วิธีทำการทดลอง

  1.เสียบไมโครคอนโทรเลอร์เข้ากับSerial

  2.เปิดโปรแกรมตัวอย่างโดยการเปิดcommand promptหลังจากติดตั้งโปรแกรมgit โดยการดูที่ตัวอย่างโปรแกรม ที่โฟลเดอร์ pattani

     - โฟล์เดอร์PATANIจะแสดงโปรแกรมตัวอย่าง 9 โปรแกรม ไปที่ตัวอย่างที่6 แล้วพิมพ์ cd 04_Output-Port

  3. ดู Source Code Program 
  
    - พิมพ์ vi src/main.cpp
      #include <ESP8266WiFi.h>
      //#include <WiFiClient.h>
      #include <ESP8266WebServer.h>

      const char* ssid = "MY-ESP8266";
      const char* password = "choompol";

      IPAddress local_ip(192, 168, 1, 1);
      IPAddress gateway(192, 168, 1, 1);
      IPAddress subnet(255, 255, 255, 0);

      ESP8266WebServer server(80);

      int cnt = 0;

      void setup(void){
	            Serial.begin(115200);

	            WiFi.softAP(ssid, password);
	            WiFi.softAPConfig(local_ip, gateway, subnet);
	            delay(100);

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
        
  3. ทำการกำหนดค่าต่างๆ ดังนี้
          
    - กำหนดชื่อและตั้งรหัสผ่าน ที่จุดนี้
   <img width="954" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 20 05 54" src="https://user-images.githubusercontent.com/80880050/112315141-66c7dc80-8cdc-11eb-90da-fffa67663931.png">

    - กำหนด IPAdress, gateway, subnet
  <img width="957" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 20 07 08" src="https://user-images.githubusercontent.com/80880050/112315264-8bbc4f80-8cdc-11eb-81ed-6494d80fed56.png">

    - เตรียม web server
<img width="957" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 20 08 30" src="https://user-images.githubusercontent.com/80880050/112315442-bad2c100-8cdc-11eb-91f9-9267a53183fc.png">

    - รันคำสั่ง softAP แล้วกำหนด ssiad กับ password
 <img width="957" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 20 09 35" src="https://user-images.githubusercontent.com/80880050/112315651-e6ee4200-8cdc-11eb-8683-408ffc593c63.png">

    - ใช้คำสั่งอัพโหลด ในการอัพโหลดโปรแกรมเข้าไปในไมโครคอนโทรลเลอร์ โดยทำตามขั้นตอนดังนี้
        - พิมพ์ pio run -t upload
        - ในขณะที่ program กำลังรันข้อมูล เพื่อให้ microcontroller รับโปรแกรมใหม่เข้าไป กดปุ่มสีแดง เพื่อให้เกิดการ reset

  4.ตรวจสอบว่า wifi ที่สร้างขึ้นนั้นแสดงผลหรือยัง โดยการพิมพ์ pio device monitor และใช้มือถือค้นหาWifi
 
 <img width="1440" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 20 12 32" src="https://user-images.githubusercontent.com/80880050/112316056-53694100-8cdd-11eb-9497-5057fffaa205.png">

## อภิปรายผลการทดลอง 
  
  จากการทดลองดังกล่าว โปรแกรม 06_Wifi-AP-Web-Server ทำให้เราสามารถสร้าง Wifi Access Point ขึ้นมาเองได้ และตรวจสอบพบว่ามีอยู่จริง 
  
  <img width="461" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 20 14 23" src="https://user-images.githubusercontent.com/80880050/112316300-8f9ca180-8cdd-11eb-8633-f589055ff617.png">

## คำถามหลังการทดลอง

ประโยชน์ของการสร้าง   Wifi Access Point ได้เอง คืออะไร

ตอบ สามารถมีสัญญาณข่ายWifi เป็นของตัวเอง และสามารถแชร์ต่อให้คนอื่นได้ โดยที่เราสามารถกำหนดค่าต่างๆได้เอง
  

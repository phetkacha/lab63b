# การทดลองที่7 การทดลองใช้หลอดไฟLEDแสดงการใช้งานของการเชื่อมต่อWifi
## วัตถุประสงค์

  1.เพื่อทำการทดลองรันไมโครคอลโทรลเลอร์ให้หลอดไฟLEDแสดงเมื่อมีการเชื่อมต่อWifi
  
## แหล่งข้อมูลเพื่อการศึกษา

  1.วิธีติดตั้งโปรแกรมgit https://www.youtube.com/watch?v=9aF0upI9Gic
  
  2.วิธีการทำการรันโปรแกรมให้ไมโครคอนโทรลเลอร์ https://youtu.be/CCnN1WJsXQY , https://youtu.be/6JnhaUILGuw
  
  3.วิธีการเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์(Wifi AP) https://youtu.be/T26DVHePlTs
  
##  อุปกรณ์

  1.ไมโครคอนโทรเลอร์ (ESP01)

  2.อุปกรณ์ต่อUSBเพื่อไปยังSerial

  3.CPU
  
  4.Adapter

  5.Relay

  6.หลอดLED
  
## วิธีทำการทดลอง 

  1.นำAdaptorที่ต่อกับLEDแล้ว เชื่อมต่อเข้ากับUSB

  2.เสียบไมโครคอนโทรเลอร์เข้ากับSerial
  
  3.เปิดโปรแกรมตัวอย่างโดยการเปิดcommand promptหลังจากติดตั้งโปรแกรมgit แล้วเขียนโปรแกรม

      #include <ESP8266WiFi.h>
      //#include <WiFiClient.h>
      #include <ESP8266WebServer.h>

      const char* ssid = "Phetkacha5G";
      const char* password = "Whyuwanttoknowthat";

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
      #include <Arduino.h>
      #include <ESP8266WiFi.h>

      int cnt = 0;

      void setup()
      {
    	Serial.begin(115200);
    	pinMode(0, OUTPUT);
	    Serial.println("\n\n\n");
      }

       void loop()
    {
      	cnt++;
      	if(cnt % 2) {
		    Serial.println("========== ON ===========");
	    	digitalWrite(0, HIGH);
	      } else {
		    Serial.println("========== OFF ===========");
		    digitalWrite(0, LOW);
	   }
      	delay(500);
     } 

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
    
    
  4. จากนั้นทำการค้นหาสัญญาณWifi ที่เราสร้างขึ้น
  
## บันทึกผลการทดลอง

หากมีการเชื่อมต่อสัญญาณWIfi หลอดไฟLEDจะกระพริบ
หากไม่มีการเชื่อมต่อสัญญาณWIfi หลอดไฟLEDจะไม่ทำงาน

## อภิปรายผลการทดลอง

การทดลองที่เขียนขึ้น เป็นเพียงความคาดหวังของผู้ทำการทดลอง ยังไม่มีการทดลองจริงแต่ออย่างใด ซึ่งขั้้นตอนอาจมีการเปลี่ยนแปลงให้ถูกต้องมากยิ่งขึ้น หากมีอุปกรณ์ที่พร้อมสำหรับการทำการทดลอง

## คำถามหลังการทดลอง

หากการทดลองนี้สำเร็จ จะส่งผลดีต่อผู้ใช้อย่างไร
	
	ผู้ใช้จะสามารถทราบได้ว่า สัญญาณWifi ของตนเอง มีการเชื่อมต่อเกิดขึ้นหรือไม่


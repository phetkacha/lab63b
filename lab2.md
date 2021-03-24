# การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ

## วัตถุประสงค์

  1. เพื่อรันโปรแกรมในไมโครคอนโรลเลอร์เพื่อใช้ในการค้นหา wi-fi

## วัสดุอุปกรณ์

  1.CPU
  
  2.เสาอากาศสำหรับรับ wifi
  
  3.อุปกรณ์เชื่อมต่อ USB เข้าไปยัง serial
  
  4.microcontroller ESP-01 ที่มี wifi ในตัวเอง

## แหล่งข้อมูลเพื่อการศึกษา

  วิธีการรันโปรแกรม
  
  https://www.youtube.com/watch?v=yBjab0UNuB8
  
## วิธีทำการทดลอง
  1.เสียบไมโครคอนโทรเลอร์เข้ากับSerial
  
  <img width="447" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 15 12 17" src="https://user-images.githubusercontent.com/80880050/112284353-b9dd6780-8cbb-11eb-992d-5dda2218a117.png">
  
  2.เปิดโปรแกรมตัวอย่างโดยการเปิดcommand promptหลังจากติดตั้งโปรแกรมgit โดยการดูที่ตัวอย่างโปรแกรม ที่โฟลเดอร์ pattani
      
      - พิมพ์ cd pattani เพื่อไปยังโฟลเดอร์

  3.ดู source code program 

      - พิมพ์ vi src/main.cpp ในcommand prompt ให้ได้ดังตัวอย่าง
      #include <Arduino.h>
      #include <ESP8266WiFi.h>

      int cnt = 0;

      void setup()
      {
	           Serial.begin(115200);
	           WiFi.mode(WIFI_STA);
	           WiFi.disconnect();
	           delay(100);
	           Serial.println("\n\n\n");
      }

      void loop()
      {
	            Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
	            int n = WiFi.scanNetworks();
	            if(n == 0) {
		                  Serial.println("NO NETWORK FOUND");
	            } else {
		                  for(int i=0; i<n; i++) {
			                         Serial.print(i + 1);
			                         Serial.print(": ");
			                         Serial.print(WiFi.SSID(i));
			                         Serial.print(" (");
			                         Serial.print(WiFi.RSSI(i));
			                         Serial.println(")");
			                         delay(10);
		                  }
	            }
	            Serial.println("\n\n");
        }
   4. ใช้คำสั่งอัพโหลด เพื่ออัพโหลดโปรแกรม 02_Scan-Wifi เข้าไปยังไมโครคอนโทรลเลอร์
    
     - พิมพ์ pio run -t upload
     - ขณะที่ program กำลังรันข้อมูล เพื่อให้ microcontroller รับโปรแกรมใหม่เข้าไป
          - กดปุ่มสีดำ เพื่อทำให้เกิดการ load
          - กดปุ่มสีแดง เพื่อให้เกิดการ reset 
          
   5.สังเกตและบันทึกผลลัพท์
      
      - พิมพ์ pio device monitor
      
      <img width="984" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 16 49 24" src="https://user-images.githubusercontent.com/80880050/112289492-f069b100-8cc0-11eb-9112-828c1bae877d.png">

# อภิปรายผลการทดลอง
  หากต้องการที่จะดูชื่อและจำนวนสัญญาณwifiที่ค้นพบ สามารถใช้คำสั่ง pio device monitor ได้ หลังจากที่อัพโหลดข้อมูลจาก 02_Scan-wifi แล้ว

# คำถามหลังการทดลอง
  
  ขณะที่ program กำลังรันข้อมูล เพื่อให้ microcontroller รับโปรแกรมใหม่เข้าไป การกดปุ่มสีดำ จะทำให้เกิดอะไรขึ้น
  
  ตอบ  เกิดการ Load
  

      
      
  

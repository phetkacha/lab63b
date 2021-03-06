# การทดลองที่ 3 เรื่อง การเขียนโปรแกรมเอ้าพุทสัญญาณดิจิทัล

## วัตถุประสงค์
  1.เพื่อศึกษาหน้าที่และการทำงานของ Relay และการเขียนโปรแกรมและรันไมโครคอนโทรลเลอร์ขณะต่อกับadapter

  2.เพื่อทำความเข้าใจoutputที่ได้จากการทำการทดลอง
  
## แหล่งข้อมูลเพื่อการศึกษา

  วิธีติดตั้งโปรแกรมgit https://www.youtube.com/watch?v=9aF0upI9Gic
  
  วิธีการทำการทดลอง https://youtu.be/CCnN1WJsXQY , https://youtu.be/6JnhaUILGuw
 
## อุปกรณ์

  1.Adapter

  2.Relay

  3.หลอดLED

  4.อุปกรณ์ต่อUSBเพื่อไปยังSerial

  5.ไมโครคอนโทรเลอร์ (ESP01)
  
## วิธีทำการทดลอง
  
  1.นำAdaptorที่ต่อกับLEDแล้ว เชื่อมต่อเข้ากับUSB

  2.เสียบไมโครคอนโทรเลอร์เข้ากับSerial

<img width="447" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 15 12 17" src="https://user-images.githubusercontent.com/80880050/112293142-64598880-8cc4-11eb-80b2-d6991a64fb81.png">

  3.เปิดโปรแกรมตัวอย่างโดยการเปิดcommand promptหลังจากติดตั้งโปรแกรมgit โดยการดูที่ตัวอย่างโปรแกรม ที่โฟลเดอร์ pattani

    - โฟล์เดอร์PATANIจะแสดงโปรแกรมตัวอย่าง 9 โปรแกรม ไปที่ตัวอย่างที่3 แล้วพิมพ์ cd 03_Output-Port
   <img width="984" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 17 19 40" src="https://user-images.githubusercontent.com/80880050/112293864-2f9a0100-8cc5-11eb-89ea-0997579014d3.png">

  4.ดู source code program โดยทำตามขั้นตอนดังนี้

    - พิมพ์ vi src/main.cpp
    - โปรแกรม นี้ set up serial port ที่ port 0 (output)
    - ใน loop แสดงการวนไปเรื่อยๆ ดังตัวอย่าง

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

  5.ใช้คำสั่งอัพโหลด ในการอัพโหลดโปรแกรม 03_Output-Port ไปในไมโครคอนโทรลเลอร์ โดยทำตามขั้นตอนดังนี้

    - พิมพ์ pio run -t upload
    - ในขณะที่ program กำลังรันข้อมูล เพื่อให้ microcontroller รับโปรแกรมใหม่เข้าไป กดปุ่มสีแดง เพื่อให้เกิดการ reset แล้วสังเกตผลลัพธ์ที่เกิดขึ้น

  6.ต่อ Relay ดข้ากับไมโครคอนโทรลเลอร์เพื่อให้Relayเป็นตัวทำหน้าที่เปิด-ปิดสวิชต์
  
  <img width="464" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 17 33 09" src="https://user-images.githubusercontent.com/80880050/112296003-0da17e00-8cc7-11eb-84ff-969aef56c9a6.png">

  7.ต่อแหล่งจ่ายไฟเข้ากับRelayเพื่อให้สามารถทำงานได้
  
      - ผลที่ได้จะเป็น ไฟสีเขียวสลับกับน้ำเงิน ดังรูป
   <img width="1433" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 17 35 42" src="https://user-images.githubusercontent.com/80880050/112296489-8d2f4d00-8cc7-11eb-847e-929c756896b3.png">

   <img width="1433" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 17 35 48" src="https://user-images.githubusercontent.com/80880050/112296530-9a4c3c00-8cc7-11eb-808f-c9711ab7f5df.png">

## บันทึกผผลการทดลอง

    ถ้านับได้เลขคี่ ไฟจะเป็นสีเขียว ซึ่งไฟติด
    ถ้านับได้เลขคู่ ไฟจะเป็นสีน้ำเงิน ไฟไม่ติด
   
## อภิปรายผลการทดลอง

    หลอดไฟ LED จะสว่างและดับตามคำสั่ง เปิดขปิด
    
    เมื่อต่อRelay เข้ากับไมโครคอนโทรลเลอร์แล้ว ลักษณะการเปิด-ปิด จะสอดคล้องกับcodeที่เราใส่ในโปรแกรม
    
## คำถามหลังการทดลอง

  cnt+++ ในขั้นตอนการทดลองที่4 หมายถึงอะไร มีการทำงานอย่างไร
  
  ตอบ  cnt++ หมายถึง การนับเพิ่มเรื่อยๆ หากcnt%2 แปลว่า ตัวเลขเป็นเลขคี่ ให้ดำเนินการ on หากตัวเลขเป็นเลขคู่ ให้ดำเนินการ off

    
 

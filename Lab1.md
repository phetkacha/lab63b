# การทดลองที่ 1 เรื่อง การเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์
## วัตถุประสงค์
1.เพื่อทดสอบการเขียนโปรแกรมโดยการใช้ไมโครคอนโทรลเลอร์
## แหล่งข้อมูลเพื่อการศึกษา
วิธีติดตั้งโปรแกรมgit
https://www.youtube.com/watch?v=9aF0upI9Gic

platform io คืออะไร
https://youtu.be/APdBR37Ukxg
## อุปกรณ์

1.ไมโครคอนโทรเลอร์ (ESP01)

2.อุปกรณ์ต่อUSBเพื่อไปยังSerial
## วิธีทำการทดลอง
1.เสียบไมโครคอนโทรเลอร์เข้ากับSerial

<img width="447" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 15 12 17" src="https://user-images.githubusercontent.com/80880050/112276452-5818ff80-8cb3-11eb-8833-81fd1c26f0c2.png">

2.เปิดโปรแกรมตัวอย่างโดยการเปิดcommand promptหลังจากติดตั้งโปรแกรมgit 
โดยการดูที่ตัวอย่างโปรแกรม ที่โฟลเดอร์ pattani
  - พิมพ์ cd pattani เพื่อไปยังโฟลเดอร์
  - แสดงโฟลเดอร์ ซึ่งมีโปรแกรมตัวอย่าง 9 โปรแกรม
  - ไปที่ตัวอย่างที่ 1
  - พิมพ์ cd 01_Serial Monitor
  - พิมพ์ vi src/main.cpp

3.กดรันโปรแกรแล้วรอดูผลที่เกิดขึ้น ตัวอย่างหลังการรันโปรแกรม
 
 #include <Arduino.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
}

void loop()
{
	cnt++;
	Serial.printf("PATTANI :%d\n",cnt);
	delay(1000);
}

4.เข้าไปที่ Configuration ใน command prompt แล้วพิมพ์ vi platformio.ini เพื่อแสดงข้อมูล
ตัวอย่างข้อมูลที่แสดง
; IOT for KIDS
;
; By Dr.Choompol Boonmee
; 

[env:exercise01]
platform = espressif8266
board = esp01_1m
framework = arduino
board_build.flash_mode = dout

upload_port = /dev/cu.usbserial-1420
;upload_port = COM3

monitor_port = /dev/cu.usbserial-1420
;monitor_port = COM3
monitor_speed = 115200

5.อัพโหลดโปรแกรม 01_serial monitor เข้าไปยังไมโครคอนโทรเลอร์โดยการใช้คำสั่งอัพโหลด

- พิมพ์ pio run -t upload
- ขณะที่ program กำลังรันข้อมูล เพื่อให้ microcontroller รับโปรแกรมใหม่เข้าไป
    - กดปุ่มสีดำ เพื่อทำให้เกิดการ load
    - กดปุ่มสีแดง เพื่อให้เกิดการ reset
 6.สังเกตและบันทึกผลลัพท์
 
 # วิธีการบันทึกผลการทดลอง
 
คำสั่งและผลลัพธ์ที่แสดง
src/main.cpp = ผลลัพธ์ของโปรแกรมส่วน set up & loop
platformio.ini = ข้อมูลใน configuration file
pio run -t upload = รันข้อมูลในตัวอย่าง
pio device monitor = PATTANIที่เพิ่มขึ้นใน 1 วินาที
การกดปุ่มสีดำ = โปรแกรมถูกโหลด
การกดปุ่มสีแดง = โปรแกรมถูกรีเซ็ต

# อภิปรายผลการทดลอง
- เนื่องจากPlatform io เป็นโปรแกรมที่รวบรวมตัวอย่างการเขียนโปรแกรมจากหลายบริษัท ดังนั้น เราสามารถเขียนโปรแกรมโดยใช้บริษัทที่ต่างกันได้

# คำถามหลังการทดลอง
Platform, Board, Framwork เป็นการแสดงข้อมูลใด ตามลำดับ
ตอบ Platform แสดงถึง เทคโนโลยีของบริษัทผู้ผลิต
    Board แสดงถึง ชื่อบอร์ด
    Framwork แสดงถึง วิธีการเขียนโปรแกรม

 





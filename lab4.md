# การทดลองที่ 4 การเขียนโปรแกรมอินพุทสัญญาณดิจิทัล
## วัตถุประสงค์
  
  1.เพื่อทำการทดลองนำสัญญาณ input จากภายนอกเข้ามาในไมโครคอนโทรลเลอร์
  
  2.เพื่อทำการทดลองใช้sensorในการดูinput/output ของสภาพแวดล้อม

## แหล่งข้อมูลเพื่อการศึกษา

  วิธีติดตั้งโปรแกรมgit https://www.youtube.com/watch?v=9aF0upI9Gic
  วิธีทำการทดลอง https://www.youtube.com/watch?v=nFqoZT26U5k
  
## อุปกรณ์
  
  1.หลอดไฟLED

  2.ไมโครคอนโทรเลอร์ (ESP01)

  3.อุปกรณ์ต่อUSBเพื่อไปยังSerial

  4.CPU

  5.adapter

  6.Light sensor

## วิธีทำการทดลอง

  1.เสียบไมโครคอนโทรเลอร์เข้ากับSerial
 
  2.เปิดโปรแกรมตัวอย่างโดยการเปิดcommand promptหลังจากติดตั้งโปรแกรมgit โดยการดูที่ตัวอย่างโปรแกรม ที่โฟลเดอร์ pattani
      
      - โฟล์เดอร์PATANIจะแสดงโปรแกรมตัวอย่าง 9 โปรแกรม ไปที่ตัวอย่างที่4 แล้วพิมพ์ cd 04_Output-Port
  
  3.Sorce code program จะแบ่งเป็นสองส่วนคือ ส่วนที่เป็น Set up และส่วน Loop จากนั้นทำตามขั้นตอนดังนี้

      - ทำการพิมพ์ vi src/main.cpp จะได้ผลลัพธ์ดังนี้
        
        #include <Arduino.h>
        #include <ESP8266WiFi.h>

        int cnt = 0;

        void setup()
        {
          Serial.begin(115200);
          pinMode(0, INPUT);
          pinMode(2, OUTPUT);
          Serial.println("\n\n\n");
        }
         
         void loop()
        {
          int val = digitalRead(0);
          Serial.printf("======= read %d\n", val);
          if(val==1) {
          digitalWrite(2, LOW);
          } else {
           digitalWrite(2, HIGH);
          }
           delay(100);
        }
      
  4.ใช้คำสั่งอัพโหลด ในการอัพโหลดโปรแกรมเข้าไปในไมโครคอนโทรลเลอร์ โดยทำตามขั้นตอนดังนี้

      - พิมพ์ pio run -t upload
      - ทำการกดปุ่มสีดำ เพื่อให้ทำการอัพโหลด
      - อโปรแกรมถูกอัพโหลดเสร็จสิ้น โปรแกรมจะทำงานโดยการตรวจสอบที่ port 0 ว่ามี input มาหรือไม่
          - ถ้า input เป็น 1 ไฟจะติดที่ port 2
          - ถ้า input เป็น 0 ไฟจะไม่ติด
      - พิมพ์ pio device monitor จะได้ค่าที่เป็น 1 ตลอด ดังภาพ
   ![112141149-86410580-8c07-11eb-8024-c3718b21e5cb](https://user-images.githubusercontent.com/80880050/112304375-ff0b9480-8ccf-11eb-8c6a-783c6dd610b3.jpg)
     
      - สายไฟเส้นสีขาว คือ port 0 ถ้าเอาสายไฟเส้นนี้ไปจิ้มจะมีค่าเป็น 0 Volt ถ้านำสายไฟเส้นสีขาวจิ้มกับช่องที่สายสีดำเสียบอยู่ จะอ่านค่าได้เป็น 0 ทั้งหมด
   ![112145978-9bb92e00-8c0d-11eb-9cfd-d1d932cd2504](https://user-images.githubusercontent.com/80880050/112304291-e7341080-8ccf-11eb-9412-95820614e55e.jpg)
 
      - ปล่อยสายไฟเส้นสีขาวออกจาก ช่องที่มีสายสีดำ output หรือ นำสายไฟสีขาวไปจิ้มที่เส้นสีแดง หรือ HIGH(on) เปลี่ยนกลับเป็น 1
   <img width="1433" alt="ภาพถ่ายหน้าจอ 2564-03-24 เวลา 18 29 01" src="https://user-images.githubusercontent.com/80880050/112303416-d6cf6600-8cce-11eb-92d9-58e35494845a.png">

      - เมื่อกดปุ่มสีดำ ซึ่งปุ่มสีดำต่ออยู่กับ port 0 ส่งผลให้ไฟติด เมื่อปล่อย ไฟจะดับ ดังรูป
   ![112144832-3add2600-8c0c-11eb-86ea-446ec0fa337f](https://user-images.githubusercontent.com/80880050/112304519-2a8e7f00-8cd0-11eb-9791-6615726d6d24.jpg)

   ![112144869-3dd81680-8c0c-11eb-908e-643573ce9f53](https://user-images.githubusercontent.com/80880050/112304760-72ada180-8cd0-11eb-890f-f48e32140a64.jpg)

  5.นำ CPU มาต่อกับ Light Sensor ที่ต่อกับตัวต้านทานแล้ว ดังรูป
  
  ![112153543-f2c30100-8c15-11eb-815a-4ae3df03f124](https://user-images.githubusercontent.com/80880050/112304935-ac7ea800-8cd0-11eb-88f6-6375ab9f45b1.jpg)

      - นำinput เส้นสีขาวต่อเข้ากับ Sensor เมื่อแสงสว่างโดนsensor หลอดไฟLED จะสว่าง ค่า output เป็น0 แต่เมื่อsensor ไม่โดนแสงสว่าง หลอดไฟLED จะดับและค่า output เป็น1 ดังรูป
![112155932-5f3eff80-8c18-11eb-8005-e237aa2f2665](https://user-images.githubusercontent.com/80880050/112306500-70e4dd80-8cd2-11eb-8711-b99ec7f4d025.jpg)
  
![112155944-6108c300-8c18-11eb-81e2-777c84f642a9](https://user-images.githubusercontent.com/80880050/112307008-02ece600-8cd3-11eb-95fc-bda492e8d995.jpg)

## บันทึกผลการทดลอง

   - ก่อนทำการต่อ Light Sensor
      
      สายสีขาว จิ้ม สายสีดำ ค่าที่อ่านได้คือ0 ทำให้ไฟติด
      
      สายสีขาว นำออกจากช่อง สายสีดำ	ค่าที่อ่านได้คือ1 ทำให้ไฟดับ
      
      สายสีขาว จิ้ม สายสีแดง	ค่าที่อ่านได้คือ1	ทำให้ไฟดับ
      
      กดปุ่มสีดำ	ค่าที่อ่านได้คือ0	ทำให้ไฟติด
    
      ปล่อยมือจากปุ่มสีดำ	ค่าที่อ่านได้คือ1	ทำให้ไฟดับ
      
   - หลังต่อ Light Sensor
   
      เมื่อsensorไม่ถูกบัง	ค่าที่อ่านได้คือ0	ทำให้ไฟติด
      
      เมื่อsensorถูกบัง	ค่าที่อ่านได้คือ1	ทำให้ไฟไม่ติด
      
 ## อภิปรายผลการทดลอง
 
    - เมื่อทำการต่อ sensorแสง หากตัวsensorถูกบดบัง ค่าจะถูกอ่านเป็น 1 หลอดไฟจะดับ ในขณะเดียวกัน เมื่อsensorแสงไม่ถูกบัง หลอดไฟจะสว่าง
    - เมื่อโค้ดที่ถูกอ่านมีค่าเป็น 0 หมายถึง หลอดไฟจะสว่าง ในขณะเดียวกัน เมื่อค่าที่ถูกอ่านเป็น 1 หลอดไฟจะดับ

## คำถามหลังการทดลอง

  จงยกตัวอย่างการนำlight sensor ไปใช้งานในชีวิตประจำวัน
  
  ตอบ  ไฟอัตโนมัติตามถนน

  
            
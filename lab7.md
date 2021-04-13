# การทดลองที่ 7 การใช้LEDควบคุมการค้นหาไวไฟแอคเซสพอยต์

## วัตถุประสงค์
1. เพื่อนำความรู้ที่ได้จากการเรียนแลปทั้ง 6 แลป มาพัฒนาต่อเป็นโปรแกรมของตัวเองได้

## อุปกรณ์ที่ใช้
1. Adapter
2. หลอดไฟ LED
3. microcontroller ESP-01
4. 2-Port Serial USB
5. Wifi

## แหล่งข้อมูลเพื่อการศึกษา
- หาที่อยู่ IP adress 
  - https://www.sony.co.th/th/electronics/support/articles/00022321

  - แลป 1 https://www.youtube.com/watch?v=NLIUsWLEpmg
  - แลป 2 https://www.youtube.com/watch?v=yBjab0UNuB8
  - แลป 3 https://www.youtube.com/watch?v=CCnN1WJsXQY และ https://www.youtube.com/watch?v=6JnhaUILGuw
  - แลป 4 https://www.youtube.com/watch?v=nFqoZT26U5k
  - แลป 5 https://www.youtube.com/watch?v=VX-QNQcO-b4
  - แลป 6 https://www.youtube.com/watch?v=T26DVHePlTs

- source code 
  - https://github.com/choompol-boonmee/lab63b/tree/master/examples

## วิธีการทำการทดลอง
1. เริ่มเขียนโปรแกรมบน microcontroller ก่อนโดยเสียบ microcontroller เข้าทาง serial port ของ USB 

![image](https://user-images.githubusercontent.com/80879966/112019858-6dcadf80-8b62-11eb-8370-cc9b002280f5.jpg)

2. รันตัวอย่างโปรแกรม จากโฟลเดอร์ pattani และตรวจสอบ source code program 
- พิมพ์ vi src/main.cpp
ข้อมูลมี 2 ส่วน คือ 
 - ส่วนของ set up
   - มี port 2 อัน port 0 (สายสีขาว) เป็น input และ port 2 (สายสีเหลือง) เป็น output
 - ส่วนของ loop หากค่าที่อ่านได้ เป็น 1 ให้ HIGH ไปที่ port 2 (หลอดไฟติด) และถ้าค่าที่อ่านได้ เป็น 0 ให้ LOW ไปที่ port 2 (หลอดไฟดับ)

#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "beamderland";
const char* password = "mumumu26";

IPAddress local_ip(160, 21, 10, 15);
IPAddress gateway(162, 21, 10, 1);
IPAddress subnet(255, 255, 255, 244);

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);
	
	pinMode(0, INPUT);
 	pinMode(2, OUTPUT);
 	Serial.println("\n\n\n");
	
		WiFi.softAP(ssid, password);
		WiFi.softAPConfig(local_ip, gateway, subnet);
		delay(1000);

		server.onNotFound([]() {
			server.send(404, "text/plain", "ERROR! Path Not Found");
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
int val = digitalRead(1);
 Serial.printf("======= read %d\n", val);
 if(val==1) {
  digitalWrite(2, HIGH);
 } else {
  digitalWrite(2, LOW);
 }
 delay(2000);
 server.handleClient();
}


3.จากนั้นเข้าไปที่ configuration file ใน program พิมพ์ vi platformio.ini เพื่อแสดงข้อมูลต่าง เช่น platform ที่มา , board เป็นต้น
4.อัพโหลดโปรแกรม 07_Sensor-wifi เข้าไปยัง microcontroller โดยใช้คำสั่ง upload ขณะที่ program กำลังรันข้อมูล กดปุ่มสีดำ เพื่อทำให้เกิดการ load และกดปุ่มสีแดง เพื่อให้เกิดการ reset
 - เมื่อโปรแกรมถูกอัพโหลดเสร็จสิ้น โปรแกรมจะทำงานโดยการตรวจสอบที่ port 0 ว่ามี input มาหรือไม่ ถ้า input เป็น 1 ไฟจะติดที่ port 2 ถ้า input เป็น 0 ไฟจะไม่ติด
5. ใช้โทรศัพท์มือถือค้นหา wifi ในกรณีที่ input เป็น 1

## การบันทึกผลการทดลอง 
  จากการทดลอง ได้ทำการเปลี่ยนcode program โดยข้อมูลที่เปลี่ยนคือชื่อและรหัสผ่านของwifi ที่อยู่ไอพี , gateway และ subnet ให้เป็นที่อยู่ปัจจุบัน ซึ่งทำการค้นหาใน control panel นอกจากนี้ยังได้ทำการเพิ่มหลอดไฟ LED ที่จะสว่างเมื่อมีการเชื่อมต่อ port ต่างๆเข้าด้วยกัน และยังทำการเปลี่ยน input เมื่อเป็น 1 ไฟจะติด และเริ่มค้นหาสัญญาณ wifi ที่เราสร้างขึ้น

## อภิปรายผลการทดลอง 
  เนื่องจากสถานการณ์ปัจจุบันทำให้ code ที่สร้างขึ้นนี้อาจทำงานได้ไม่เต็มประสิทธิภาพ แต่เราก็ยังสามารถเขียนโปรแกรมเบื้องต้นเกี่ยวกับการประยุกต์ใช้การสร้าง wifi และ การเชื่อมต่อหลอดไฟ LED ดังการทดลองที่ 7 นี้ได้

## คำถามหลังการทดลอง 
ส่วนไหนที่แสดงชื่อของ wifi

*answer* const char* ssid = "beamderland";

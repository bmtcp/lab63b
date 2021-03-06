# การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)

## วัตถุประสงค์
1.เพื่อเพิ่มความเข้าใจในการเขียนโปรแกรมสร้าง Wifi Access Point และสามารถนำไปใช้กับอุปกรณ์ของตัวเองได้

## อุปกรณ์ที่ใช้
1. Microcontroller
2. 2-Port Serial USB 

## ข้อมูลเบื้องต้น
[https://youtu.be/T26DVHePlTs](https://youtu.be/T26DVHePlTs)

## วิธีการทำการทดลอง
1. ติดตั้งเชื่อมไมโครคอนโทรเลอร์ และ USB 
2. กำหนดชื่อ และ password ของ Wifi ที่ต้องการเชื่อม
3. กำหนด IPAdress ,gateway และ subnet

![image](https://user-images.githubusercontent.com/80880311/112317696-e656ab00-8cde-11eb-8048-1e9cabed4eec.jpeg)

4. เตรียม web server ,softAP(ssid, password)

![image](https://user-images.githubusercontent.com/80880311/112317742-f078a980-8cde-11eb-82ae-6661d133f63c.jpeg)

5. Upload โปรแกรมไปยังไมโครคอนโทรเลอร์ใช้คำสั่ง pio run -t upload
6. ขณะโปรแกรมเริ่มรัน กดปุ่มสีดำบนตัวไมโครคอนโทรเลอร์ port 0 และ Reset เพื่อรับข้อมูล
7. เมื่อโปรแกรมโหลดเสร็จ ให้ใช้คำสั่ง pio device monitor แสดงผลจากไมโครคอนโทรเลอร์
8. ลองใช่อุปกรณ์ของตัวเองค้นหา Wifi

![image](https://user-images.githubusercontent.com/80880311/112317789-fa9aa800-8cde-11eb-9ae0-0b82b654dffc.png)

## การบันทึกผลการทดลอง
เมื่อโปรแกรมโหลดเสร็จ ใช่คำสั่ง pio device monitor และลองค้นหาสัญญาณ Wifi จะพบว่า อุปกรณ์สามารถตรวจจับสัญญาณดังรูป

## อภิปรายผลการทดลอง
จากการทดลองที่ 6 นี้จะเห็นว่าเราสามารถสร้างเครือข่ายสัญญาณ Wifi ของตัวเองขึ้นมาเพื่อนใช้กับอุปกรณ์ของตัวเองได้ โดยการรันโปรแกรมตามการทดลองที่ 6 นี้

## คำถามหลังการทดลอง
จากการศึกษาการทดลองดังกล่าวถ้ากำหนดค่า IP ต่างๆไม่ครบ จะต้องทำการ Reset ไมโครคอนโทรเลอร์ใหม่หรือไม่

*answer* ไม่จำเป็นเพราะยังไม่ได้ upload โปรแกรมไปยังไมโครคอนโทรเลอร์

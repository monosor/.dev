# ตัวเลข และชุดอักขระ

## ตัวเลข

ตัวเลขของภาษา Ruby มีสองแบบหลักๆ คือจำนวนเต็ม และแบบมีทศนิยม

จำนวนเต็มจะเรียกว่า **Integer** หรือ **Fixed** เช่น `0`, `112`, `-256`

เลขทศนิยมจะเรียกว่า **Float** หรือ **Double** หรือ **Decimal** เช่น `3.5`, `100.0`

การคำนวนด้วยตัวเลขจะใช้ตัว `+` แทนการบวก `-` แทนการลบ `*` แทนการคูณ และ `/` แทนการหาร 

![&#xE17;&#xE14;&#xE25;&#xE2D;&#xE07;&#xE23;&#xE31;&#xE19;&#xE1A;&#xE19; irb](../../.gitbook/assets/image%20%2834%29.png)

![&#xE17;&#xE14;&#xE25;&#xE2D;&#xE07;&#xE23;&#xE31;&#xE19;&#xE14;&#xE49;&#xE27;&#xE22;&#xE40;&#xE27;&#xE47;&#xE1A; repl.it](../../.gitbook/assets/image%20%2835%29.png)

ถ้ารันบน repl.it แล้วไม่เห็นบน ให้ใส่ `puts` เพื่อพิมพ์ค่าออกมาใน Console \(ช่องทางขวาสีดำๆ\) แต่ถ้ารันใน irb ซึ่งจะรันโค้ดเราทีละบรรทัด ไม่ต้องใส่ `puts` ก็ได้

การพิมพ์คำสั่งในการคำนวณเลข จะเว้นวรรค \(Space\) ระหว่างตัวเลขและสัญลักษณ์อย่างไรก็ได้ ดังภาพ \(แต่ต้องเว้นวรรคกับคำสั่ง `puts` มิเช่นนั้นโปรแกรมจะทำงานผิดพลาด \(Error\)

![puts4+5 &#xE08;&#xE30; Error &#xE40;&#xE1E;&#xE23;&#xE32;&#xE30;&#xE40;&#xE25;&#xE02; 4 &#xE2D;&#xE22;&#xE39;&#xE48;&#xE15;&#xE34;&#xE14;&#xE01;&#xE31;&#xE1A;&#xE04;&#xE33;&#xE2A;&#xE31;&#xE48;&#xE07; puts](../../.gitbook/assets/image%20%2828%29.png)

### ลำดับการคำนวณเลข

การคำนวณเลขจะมีมากกว่า 2 พจน์ก็ได้ แต่ลำดับการคำนวณจะมีลำดับขั้นอยู่ โดยตัวคูณและหารจะทำก่อนบวกและลบเสมอ ยกเว้นจะใช้วงเล็บ `( )` ในการกำกับ โปรแกรมจะคำนวณภายในวงเล็บก่อน

![&#xE25;&#xE2D;&#xE07;&#xE04;&#xE34;&#xE14;&#xE15;&#xE32;&#xE21;&#xE14;&#xE39; &#xE27;&#xE48;&#xE32;&#xE44;&#xE14;&#xE49;&#xE15;&#xE23;&#xE07;&#xE01;&#xE31;&#xE1A;&#xE17;&#xE35;&#xE48;&#xE04;&#xE34;&#xE14;&#xE44;&#xE27;&#xE49;&#xE2B;&#xE23;&#xE37;&#xE2D;&#xE44;&#xE21;&#xE48;](../../.gitbook/assets/image%20%2832%29.png)

### การหารเลขจำนวนเต็ม

สำหรับการหารในเลขจำนวนเต็มนั้น ถ้ามีเศษ **เศษจะถูกปัดทิ้งเสมอ**

![5 / 2 = 2.5 -&amp;gt; &#xE1B;&#xE31;&#xE14;&#xE40;&#xE28;&#xE29;&#xE17;&#xE34;&#xE49;&#xE07;&#xE40;&#xE2B;&#xE25;&#xE37;&#xE2D; 2](../../.gitbook/assets/image%20%2833%29.png)

### เลขทศนิยม

สำหรับเลขทศนิยมจะคำนวณได้เหมือนกับจำนวนเต็มทุกอย่าง โดยจะใช้คำนวณผสมกับจำนวนเต็มก็ได้ แต่ค่าที่ได้จะกลายเป็นทศนิยมไปด้วย

![&#xE01;&#xE32;&#xE23;&#xE04;&#xE33;&#xE19;&#xE27;&#xE13;&#xE01;&#xE31;&#xE1A;&#xE40;&#xE25;&#xE02;&#xE17;&#xE28;&#xE19;&#xE34;&#xE22;&#xE21;](../../.gitbook/assets/image%20%2831%29.png)

### การแปลงประเภทของตัวเลข

เราสามารถแปลงจาก Integer เป็น Float หรือ Float เป็น Integer ได้ด้วยคำสั่ง `.to_f` และ `.to_i` ตามลำดับ \(หากแปลงจาก Float เป็น Integer เศษทศนิยมจะถูกปัดทิ้งเช่นเดียวกับการหาร\)

![&#xE15;&#xE31;&#xE27;&#xE2D;&#xE22;&#xE48;&#xE32;&#xE07;&#xE01;&#xE32;&#xE23;&#xE41;&#xE1B;&#xE25;&#xE07;&#xE14;&#xE49;&#xE27;&#xE22; .to\_f &#xE40;&#xE1B;&#xE47;&#xE19; Float &#xE41;&#xE25;&#xE30; to\_i &#xE40;&#xE1B;&#xE47;&#xE19; Integer](../../.gitbook/assets/image%20%2826%29.png)

## ชุดอักขระ

ชุดอักขระ หรือภาษาอังกฤษจะเรียกว่า String \(สตริง\) เป็นชุดของตัวหนังสือนั่นเอง \(โดยในภาษาอื่นๆ อาจมีเป็นตัวอักระตัวเดียวหรือ Character ด้วย แต่ใน Ruby จะมีแต่ String อย่างเดียว\)

วิธีสร้าง String ก็ง่ายๆ ให้ครอบคำด้วยเครื่องหมายคำพูด แบบ Single Quote `' '` หรือ Double Quote `" "` ก็ได้

![&#xE2A;&#xE23;&#xE49;&#xE32;&#xE07; String &#xE14;&#xE49;&#xE27;&#xE22;&#xE01;&#xE32;&#xE23;&#xE04;&#xE23;&#xE2D;&#xE1A;&#xE14;&#xE49;&#xE27;&#xE22; &apos; &#xE2B;&#xE23;&#xE37;&#xE2D; &quot;](../../.gitbook/assets/image%20%2830%29.png)

### แถม : ปั๊ม String ด้วยการคูณ

ในภาษา Ruby นั้นเราสามารถเอาตัวเลขไปคูณกับ String ได้! \(แต่ต้องเอาตัวเลขไว้ด้านหลังเท่านั้นนะ\)

![](../../.gitbook/assets/image%20%2829%29.png)

ในตอนหน้าเราจะมาเล่นกับ String กันต่อ โดยจะมีเรื่องของ Method ด้วย


# Boolean

**Boolean \(บูเลียน\)** ถึอว่าเป็นข้อมูลพื้นฐานที่สำคัญมากในการเขียนโปรแกรม เนื่องจากจะทำให้โปรแกรมนั้นมีการ "ตัดสินใจ" ได้จากเงื่อนไขที่เราสร้างขึ้น

Boolean จะมีค่าเพียง 2 แบบ คือ จริง `true` และเท็จ `false` ในภาษา Ruby นั้นจะเขียนเป็นตัวพิมพ์เล็ก

{% hint style="info" %}
เพราะฉะนั้น เราจึงไม่สามารถตั้งชื่อตัวแปรเป็น `true` หรือ `false` ได้ เพราะว่าภาษาได้ทำการ "จอง" ชื่อนี้ไปแล้ว เรียกว่าเป็น **Reserved Keywords** ที่เราจะเอามาใช้เป็นชื่อของตัวแปรไม่ได้นั่นเอง

ดู Reserved Keywords ทั้งหมดได้ที่นี่ [https://ruby-doc.org/core-3.0.0/doc/keywords\_rdoc.html](https://ruby-doc.org/core-3.0.0/doc/keywords_rdoc.html)
{% endhint %}

{% embed url="https://repl.it/@narze/boolean-basic?lite=true" caption="การใช้ Boolean และการสร้างตัวแปรให้มีค่าเป็น Boolean" %}

## Boolean Expression

Boolean Expression \(นิพจน์บูเลียน\) เป็นการสร้างค่า Boolean จากการเขียนโค้ดให้เป็น Expression ต่างๆ ในที่นี้จะขอยกตัวอย่างนิพจน์ทางคณิตศาสตร์ \(สมการ\) ก่อน อาทิเช่น

* `10 > 5` ใช้เครื่องหมาย "มากกว่า" `>` 
  * เหมือนกับการตั้งคำถามว่า "10 มากกว่า 5 หรือเปล่า?" ซึ่งคำตอบคือ จริง ฉะนั้นผลของ Expression นี้คือ  `true`
* `10 < 5` ใช้เครื่องหมาย "น้อยกว่า" `<`
  * เหมือนกับการตั้งคำถามว่า "10 น้อย 5 หรือเปล่า?" ซึ่งคำตอบคือ เท็จ ฉะนั้นผลของ Expression นี้คือ `false`
* `a <= 5` ใช้เครื่องหมาย "น้อยกว่า**หรือ**เท่ากับ" `<=`
  * Expression สามารถใช้คู่กับตัวแปรได้
  * ถ้า `a` มีค่าน้อยกว่าหรือเท่ากับ `5` เช่น 0, 5, -100 ผลของ Expression นี้คือ `true`
  * ถ้า `a` มีค่าไม่น้อยกว่าหรือเท่ากับ `5` \(มากกว่า\) เช่น 6, 1000, 5.1 ผลของ Expression นี้คือ `false`
  * ถ้า `a` เป็นข้อมูลประเภทอื่นที่ไม่ใช้ตัวเลข \(เช่น String\) โปรแกรมจะทำงานไม่ได้ \(Error\)
* `7 >= b` ใช้เครื่องหมาย "มากกว่า**หรือ**เท่ากับ" `>=`
  * ตัวแปรจะอยู่ด้านไหนของ Expression ก็ได้ หรือจะท้ังสองด้านก็ได้
  * ถ้า `7` มีค่ามากกว่าหรือเท่ากับ `b` เช่น `b` เป็น 7, 6, 5, ... ผลของ Expression นี้คือ `true`
  * ถ้า `7` มีค่าไม่มากกว่าหรือเท่ากับ `b` \(น้อยกว่า\) เช่น `b` เป็น 8, 9, 10, ... ผลของ Expression นี้คือ `false`
* `a == b`ใช้เครื่องหมายเท่ากับสองตัว เพื่อเทียบว่ามีค่าเท่ากันหรือเปล่า
  * ถ้าค่าท้ังสองด้านเท่ากัน ผลของ Expression นี้คือ `true`
  * ถ้าค่าท้ังสองด้านไม่เท่ากัน ผลของ Expression นี้คือ `false`
* `a != b`ใช้เครื่องหมายอัศเจรีย์ `!`ตามด้วยเท่ากับ เพี่อเทียบว่ามีค่า**ไม่**เท่ากันหรือเปล่า \(ตรงข้ามกับ `==`\)
  * ถ้าค่าท้ังสองด้านไม่เท่ากัน ผลของ Expression นี้คือ `true`
  * ถ้าค่าท้ังสองด้านเท่ากัน ผลของ Expression นี้คือ `false`

{% hint style="info" %}
เหตุผลที่ Expression "เท่ากับ" ต้องใช้เครื่องหมายเท่ากับสองตัว เพราะว่าการใช้เครื่องหมายเท่ากับตัวเดียว แสดงถึง**การกำหนดค่าให้กับตัวแปร**

* `a = 1` หมายถึง กำหนดให้ตัวแปร `a` มีค่าเป็น `1`
* `a == 1` หมายถึง การถามว่า `a` มีค่าเท่ากับ `1` หรือไม่
{% endhint %}

นิพจน์ที่เป็นการเทียบว่าค่าเท่ากัน หรือไม่เท่ากัน สามารถใช้กับประเภทข้อมูลอื่นนอกจากตัวเลขได้ด้วย

* String : `name == "monosor"` เป็นการเช็คว่าตัวแปร `name` มีค่าเป็น `"monosor"` หรือไม่
* Boolean : `is_admin == false` เป็นการเช็คว่าตัวแปร `is_admin` มีค่าเป็น `false` หรือไม่
* Nil : `value == nil` เป็นการเช็คว่าตัวแปร `value` มีค่าเป็น `nil` หรือไม่

{% embed url="https://repl.it/@narze/boolean-expressions?lite=true" caption="ตัวอย่าง Boolean Expression" %}

### นิเสธ \(Negation\)

ใช้เครื่องหมายอัศเจรีย์ด้านหน้าตัวแปร หรือ Expression เพื่อแปลงค่าความจริงไปเป็นตรงกันข้าม \(จาก `true` เป็น `false` และ `false` กลายเป็น `true`\)

{% embed url="https://repl.it/@narze/boolean-negation?lite=true" %}






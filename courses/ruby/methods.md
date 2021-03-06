# เมธอด

ในบทที่แล้ว เรามีการแนะนำเรื่องชุดอักขระ หรือ String \(สตริง\) นั่นคือชุดของตัวอักขระ ที่จะครอบด้วย `" "` หรือ `' '` เพื่อใช้ในการแสดงผลคำต่างๆ นั่นเอง

ในบทนี้เราจะมาเรียนรู้กันถึงเมธอด และการใช้เมธอดของสตริงกัน

## เมธอด \(Method\)

หากแปลตรงๆ คำนี้จะแปลว่า "วิธีการ" แต่ว่าในโลกของการเขียนโค้ดนั้น เมธอดจะเป็น "ชุดคำสั่ง" ที่เราสามารถกระทำการต่างๆ กับโปรแกรม หรือข้อมูลได้

> บางครั้งอาจเรียกว่า "ฟังก์ชั่น" \(Function\) ในการเรียนขั้นพื้นฐานนี้ จะถือว่าเป็นสิ่งเดียวกันก็ได้ครับ

การเรียกใช้เมธอดนั้น จะอยู่ในรูปแบบของตัวจุด `.` แล้วตามด้วยชื่อของเมธอดนั้น \(ในบทที่แล้วเราจะเห็น `.to_f`, `.to_i` ซึ่งก็เป็นเมธอดเช่นกัน\) ซึ่งในการเขียนภาษา Ruby เราจะมีเมธอดต่างๆ ให้เราเลือกใช้มากมาย

## ตัวอย่างเมธอดของสตริง

เมธอดของสตริง หมายถึงชุดคำสั่งที่สามารถแปลงค่าของสตริง ให้เป็นอย่างอื่นได้

### แปลงตัวพิมพ์เล็กเป็นตัวพิมพ์ใหญ่ ด้วย upcase

ใช้เมธอด `.upcase` เพื่อแปลงสตริงเป็นตัวพิมพ์ใหญ่ทั้งหมด

{% embed url="https://repl.it/@narze/string-and-methods-upcase?lite=true" caption="upcase แปลงสตริงเป็นตัวพิมพ์ใหญ่" %}

### แปลงตัวพิมพ์ใหญ่เป็นตัวพิมพ์เล็ก ด้วย downcase

ในทางกลับกัน ถ้าอยากได้ตัวพิมพ์เล็กทั้งหมด ก็เปลี่ยนเป็น `.downcase` แทน

{% embed url="https://repl.it/@narze/string-and-methods-downcase?lite=true" caption="downcase แปลงสตริงเป็นตัวพิมพ์เล็ก" %}

### กลับหัวกลับหางสตริง ด้วย reverse

ใช้ `.reverse` เพื่อกับด้านสตริง \(ตัวแรกจะเป็นตัวสุดท้าย ไล่กลับมาเรื่อยๆ\)

{% embed url="https://repl.it/@narze/string-and-methods-reverse?lite=true" caption="reverse กลับด้านสตริง" %}

## วงเล็บหายไปไหน? 🧐

หากเคยใช้งานภาษาเขียนโปรแกรมอื่นๆ มา อาจสงสัยว่า ทำไมการเรียกใช้เมธอดถึงไม่มีวงเล็บ `()` ด้านหลังชื่อเมธอดล่ะ คำตอบก็คือ เพื่อความสวยงามนั่นเอง

จริงๆ แล้วจะใส่ก็ได้นะ แต่เขาไม่นิยมใช้กัน ถ้าไม่จำเป็น

{% embed url="https://repl.it/@narze/string-and-methods-parentheses?lite=true" caption="ใส่วงเล็บหลังเมธอด หรือไม่ใส่ก็ได้ ค่าเท่ากัน" %}

## การต่อเมธอด \(Method Chaining\)

เราสามารถที่จะนำเมธอดมาต่อกันได้ เช่นถ้าเราต้องการแปลงให้เป็นตัวพิมพ์ใหญ่ และกลับด้านสตริงไปพร้อมๆ กัน ก็ให้พิมพ์เมธอดต่อท้ายกันได้เลย

{% embed url="https://repl.it/@narze/string-and-methods-chaining?lite=true" caption="การนำเมธอดมาต่อกัน \(.reverse.reverse คือกลับด้านสองครั้ง จึงได้ค่ากลับมาเหมือนเดิม\)" %}

เมธอดของสตริงนั้น[ยังมีอีกมากมาย](https://docs.ruby-lang.org/en/3.0.0/String.html) และของข้อมูลประเภทอื่นๆ ก็ยังมีอีกมาก แต่ในบทต่อไปเราจะแนะนำการสร้างและใช้งานตัวแปร พร้อมกับรู้จักข้อมูลพื้นฐานประเภทอื่นๆ กันให้ครบก่อน


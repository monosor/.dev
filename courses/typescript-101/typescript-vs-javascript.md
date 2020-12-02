# TypeScript vs JavaScript

[Ben Awad](https://www.youtube.com/channel/UC-8QAzbLcRglXeN_MY9blyw) ได้กล่าวเอาไว้ว่า

> ## JavaScript คือ Web Dev แบบ Hardcore Mode

{% embed url="https://www.youtube.com/watch?v=bAB\_nNf8-a0" %}

เนื่องจาก JavaScript เป็นภาษาที่มีความยืดหยุ่นสูง ใช้ง่าย เขียนได้หลากหลายท่า หลายรูปแบบมากๆ สามารถทำให้นำไปต่อยอดเป็น Concept, Library, Framework ต่างๆ ได้มากมาย

แต่ด้วยความที่ง่ายของมัน ก็ทำให้**เกิดบั๊กได้ง่ายขึ้น**เช่นกัน

การใช้ TypeScript ร่วมกับ Linter \(Static Code Analysis Tool : เครื่องมือตรวจสอบโค้ด\) อย่าง [ESLint](https://eslint.org/) จะทำให้คนเขียนโค้ดเห็นทันทีเมื่อโค้ดนั้น Violate Rules หรือผิดกฎของ TypeScript ที่ตั้งไว้ เช่น Type ไม่ตรง, สะกด Property ผิด, ลืม `return`

ส่วนตัวคิดว่าหากเขียน JavaScript เป็นในเบื้องต้นแล้ว หรือว่าต้องทำ Project ที่ใหญ่ขึ้นและต้องการให้ Maintenance ได้ง่าย ควรที่จะเริ่มเขียน หรือว่าแปลงโค้ดให้เป็น TypeScript เท่าที่จะทำได้ เพราะว่า Tooling ในฝั่งของ TypeScript นั้นดีมากๆ แม้จะแลกกับ Learning Curve ที่สูงขึ้นหน่อย 

ถ้าไม่ได้ถึงกับเขียน Library เอง คิดว่าเรียนแค่พออ่าน Syntax ได้และใช้ Type, Interface เป็นบ้างก็เพียงพอแล้ว ซึ่งทั้งหมดนี้จะอยู่ภายใน Course นี้


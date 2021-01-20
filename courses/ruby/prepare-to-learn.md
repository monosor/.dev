# เตรียมพร้อมเรียน Ruby

## UPDATE : Interactive Learning

ในบทเรียนใหม่ๆ \(ตั้งแต่บท [เมธอด](methods.md) โค้ดตัวอย่างจะใช้ Repl แบบ Embed ที่ผู้เรียนสามารถทดลองแก้ไขและรันแบบสดๆ บนเว็บนี้ได้เลย โดยการรันสามารถกดปุ่ม ▶️ และดูผลได้จาก Console

{% embed url="https://repl.it/@narze/repl-example" %}

## แบบ Online

ก่อนที่จะเริ่มเรียน Ruby ไปกับเรา สำหรับคอร์สนี้ เราจะให้เขียนโค้ด Ruby จากบนเว็บเป็นหลัก โดยใช้ Online Editor บนเว็บเหล่านี้

* [Try Ruby](https://try.ruby-lang.org/) : ทดลองเขียน Ruby จากบนเว็บได้เลย แต่เมื่อปิดตัวเว็บ โค้ดจะหายไป
* [Online-IDE](https://www.online-ide.com/online_ruby_compiler) : เขียน Ruby แล้วเซฟเป็นไฟล์ `.rb` ลงเครื่องได้ และอัปโหลดโค้ดกลับขึ้นไปเพื่อใช้ต่อได้
* [Repl.it](https://repl.it/languages/ruby) : ตัวนี้จะมีฟังก์ชั่นครบเครื่องที่สุด โค้ดจะเซฟไว้บนเว็บ และ Sync โค้ดกับ GitHub ได้ด้วย แต่ต้องล็อกอินก่อนถ้าจะใช้ฟีเจอร์การเซฟโค้ด

![online-ide](../../.gitbook/assets/image%20%2824%29.png)

![repl.it](../../.gitbook/assets/image%20%2825%29.png)

เพื่อนๆ สามารถเลือกได้ตามความถนัดเลย ข้อดีของการเขียนบนเว็บก็คือจะมีทั้ง Editor ที่ใช้เขียนโค้ด กับ Console ที่แสดงผลโค้ด ในหน้าจอเดียวกัน เมื่อเรากดปุ่ม ▶️ Run \(หรือ Ctrl+Enter หรือ Command+Enter โค้ดก็จะไปรันบน Console ทันที

## แบบ Offline

แต่ถ้าอยากรันโค้ดเองบนเครื่อง ก็จะต้องติดตั้งตัว Ruby ซึ่งวิธีการติดตั้ง Ruby มีหลายแบบมาก [ดูวิธีทั้งหมดจาก Official Document](https://www.ruby-lang.org/en/documentation/installation/) เลือกกันเอาเองตามความสะดวก เราขอแนะนำว่า...

### ใช้ Windows

โหลดและติดตั้ง [RubyInstaller](https://rubyinstaller.org/) 

### ใช้ macOS

ไม่ต้องทำอะไร Ruby มีแถมมาบนเครื่องอยู่แล้ว ถ้าไม่เชี่อลองเปิด Terminal แล้วรัน `ruby -v`

### ใช้ Linux

ติดตั้งผ่าน Package Manager เช่น `apt-get install ruby-full`

### การใช้งาน

การรันโค้ด Ruby จะมีสองแบบ คือแบบ Interactive คือเราพิมพ์โค้ดเข้าไปให้รันทีละบรรทัด ให้ใช้คำสั่ง irb \(Interactive Ruby\)

```text
irb
```

อีกแบบหนึ่งคือสร้างไฟล์นามสกุล `.rb` แล้วใช้ `ruby` ในการรัน

```text
ruby hello.rb
```




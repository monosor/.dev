---
description: ไม่รู้จะแปลไทยยังไงดี...
---

# Literal Types

นอกจาก `interface` แล้ว เรายังสามารถสร้าง Type ใหม่ด้วยคีย์เวิร์ด `type` ได้เช่นกัน โดยความแตกต่างคีอ `interface` ใช้สร้าง Type สำหรับ Object หรือ Class แต่ `type` จะสามารถกำหนดเป็นค่าแบบตรงตัว \(Literal\) ได้เลย

สรุปง่ายๆ ว่ามันคือการประกาศตัวแปรให้เป็น `type` เพื่อที่จะนำไปใช้ต่อ

```typescript
type Hello = string           // ให้ type Hello เป็น string
const a: Hello = "World"      // ใช้งาน type Hello

type Hi = "Hi"                // ให้ type Hi เป็น "Hi" แบบตรงตัว
const b: Hi = "Hi"
const c: Hi = "Hello"         // Error : เพราะค่าต้องเป็น "Hi" แบบตรงตัวเท่านั้น
```

ประโยชน์ของ Literal Type คือเราสามารถใช้ Union `|` ได้ เพื่อกำหนดให้ Type เป็นค่าใดค่าหนึ่ง

```typescript
type Hi = "Hi" | "Hello"     //  type Hi เป็นคำว่า "Hi" หรือ "Hello" ก็ได้

type Dice =                  // type Dice ต้องเป็นเลข 1-6
  | 1                        // เขียนแบบหลายบรรทัด
  | 2 
  | 3 
  | 4 
  | 5 
  | 6
```

หรือจะใช้ Union กับตัว Type อื่นๆ ก็ยังได้

```typescript
type NotNumber = string | boolean | array 
// ต้องมี type string หรือ boolean หรือ array
```

## Literal Narrowing

การต้ังค่าคงที่ `const` นั้นจะทำให้ Type เป็นแบบ Literal ส่วนการตั้งตัวแปรแบบ `let` หรือ `var` นั้นจะเป็น Type แบบปกติ ซึ่งเปลี่ยนค่าได้ เช่น

```typescript
const x = "ABC"    // x มี Type เป็น "ABC" ซึ่งเป็น Literal เพราะใช้ const
x = "DEF"          // ❌ เปลี่ยนค่า x ไม่ได้ เพราะต้องเป็น "ABC" เสมอ

let y = "XYZ"      // y มี Type เป็น string เพราะเปลี่ยนเป็นค่าอื่นได้เนื่องจากใช้ let
y = "ABC"          // ✅ เปลี่ยนค่า y ได้ เพราะยังเป็น string อยู่
```




---
description: Type กับ Interface ต่างกันอย่างไร เมื่อไหร่ควรใช้ตัวไหน?
---

# Type vs Interface

เมื่อได้รู้จักวิธีการสร้าง Type ด้วย `type` กับ `interface` แล้ว อาจมีความสงสัยว่า แล้วมันต่างกันอย่างไร

สำหรับการกำหนดรูปร่างหน้าตาของออปเจกต์นั้น สามารถใช้ได้ทั้ง `type` และ `interface`

```typescript
interface Point {
  x: number
  y: number
}

type Point = {
  x: number
  y: number
}
```

สังเกตว่าการใช้ `interface` จะคล้ายกับการสร้าง Class และการใช้ `type` จะคล้ายการประกาศค่าของตัวแปรโดยใช้ `=` เพราะฉะนั้นหากเป็นกรณีที่ตั้งชื่อให้กับ Type มาตรฐานทั่วไป หรือทำ Literal Types จะไม่สามารถใช้ `interface` ได้

```typescript
type Color = "Yellow" | "Red" // OK

interface Color "Yellow" | "Red" // ❌ ไม่ได้ เพราะไม่ใช่ออบเจกต์
```

นอกจากนี้ยังมีข้ออื่นๆ ที่ `interface` ไม่เหมือนกับ `type` อีก 2-3 เรื่อง [ดูรายละเอียดที่นี่](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

ส่วนเรื่องอะไรควรใช้เมื่อไหร่ จากความเห็นส่วนตัว และประสบการณ์ที่เขียนมา ขอสรุปแบบจำง่ายๆ ตามนี้

> #### ถ้าใช้ `interface` ได้ \(เช่นกำหนดสำหรับ Object, Class\) ก็ใช้ ถ้าทำไม่ได้ค่อยใช้ `type` แทน


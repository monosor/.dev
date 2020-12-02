# Optional Properties

โดยปกติแล้วเมื่อเรากำหนด Interface หรือ Type \(แบบ Object\) แล้ว เมื่อนำไปใช้สร้าง Object ใดๆ ทุก Property จะเป็นแบบ Required คือต้องมีค่านั้นอยู่เสมอ เพื่อการันตีว่า Type จะเป็นตามที่กำหนดไว้เสมอ เช่น

```typescript
interface User {
  username: string
  email: string
}

// หรือ
type User = {
  username: string
  email: string
}

let a: User = {
  username: "foo",
  email: "foo@example.com",
}

let b: User = { // ❌ Type Error : ไม่ได้กำหนด Property 'email'
  username: "bar"
}
```

โค้ดนี้ถ้า Compile เป็น JavaScript ปกติก็จะยังใช้ได้ แต่ถ้าเราเรียก `b.email` จะได้ `undefined` แปลว่าโค้ดนี้จะไม่มีความ Type-safe แล้ว

ถ้าหากเราต้องการทำให้ Property ไม่เป็นแบบ Required ยกตัวอย่างเช่น การสร้าง User Account ใหม่ ไม่จำเป็นต้องกรอกเบอร์โทรศัพท์เสมอไป จะทำได้สองวิธี แบบแรกคือใช้ Union `|` กับ `null`

```typescript
interface User {
  username: string
  phone: string | null
}
```

แต่วิธีนี้จะมีปัญหาว่า เรายังคงต้องกำหนดให้ `phone` เป็น `null` อยู่ดี

```typescript
const user: User = { username: "foo", phone: "0876543210" } // ✅
const user: User = { username: "foo", phone: null }         // ✅
const user: User = { username: "foo" }                      // ❌
```

อีกวิธีหนึ่งคือเราต้องการให้ละ Property ไปเลย จะต้องใช้การกำหนดว่าเป็น Optional โดยใช้ตัว `?` ด้านหลังชื่อ Property ดังนี้

```typescript
interface User {
  username: string
  phone?: string   // ให้ phone เป็น Optional Property
}

const user: User = { username: "foo" } // ✅ ไม่ต้องมี phone ก็ใช้ได้

user.phone // undefined
```

โดยค่าของ `phone` จะเป็น Type ที่เรากำหนดให้ มา Union กับ `undefined`

![phone &#xE21;&#xE35;&#xE04;&#xE48;&#xE32;&#xE40;&#xE1B;&#xE47;&#xE19; string &#xE2B;&#xE23;&#xE37;&#xE2D; undefined](../../.gitbook/assets/image%20%287%29.png)


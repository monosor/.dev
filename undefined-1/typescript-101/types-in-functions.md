# การกำหนด Type ในฟังก์ชั่น

นอกจากการกำหนด Type ให้กับตัวแปรต่างๆ แล้ว ในกรณีของฟังก์ชั่น เราสามารถกำหนด Type ให้กับพารามิเตอร์ และค่าที่จะ Return ได้

### Parameter Type

```typescript
function say(word: string, times: number) {
  [...Array(times).keys()].forEach(() => {
    console.log(word)
  })
}
```

ฟังก์ชั่น `say` มีพารามิเตอร์ 2 ตัว โดยตัวแรก \(`word`\) เป็น String และตัวที่สอง \(`times`\) เป็น Number

```typescript
say("Very Good", 3) // OK

say("กล้ามาก", "เก่งมาก")
// Argument of type 'string' is not assignable to parameter of type 'number'.
```

หมายเหตุ ค่าตัวแปรในฟังก์ชั่นเรียกว่า Parameter แต่ค่าที่ส่งเข้าไปตอนเรียกฟังก์ชั่นเรียกว่า Argument

### Return Type

เป็นการกำหนดว่า ค่าที่ส่งกลับมาจากฟังก์ชั่นจะเป็น Type ใด \(ในตัวอย่างขอละ Parameter Type เพื่อความเข้าใจง่าย\) โดยการกำหนด Return type จะเติมเข้าไปด้านหลัง Parameter ทั้งหมด

```typescript
function sum(a, b): number {
  return a + b
}
```

หรือในกรณีที่เขียนเป็น Arrow Function จะไว้หลัง Parameter เช่นกัน แต่อยู่ด้านหน้าของ `=>`

```typescript
const sum = (a, b): number => {
  return a + b
}

// แบบ One-liner
const sum = (a, b): number => a + b
```

ในกรณีที่ฟังก์ชั่นไม่คืนค่าเลย ให้ใช้ `void`

```typescript
function say(word, times): void {
  [...Array(times).keys()].forEach(() => {
    console.log(word)
  })
}
```

และอีกกรณีที่พบบ่อย คือฟังก์ชั่นที่เป็น Asynchronous ที่มีคีย์เวิร์ด `async` เราจะต้อง Return `Promise<>` โดยห่อค่าที่จะคืนเอาไว้ เช่นการเรียกใช้ API

```typescript
const fetchUser = async (url: string): Promise<User> => { // ไม่ใช้ User เฉยๆ
  const response = await fetch(url)
  const { data } = await response.json()
  return data
}
```

User คือ Interface ที่กำหนดขึ้นมาเอง ซึ่งจะอธิบายถึงวิธีในการสร้าง Interface ในบทต่อไป


# Generics ขั้นพื้นฐาน

Generics นั้นเป็นคอนเซ็ปท์ที่มีในหลายๆ ภาษาที่เป็น Static Typing อยู่แล้ว เพราะมันทำให้เราสามารถเขียนโค้ดให้ใช้งานซำ้ได้ในหลายๆ Type ขอยกตัวอย่างจากฟังก์ชั่น JavaScript นี้ ที่จะคืนค่าแรกภายใน Array

```javascript
// JavaScript
function getFirst(arr) {
  return arr[0]
}

getFirst([1, 2, 3]) // 1
getFirst(["One", "Two", "Three", "Four", "Five"]) // "One"
```

ลองสังเกตว่า ฟังก์ชั่นนี้รองรับ Array ของ Type ใดก็ได้ ถ้าเรากำหนด Type เฉพาะเจาะจงว่าเป็น `number` หรือ `integer` จะใช้กับอีกตัวไม่ได้ เช่น

```typescript
// TypeScript
function getFirst(arr: number[]): number {
  return arr[0]
}

getFirst([1, 2, 3]) // 1
getFirst(["One", "Two", "Three", "Four", "Five"]) // Type Error
```

เราอาจใช้ `any[]` แทนได้ แต่การคืนค่า `any` ออกมา ไม่ใช่เรื่องที่ดี เพราะจะเสียความ Type-safe ไป

```typescript
function getFirst(arr: any[]): any {
  return arr[0]
}

const a = getFirst([1, 2, 3])                               // a: any
const b = getFirst(["One", "Two", "Three", "Four", "Five"]) // b: any
```

การใช้ Generic จะทำให้เรา "จับ" \(Capture\) Type ที่โยนเข้าไปในฟังก์ชั่น ให้เหมือนกับค่าที่จะ Return ออกมา โดยการใช้สัญลักษณ์ `<T>` แล้วนำค่า `T` ไปใช้ต่อเป็นพารามิเตอร์ หรือค่า Return ได้ และเราจะเรียก `T` ว่าเป็นตัวแปรแบบ "Type Variable" \(ไม่ได้บังคับว่าต้องเป็นตัว T สามารถใช้ตัวอื่นได้ แต่ปกติแล้วจะใช้ตัว T เพื่อความเข้าใจตรงกันว่าเป็นตัวแปรสำหรับ Type\)

```typescript
function getFirst<T>(arr: T[]): T {
  return arr[0]
}

const a = getFirst<number>([1, 2, 3])
//    a: number

const b = getFirst<string>(["One", "Two", "Three", "Four", "Five"]) 
//    b: string
```

ตัวอย่างนี้เราจะเซ็ตค่า T โดยตรงด้วย `number` และ `string`แต่ที่จริงแล้วเราไม่ต้องใส่ Type Variable เลยก็ได้ แล้ว TypeScript จะจัดการอนุมาน Type ให้เราเอง เรียกว่า Type Argument Inference

```typescript
const a = getFirst([1, 2, 3])
//    a: number เพราะ [1,2,3] เป็น number[] ทำให้ T = number

const b = getFirst(["One", "Two", "Three", "Four", "Five"])
//    b: string เพราะ argument เป็น string[] ทำให้ T = string
```

เราสามารถใช้ Type Variable มากกว่าหนึ่งตัวก็ได้ เช่น

```typescript
function map<T, U>(arr: T[], func: (arg: T) => U): U[] {
  return arr.map(func)
}

const input = ["4", "5", "6"]

map(input, (s) => parseInt(s)) // [4, 5, 6]
```

ดูจาก Argument ตัวแรกของฟังก์ชั่น `map`:

* `input` เป็น `string[]`
* `arr` ต้องเป็น `T[]`
* ฉะนั้น `T`   เป็น `string`

ดูจาก Argument ตัวที่สองของฟังก์ชั่น `map` :

* `(s) => parseInt(s)` เป็นฟังก์ช้่นที่ Return `parseInt()` ซึ่งเป็นฟังก์ชั่นที่จะคืน `number`
* `func` ต้องเป็น `(arg: string) => U`
* ฉะนั้น `U` เป็น `number`

และค่า Return ของฟังก์ชั่น เป็น `U[]`สรุปได้ว่าฟังก์ชั่น `map` นี้จะคืนค่าเป็น `number[]` หรืออาเรย์ของตัวเลข \(เฉพาะในกรณี`map(input, (s) => parseInt(s))` เท่านั้น ถ้าเรียกใช้แบบอื่น ค่า Return จะขึ้นอยู่กับฟังก์ชั่นที่ใส่เข้าไป\)

การใช้ Generics นั้นมีความซับซ้อนมาก \(ผู้เขียนก็ยังไม่เชี่ยวชาญเท่าไร\) เลยขอพักไว้เท่านี้ก่อน โค้ดเริ่มเยอะ

เดี๋ยวจะมีตอนต่อสำหรับ Generics แน่นอนครับ


# รู้จัก Basic Type ต่างๆ

คราวนี้เราจะมาแนะนำ Type พื้นฐานที่ควรรู้ก่อน ซึ่งจะแนะนำเฉพาะ Type ที่ใช้บ่อยๆ ในการเขียนโปรแกรมแบบที่ไม่ซับซ้อนมากก่อน

การกำหนด Type ให้กับตัวแปร ให้เราเพิ่ม `: [ชื่อ Type]` หลังจากชื่อตัวแปรและคีย์เวิร์ดที่ใช้สร้างตัวแปร \(`var`, `let`, `const`\)

### Number

`number`ใช้เก็บตัวเลข ทั้งที่เป็นจำนวนเต็ม \(Integer\) หรือมีทศนิยม \(Floating Point\)

```typescript
let a: number = 6
let b: number = 0xf00d
let c: number = -10.15
let d: bigint = 100n // BigInt จะเก็บข้อมูลได้เยอะกว่า Number ปกติ
```

### Boolean

`boolean` ใช้เก็บ `true` หรือ `false`

```typescript
let isGod: boolean = false
let isHuman: boolean = !isGod
```

### String

`string` ใช้เก็บข้อมูลสตริง \(ชุดอักขระ\)

```typescript
let a: string = "Jane"
let b: string = 'Noon'
let c: string = `Bow`
let d: string = `หนูชื่อ ${a} มากับ ${b} แล้วก็มากับ ${c}`
```

### Array

สำหรับอาเรย์จะเขียนได้สองแบบ ซึ่งทั้งคู่จะต้องระบุว่าทุกค่าในอาเรย์จะต้องเป็นประเภทไหน

```typescript
// แบบที่หนึ่ง ใช้ [] ต่อจากชี่อ Type
let list: number[] = [1, 2, 3]

// แบบที่สอง ใช้รูปแบบ "Generic" <> แล้วใส่ชื่อ Type ด้านใน
let list: Array<number> = [4, 5, 6]
```

### Tuple

Tuple คือ Array ที่กำหนดตายตัวแล้วว่ามีกี่ Element ซึ่งถ้าทำแบบนี้จะกำหนดให้แต่ละ Index มีค่าคนละประเภทกันได้

```typescript
let x: [number, string, boolean]

x = [10, "hello", true] // OK
x = [10, "hello"] // TypeError เพราะ Element ไม่ครบ
x = [10, "hello", "world"] // TypeError เพราะ Element ตัวสุดท้ายไม่ใช่ Boolean
```

### Any

`any` สำหรับการกำหนดให้เป็น "อะไรก็ได้"

```typescript
let x: any

x = 1 // OK
x = true // OK
x = "Bye" // OK
```

การใช้ `any` นั้นปกติไม่แนะนำให้ใช้ ยกเว้นกรณีที่จำเป็นเท่านั้น เพราะมันเป็นการทำให้ความ Type Safety ลดลง \(เหมือนกลับไปใช้ JavaScript\)

### Object

สำหรับออบเจกต์ จะมี `object` ให้ แต่โดยปกติแล้วจะไม่ใช้กัน มักทำเป็น Interface มากกว่า ซึ่งจะสอนในบทถัดๆ ไป

### Basic Type อื่นๆ

ยังมี Type อื่นๆ เช่น `Enum`, `Void`, `Null`, `Undefined`สามารถอ่านเพิ่มเติมได้จาก [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/basic-types.html)

## อ้างอิง

* [https://www.typescriptlang.org/docs/handbook/basic-types.html](https://www.typescriptlang.org/docs/handbook/basic-types.html)


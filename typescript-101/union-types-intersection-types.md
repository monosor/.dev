# Union Types และ Intersection Types

มีบ่อยครั้งที่ Type ที่สร้างขึ้นมาจะไม่ครอบคลุมการใช้งานได้ทั้งหมด หรือมีความต้องการที่จะใช้ตัวแปรเก็บค่าที่มีความซับซ้อนมากขึ้น เราสามารถใช้ Union Types และ Intersection Types มาช่วยได้

### Union Types

สำหรับการ Union เคยเกริ่นไปแล้วในบทก่อน \([Literal Types](literal-types.md)\) คือการใช้ `|` เพื่อเชื่อม Type เข้าด้วยกัน ทำให้ Type ที่สร้างขึ้นใหม่มีความยืดหยุ่นมากขึ้น

```typescript
type ID = string | number // ID สามารถเป็น string `หรือ` ตัวเลขก็ได้

const a: ID = "abc"
const b: ID = 101
```

เราจะนำ Union ไปเขียนเป็น Inline ในฟังก์ชั่นก็ได้เช่นกัน

```typescript
function sayHello(people: string | string[]) { // รับ string หรือชุดอาเรย์ของ string
  ...
}
```

เมื่อใช้ Union แล้วต้องการใช้ตัวแปรนั้น จะต้องทำการเช็ค Type ก่อนในโค้ด เรียกว่าการ Narrowing เช่นตามตัวอย่าง `people` อาจเป็น String หรือ Array ก็ได้ ถ้าไม่เช็คแล้วใช้ Function กับตัวแปรนั้น อาจมี Error เกิดขึ้นได้

```typescript
function sayHello(people: string | string[]) {
  console.log(`สวัสดี ${people.join(", ")}`)
}

sayHello(["เจน", "นุุ่น"]) // ✅ สวัสดี เจน, นุ่น
sayHello("โบว์")         // ❌ Error
```

![&#xE44;&#xE21;&#xE48;&#xE2A;&#xE32;&#xE21;&#xE32;&#xE23;&#xE16;&#xE43;&#xE0A;&#xE49; join\(\) &#xE44;&#xE14;&#xE49; &#xE40;&#xE1E;&#xE23;&#xE32;&#xE30;&#xE16;&#xE49;&#xE32; people &#xE40;&#xE1B;&#xE47;&#xE19; String &#xE08;&#xE30;&#xE40;&#xE01;&#xE34;&#xE14; Runtime error](../.gitbook/assets/image%20%285%29.png)

จากตัวอย่างข้างต้น ต้องทำการแก้ไขโค้ดให้รองรับทุก Type ที่ Union กัน เช่น

```typescript
function sayHello(people: string | string[]) {
  if (typeof people == "string") {
    console.log(`สวัสดี ${people} มาคนเดียวเหรอ`)
  } else {
    console.log(`สวัสดี ${people.join(", ")}`)
  }
}

sayHello(["เจน", "นุุ่น"]) // ✅ สวัสดี เจน, นุ่น
sayHello("โบว์")         // ✅ สวัสดี โบว์ มาคนเดียวเหรอ
```

อีกตัวอย่างหนึ่งที่จะได้ใช้ Union Type เช่น Literal Types

```typescript
type Color = "red" | "green" | "blue"

function printColorCode(c: Color): string {
  switch (c) {
    case "red":
      return "#FF0000"
    case "green":
      return "#00FF00"
    case "blue":
      return "#0000FF"
}
```

ถ้าในฟังก์ชั่นนี้ไม่ได้เช็คทุกกรณี เช่นมี case `red` กับ `green` แต่ไม่มี `blue` หรือสะกดเคสใดๆ ผิด จะเกิด Error ขึ้น

![Error &#xE40;&#xE1E;&#xE23;&#xE32;&#xE30;&#xE1E;&#xE34;&#xE21;&#xE1E;&#xE4C; &quot;blue&quot; &#xE1C;&#xE34;&#xE14;](../.gitbook/assets/image%20%286%29.png)

จะเห็นได้ว่า TypeScript จะทำให้เราเขียนโค้ดที่ Bug-free มากขึ้น เนื่องจากเรารองรับ Edge Case ท้ังหมดได้จากการจำกัด Type ที่จะใช้ในฟังก์ชั่น แต่ก็ยังมีความยืดหยุ่นจากการ Union ได้ ทำให้ไม่ต้องเขียนแยกกัน ทำให้มีโค้ดมากเกินความจำเป็น

### Intersection Types

การใช้ Intersection จะใช้กับ Interface จะเป็นเสมือนการ "ต่อ" Interface ต่างๆ เข้าด้วยกัน แต่เงื่อนไขจะแตกต่างกับ Union คือ Intersection นั้นค่าจะต้องเป็นออบเจกต์ที่มีหน้าตา ตรงกันกับทุก Type ที่นำมา Intersect กัน 

สมมุติว่ามี Interface ที่เป็นรูปวงกลม กับสี่เหลี่ยมที่มีค่าสี และคำนวณพื้นที่ได้

```typescript
interface ColorfulCircle {
  color: string
  radius: number
  area: () => number
}

interface ColorfulSquare {
  color: string
  size: number
  area: () => number
}
```

สังเกตว่ามีการใช้ชื่อและ Type ของ `color` และ `area` ซำ้กัน ซึ่งถ้าเราใช้ความสามารถของ Intersection \(ตัว `&`\) เราจะแยก Interface ที่ใช้ซำ้กันออกมา แล้ว Intersect ทีหลังได้ แบบนี้

```typescript
interface Colorful {
  color: string
}

interface Circle {
  radius: number
}

interface Square {
  size: number
}

interface Measurable {
  area: () => number
}

// มี color, radius และฟังก์ชั่น area
type ColorfulCircle = Colorful & Circle & Measurable

// มี color, size และฟังก์ชั่น area
type ColorfulSquare = Colorful & Square & Measurable
```

การใช้ Intersection จะทำให้เราสร้าง Interface เล็กๆ แล้วเอามา Reuse ต่อได้ ทำให้ Code อ่านง่ายขึ้นด้วย


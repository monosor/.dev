# Class \(1\)

คอนเซปท์ของ Class นั้นเป็นเหมือนกับตัวต้นแบบในการสร้าง Object ขึ้นมา เราสามารถนำ Class ไปใช้ประโยชน์ได้หลายทาง เช่นการแบ่งแยกประเภทข้อมูล หรือกำหนดลักษณะและความสามารถของ Object ที่จะสร้างขึ้นมาได้ ตัวอย่างยอดนิยมของ Class เช่น `Car` ที่สร้าง Object ต่างๆ ที่มีลักษณะไม่เหมือนกัน เช่นยี่ห้อรถ สี ความเร็ว นำ้หนัก เป็นต้น

JavaScript นั้นมีการใช้คีย์เวิร์ด Class มาตั้งแต่ ES2015 \(หรือ ES6\) และ TypeScript ก็เพิ่มความสามารถต่างๆ ให้กับตัว Class เพื่อรองรับการใช้ Type และ Interface ด้วย

### การสร้าง Class

Syntax การสร้าง Class จะคล้ายกับการประกาศ Interface ดังนี้

```typescript
class Car {
  year: number               
  color: "green" | "red" | "blue"
}

const c = new Car() // สร้างด้วยคีย์เวิร์ด new
c.year = 2560       // อ่านหรือเขียน year ได้ ตาม type ที่กำหนด
c.color = "red"
```

ถ้าต้องการให้ Field มีค่าเริ่มต้น ให้ Assign ค่าได้เลยด้านหลัง Field นั้น

```typescript
class Car {
  year: number = 2540                // ให้ค่าเริ่มต้นของ year เป็น 2540          
  color: "green" | "red" | "blue"
}

const c = new Car()
console.log(c.year) // 2540
```

หรือถ้าอยากกำหนดค่าเองตั้งแต่ตอน Initialize \(`new`\) ให้สร้าง `constructor` ด้านใน Class

```typescript
class Car {
  year: number       
  color: "green" | "red" | "blue"
  
  constructor(year = 2540, color = "green") { // ตั้งค่าเริ่มต้นของ year และ color
    this.year = year // ใช้ this เพื่อเซ็ตค่าใน Object
    this.color = color
  }
}

const c = new Car()
console.log(c.year) // 2540
console.log(c.color) // green

const d = new Car(2549, "blue")
console.log(d.year) // 2549
console.log(d.color) // blue
```

### Method

อันที่จริงแล้ว `constructor` ก็เป็น Method หนึ่ง เพียงแต่ว่ามันจะถูกเรียกเมื่อเราสร้าง Object ใหม่เท่านั้น การสร้าง Method จึงมีลักษณะเหมือนกับการสร้าง Constructor เลย แล้วเรียกใช้หลังจากที่สร้าง Object แล้ว

```typescript
class Car {      
  color: string
  
  constructor(color = "ดำ") {
    this.color = color
  }
  
  // ประกาศ Method printColor เพื่อ log ค่าสีออกมาใน console
  printColor() { 
    console.log(`รถคันนี้สี${this.color}`) // ใช้ this เพื่อดึงค่าใน Object ออกมา
  }
  
  // ประกาศ Method isColor เพื่อเช็คว่าสีรถตรงกับ input หรือไม่ โดยจะ Return boolean
  isColor(colorInput: string): boolean {
    return this.color == colorInput
  }
  
  // ประกาศ Method changeColor ไว้เปลี่ยนสีรถ
  changeColor(newColor: string) {
    this.color = newColor
  }
}

const car = new Car("ชมพู")

car.printColor() // รถคันนี้สีชมพู

console.log(car.isColor("ดำ")) // false
console.log(car.isColor("ชมพู")) // true

car.changeColor("แดง")
car.printColor() // รถคันนี้สีแดง
```

### Readonly

เราสามารถใช้คีย์เวิร์ด `readonly` เพื่อทำให้ค่าตัวแปรใน Object ไม่สามารถแก้ไขได้หลังจากที่รัน `constructor` เสร็จแล้ว

```typescript
class Car {      
  readonly color: string // ให้ color เป็น readonly
  
  constructor(color = "ขาว") {
    this.color = color
  }
 
  // ❌ Method changeColor ไม่สามารถใช้ได้เพราะ color เป็น readonly ไปแล้ว
  changeColor(newColor: string) {
    this.color = newColor
  }
}

const car = new Car("ชมพู") // ✅
car.color = "แดง" // ❌ แก้ไข color ด้วยการ assign ไม่ได้
```

### สร้าง Class ที่ Implement ตัว Interface

การใช้ Interface จะทำให้เราสร้าง Class ตามรูปแบบที่กำหนดใน Interface ได้ เพื่อการันตีว่าอย่างน้อย Class ของเรามีทั้ง Field และ Method ครบตาม Interface นั้นๆ โดยใช้คีย์เวิร์ด `implements`

```typescript
interface WithColor {
  color: string
  changeColor: (newColor: string) => void
}

class Car implements WithColor { // กำหนดให้ Car ต้อง implement ตาม WithColor
  year: number
}
// ❌ Error : ขาด Field color และ Method changeColor()


class DoYouLikeMyCar implements WithColor { 
  year: number = 2563
  color: string = "ดำ"

  changeColor(newColor: string) {
    this.color = newColor
  }
}
// ✅
```

การใช้ `implements` จะเหมาะกับกรณีเช่น เราขึ้นโครงด้วยการออกแบบ Interface ไว้ก่อน แล้วค่อยทำการเขียนโค้ดการใช้งานตามทีหลัง

### สร้าง Class ที่ Extend อีก Class หนึ่ง

เมื่อเราได้สร้าง Class ขึ้นมาแล้ว อาจพบว่ามีการใช้โค้ดซำ้กันบ้าง

```typescript
class Car {
  color: string = "ดำ"
  year: number = 2563
  
  changeColor(newColor: string) {
    this.color = newColor
  }
  
  printYear() {
    console.log(this.year)
  }
}

class Shirt {
  color: string = "ดำ"
  size: "S" | "M" | "L" = "M"
  
  changeColor(newColor: string) {
    this.color = newColor
  }
}
```

จะเห็นได้ว่าทั้งสอง Class นั้นมี Field `color` และ Method `changeColor` เหมือนกัน เราสามารถดึงโค้ดส่วนที่ซำ้ออกมาเป็น Class ใหม่ได้ แล้วใช้ `extends` เพื่อนำทั้ง Field และ Method มาใช้ \(เป็นการ Refactor แบบหนึ่ง\)

```typescript
class WithColor { 
  color: string = "ดำ"

  changeColor(newColor: string) {
    this.color = newColor
  }
}

class Car extends WithColor {
  year: number = 2563
  
  printYear() {
    console.log(this.year)
  }
}

class Shirt extends WithColor {
  size: "S" | "M" | "L" = "M"
  color: string = "ขาว"              // เปลี่ยนค่า Default เป็นสีขาว
}

const car = new Car()
car.changeColor("แดง")
console.log(car)
// Car: {
//   "color": "แดง",
//   "year": 2563
// }

const shirt = new Shirt()
console.log(shirt)
// Shirt: {
//   "color": "ขาว",
//   "size": "M"
// }
```

_To be continued_


# Class \(2\)

### Encapsulation

คลาสใน JavaScript, TypeScript ก็รองรับการตั้งค่า Access เหมือนกับภาษาทั่วๆ ไป เพื่อใช้ซ่อนข้อมูลจากคลาสอื่นๆ ได้ คีย์เวิร์ดที่ใช้คือ `public` `protected` และ `private`

#### Public Access

การตั้งค่าของตัวแปรและเมธอดเป็น `public` จะมีผลให้สามารถเรียกใช้จากข้างนอกได้

```typescript
class Dog {
  public name: string // ใช้ได้ทั้งใน ​Class และเรียกจากนอก Class
  
  public bark() {
    console.log("Woof!")
  }
}

const d = new Dog()
d.name = "Doge"
d.bark() // Woof!
```

ปกติถ้าไม่กำหนด Access ใดๆ เลย จะถือว่าเป็น `public` โดยอัตโนมัติ เราจึงไม่เห็นคนใช้ `public` กันเท่าไร

#### Protected Access

สำหรับ `protected` จะไม่สามารถเรียกจากภายนอกได้ แต่ถ้าเกิดการสร้าง Subclass ด้วยการใช้ `extend` จะสามารถใช้ภายใน Subclass ได้

```typescript
class Dog {
  protected color: string = "white" // color จะใช้ได้แค่ภายใน Class และ Subclass
  
  printColor() {
    console.log(`This dog is ${this.color}`)
  }
}

class MyDog extends Dog {
  printColor() {
    console.log(`My dog is ${this.color}, and he's cute!`)
  }
}

const d = new Dog()
d.color // ❌ เรียกใช้ไม่ได้ เพราะเป็น protected  
d.printColor() // This dog is white

const e = new MyDog()
e.printColor() // My dog is white, and he's cute!
```

#### Private Access

ถ้าเป็น `private` ตัวแปรและเมธอดจะใช้ได้แค่ภายในคลาสนั้นเท่านั้น Subclass ก็ไม่สามารถใช้ได้

```typescript
class Brain {
  private cellCount: number // cellCount จะใช้ได้แค่ใน Class นี้
  
  constructor(c: number) {
    this.cellCount = c
  }

  countCells() {
    console.log(`The brain has ${this.cellCount} cells`) // ✅
  }
}

const brain = new Brain(84000)
console.log(brain.cellCount) // ❌ ไม่สามารถเรียกใช้ cellCount จากภายนอกคลาสได้

class BigBrain extends Brain {
  doubleCells() {
    // ❌ ไม่สามารถเรียกใช้ cellCount จาก Subclass ได้
    this.cellCount = this.cellCount * 2
  }
}


```




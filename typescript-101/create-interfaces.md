# การสร้าง Interface

Interface จะเป็นตัวกำหนดว่า Object หรือ Class จะมีหน้าตาอย่างไรบ้าง ยกตัวอย่างดังนี้

```typescript
let person = {
  name: "Tu",
  age: 66,
  sayHi: () => "สวัสดีพ่อแม่พี่น้อง",
}
```

Type ของ `person` จะเป็นดังนี้ \(สังเกตว่าไม่ต้องใช้ `,` ท้ายบรรทัดก็ได้\)

```typescript
{
  name: string,
  age: number,
  sayHi: () => string, // Function ที่คืนค่าเป็น String
}
```

หากเราต้องการใช้ค่าเหล่านี้ซำ้ ให้ทำการสร้าง Interface ขึ้นมา แล้วจึงใช้ Interface ที่สร้างไว้ กำหนด Type ของตัวแปรออปเจกต์ ดังนี้

```typescript
interface Person { // ใช้ตัวพิมพ์ใหญ่
  name: string; // สังเกตว่าใช้ ; ท้ายบรรทัด ซึ่งจะมีหรือไม่มีก็ได้
  age: number;
  sayHi: () => string;
}

let person: Person = { // กำหนด Interface Person ให้กับตัวแปร
  name: "Tu",
  age: 66,
  sayHi: () => "สวัสดีพ่อแม่พี่น้อง",
}
```

ถ้าค่าของตัวแปรที่ไม่ตรงกับ Interface ที่กำหนดไว้ จะเกิด Error เช่นเดียวกับ Type อื่นๆ

```typescript
let person: Person = { 
  name: "Pom",
  
  // Error : Type 'string' is not assignable to type 'number'
  age: "75", 

  // Error : Type 'string' is not assignable to type '() => string'
  sayHi: "ไม่รู้ ไม่รู้ ไม่รู้", 
}
```

และเช่นเดียวกัน เราสามารถใช้ Interface กับพารามิเตอร์ของฟังก์ชั่น หรือค่า Return ของฟังก์ชั่นได้ด้วย

```typescript
function renamePerson(person: Person, newName: string): Person {
  person.name = newName
  
  return person
}

renamePerson(person, "Wissanu")
```

### Optional Properties

การสร้าง Interface ปกติจะถือว่า Properties ทุกตัวจำเป็นต้องถูกกำหนด \(Required\) แต่ถ้าหากต้องการให้สามารถเว้นว่างได้ ให้ทำเป็น Optional โดยการใช้ `?` ด้านหลังชี่อ Property

```typescript
interface House {
  area: number
  color?: string // กำหนดให้ color เป็น optional สามารถเว้นว่างได้
}

let house1 = { area: 100, color: "Green" }
let house2 = { area: 200 } // OK
let house3 = { color: "Green" } // Error : ขาด area
```

### อ้างอิง

* ศืกษาเรื่อง Interface เพิ่มเติม [https://www.typescriptlang.org/docs/handbook/interfaces.html](https://www.typescriptlang.org/docs/handbook/interfaces.html)




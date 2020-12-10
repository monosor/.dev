# ลองเขียนเว็บง่าย ๆ ด้วย TypeScript

เรียนทฤษฎีกันมาเยอะแล้ว ลองมาเขียนเว็บแบบง่ายๆ ด้วย TypeScript กันดีกว่า!

โดยเราจะใช้ CodeSandbox ในการเซ็ตอัปโปรเจกต์ [คลิกที่นี่เลย](https://codesandbox.io/s/vanilla-typescript-vanilla-ts)

ถ้าลิงก์ไม่เสีย เราจะเห็น Editor หน้าตาประมาณนี้ ซึ่งมีโค้ด TypeScript `index.ts` ที่ทำการ Render หน้าเว็บให้แบบโล่งๆ โค้ดที่มีอยู่แล้วให้ทำการลบไปได้เลย เราจะมาลองเขียน TypeScript และเรียนรู้ไปด้วยว่า มันต่างกับ JavaScript ยังไงบ้าง

![](../../.gitbook/assets/image%20%289%29.png)

เว็บที่เราจะเขียนจะใช้การเรียก API มาแล้วแสดงผลเป็นข้อมูล User โดยในที่นี้เราจะใช้บริการของ [Randomuser.me](https://randomuser.me) เพื่อคืนรายซื่อ User มาแบบสุ่ม และใช้ฟังก์ชั่น `fetch` ในการเรียก

เมื่อเราลองพิมพ์ `fetch(` ลงใป ตัว Editor จะแนะนำเราแบบคร่าวๆ ว่าต้องการอากิวเมนต์กี่ตัว และแต่ละตัวมี Type อะไรบ้าง \(Feature นี้เรียกว่า Intellisense\)

![](../../.gitbook/assets/image%20%2813%29.png)

จากภาพ `fetch` จะรับ Argument ตัวแรกเรียกว่า `input` ที่มีชนิดเป็น `RequestInfo` และตัวที่สองเรียกว่า `init` เป็น `RequestInit` หรือ `undefined` \(แปลว่าตัวที่สองเราจะไม่ใส่ก็ได้\) และมีการคืนค่าเป็น `Promise<Response>`

ต่อมาเราจะใส่ `input` ให้เป็น URL ของ API ที่เราต้องการใช้ คือ `https://randomuser.me/api` 

```typescript
fetch("https://randomuser.me/api")
```

เนื่องจาก `fetch` นั้นคืนค่าเป็น `Promise<Response>` เราต้องทำการรับด้วย `.then` แล้วภายในจะเป็นค่าที่มีชนิดเป็น `Response`หรือจะใช้ Syntax แบบ `async/await` ก็ได้

```typescript
fetch("https://randomuser.me/api").then(res => )
// res: Response

const res = await fetch("https://randomuser.me/api")
// res: Response
```

ในที่นี้เพื่อความง่ายเราจะใช้แบบ Promise ไปก่อน โดยทำการแปลงค่า`Response` ที่ได้มาเป็น Object ด้วย `.json()` เนื่องจาก API ที่เราทำการยิงไปนั้นคืนค่าเป็น JSON ต่อจากนั้นเราจะ Chain ด้วย `.then()` อีกครั้งเพื่อทดลอง Log ข้อมูลออกมา

```typescript
fetch("https://randomuser.me/api")
  .then(res => res.json())
  .then(res => console.log(res))
```

ใน Editor ให้กดที่ปุ่ม Console เพื่อดูค่าที่ Log ไว้

![](../../.gitbook/assets/image%20%2818%29.png)

จะเห็นว่า ข้อมูลของ `console.log(res)` เป็น Object ที่มีรูปร่างแบบนี้ 

```typescript
res = {
  results: [
    {
      gender: "male",
      name: {
        title: "Mr",
        first: "Xavier",
        last: "Anderson",
      },
      // etc
    }
  ]
}
```

แต่เมื่อเราลองไปชี้ที่ `res` ตัวล่างกลับพบว่า มันมี Type เป็น `any` เฉยเลย

![](../../.gitbook/assets/image%20%2814%29.png)

สาเหตุก็คือ ตัว `.json()` นั้นมีแค่หน้าที่แปลงข้อมูลเท่านั้น ไม่ได้รู้ล่วงหน้าว่าเราจะ Fetch ข้อมูลแบบไหนมา จึงทำให้มันกลายเป็น `any` ในท้ายที่สุด แปลว่าหลังจากนี้เราจะเรียกฟังก์ชั่นหรือทำอะไรกับ `res` ก็จะไม่ขึ้น Type Error เลย

![](../../.gitbook/assets/image%20%2812%29.png)

การที่จะทำให้ `res` กลับมามี Type อีกครั้ง ทำได้ด้วยการแปลงค่า โดยเรารู้อยู่แล้วว่าหน้าตาของข้อมูลจะเป็นประมาณไหน ให้สร้าง Interface หรือ Type ขึ้นมาจากข้อมูลนั้นได้เลย

```typescript
// res = {
//   results: [
//     {
//       gender: "male",
//       name: {
//         title: "Mr",
//         first: "Xavier",
//         last: "Anderson",
//       },
//       // etc
//     }
//   ]
// }

interface Res {
  results: [
    {
      gender: string;
      name: {
        title: string;
        first: string;
        last: string;
      };
      // Field ที่เหลือไม่ต้องใส่ก็ได้ เพราะเราไม่ใช้ทั้้งหมด
    }
  ];
}

fetch("https://randomuser.me/api")
  .then((res) => res.json())
  .then((res: Res) => console.log(res))
            // ^ กำหนดให้ res ตรงนี้มี Type เป็น Res
```

เมื่อเราทำให้ `res` มี Type ถูกต้องแล้ว Intellisense ก็จะกลับใช้งานได้อีกครั้ง เพราะไม่ได้เป็น `any` แล้ว

![Intellisense &#xE41;&#xE19;&#xE30;&#xE19;&#xE33; Field &#xE43;&#xE2B;&#xE49;&#xE15;&#xE32;&#xE21; Type &#xE17;&#xE35;&#xE48;&#xE40;&#xE23;&#xE32;&#xE01;&#xE33;&#xE2B;&#xE19;&#xE14;](../../.gitbook/assets/image%20%2815%29.png)

คราวนี้เรามาลองทำให้พิมพ์ User ออกมา 5 คนดู โดยแก้ API URL นิดหน่อย แล้วเขียนฟังก์ชั่นมารับค่าไปแสดงผลทางเว็บ แนะนำให้ลองพิมพ์ตามแทนที่จะ Copy-Paste เพื่อให้เห็นว่า TypeScript สามารถช่วยเราในการพิมพ์โค้ดได้เยอะมากๆ ต่างจาก JavaScript ที่เราอาจต้อง `console.log` เพื่อดีบั๊กค่าตัวแปรอยู่เรื่อยๆ

```typescript
function printToWeb(res: Res) {
  res.results.forEach((user) => {
    document.getElementById("app").innerHTML += 
      `<h2>${user.name.first} ${user.name.last}</h2>`
  })
}

// เติม ?results=5 เพื่อให้ API คืนข้อมูลจำนวน 5 คน
fetch("https://randomuser.me/api?results=5")
  .then((res) => res.json())
  .then((res: Res) => printToWeb(res))
```

เมื่อทำเสร็จแล้ว กดดูที่ Browser จะเห็นว่ามีชื่อที่พิมพ์ออกมาแล้ว

![](../../.gitbook/assets/image%20%2810%29.png)

### Improvements

โค้ดของเราอาจทำงานได้ตามต้องการแล้ว แต่ยังมีบางจุดที่สามารถจัดการให้เรียบร้อยขึ้นได้ ดังนี้

#### 1. Refactor Type

โดยทั่วไปแล้วเราจะไม่สร้าง Type/Interface ที่มีข้อมูลหลายชั้นมากจนเกินไป ตาม Practice แล้วควรจะ Refactor ด้วยการสร้าง Type/Interface เพิ่มเติม และตั้งชื่อให้เข้าใจได้ง่าย จากตัวอย่างเรามี Interface `Res` หน้าตาแบบนี้

```typescript
interface Res {
  results: [
    {
      gender: string;
      name: {
        title: string;
        first: string;
        last: string;
      };
    }
  ];
}
```

เราสามารถแยกออกมาเป็น Interface ย่อยๆ ได้ คล้ายๆ กับการแยกตัวแปรเลย แบบนี้

```typescript
interface Results {
  results: [User] // Array ของ User
}

interface User {
  gender: string
  name: Name
}

interface Name {
  title: string
  first: string
  last: string
}
```

#### 2. Fix warnings

จะมีบ่อยคร้ัง ที่เราทำงานกับเว็บแล้วเรียกฟังก์ชั่นที่ "อาจคืนค่าเป็น `null`" ก็ได้ เช่นกรณีนี้เราจะหา HTML Element ที่มีไอดีเป็น app เช่น `<div id="app">` แต่ถ้าเราไม่มี Element นี้บนหน้าเว็บเลย ฟังก์ชั่นนี้จะคืนค่า `null` แทน และโค้ดนี้จะพังเพราะว่าไม่สามารถใช้ `innerHTML` ได้

ถ้าลองชี้ที่ getElementById ดู มันจะบอกว่า ฟังก์ชั่นนี้คืน `HTMLElement | null`

![&#xE02;&#xE35;&#xE14;&#xE40;&#xE2A;&#xE49;&#xE19;&#xE43;&#xE15;&#xE49;&#xE40;&#xE2D;&#xE32;&#xE44;&#xE27;&#xE49; &#xE27;&#xE48;&#xE32;&#xE40;&#xE18;&#xE2D;&#xE21;&#xE35;&#xE1A;&#xE31;&#xE4A;&#xE01;~](../../.gitbook/assets/image%20%288%29.png)

เราอาจแก้ด้วยการเช็คก่อนว่าค่านั้นเป็น `null` หรือไม่ แต่จะทำให้โค้ดดูยาวขึ้นโดยไม่จำเป็น

```typescript
if (document.getElementById("app") !== null) {
  document.getElementById("app").innerHTML += `...`
}
```

กรณีนี้เรารู้อยู่แก่ใจว่ามีไอดี `app` อยู่แน่นอน และจะทำการ "บังคับ" ให้ไม่มี Error โดยการใช้ [Non-null operator](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#non-null-assertion-operator) หรือเครื่องหมาย `!` เป็นการบอกกับ TypeScript ว่าเรามั่นใจว่าโค้ดไม่ Return `null` แน่ๆ

```typescript
function printToWeb(res: Results) {
  res.results.forEach((user) => {
    document.getElementById("app")!.innerHTML += 
      `<h2>${user.name.first} ${user.name.last}</h2>`;
  });
}
```

เมื่อทำแบบนี้แล้วเส้นแดง Warning ก็จะหายไปแล้ว \(แต่ว่าถ้าเราไม่มีไอดี `app` อยู่จริง แอปก็จะพังอยู่ดีนะ ฉะนั้นไม่ควรใช้ Non-null operator พรำ่เพรื่อ\)

### Code ทั้งหมด \(เฉพาะ TypeScript\)

```typescript
interface Results {
  results: [User]
}

interface User {
  gender: string
  name: Name
}

interface Name {
  title: string
  first: string
  last: string
}

function printToWeb(res: Results) {
  res.results.forEach((user) => {
    document.getElementById("app")!.innerHTML += 
      `<h2>${user.name.first} ${user.name.last}</h2>`;
  })
}

fetch("https://randomuser.me/api?results=5")
  .then((res) => res.json())
  .then((res: Results) => printToWeb(res))
```

จากทั้งหมดนี้ เราจะเห็นประโยชน์ในการใช้งาน TypeScript ในการทำเว็บ ทั้งการใช้ประโยชน์จาก Intellisense เพื่อช่วยแนะนำในการเขียนโค้ดต่างๆ ได้ รวมถึงการ Type Check ที่จะเตือนเราด้วย Error หรือ Warning เมื่อโค้ดบางจุดมีโอกาสที่จะเกิดบั๊กได้ ทำให้เราระมัดระวังและเขียนโค้ดได้อย่างมั่นใจมากขึ้น และการสร้าง Type/Interface เองทำให้เราหรือคนอื่นที่มาแก้โค้ด เข้าใจ Structure ได้ดีขึ้นด้วย


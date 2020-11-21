# ติดตั้ง TypeScript

โค้ดที่เป็น TypeScript เมื่อจะนำมาใช้จะต้องทำการคอมไพล์ หรือแปลงเป็น JavaScript ก่อน โดยต้องทำการลงแพคเกจ `typescript` ผ่าน `npm`, `yarn`

```bash
npm install -g typescript # npm
yarn global add typescript # yarn
```

หรือติดตั้งในโปรเจกต์ที่มี `package.json` อยู่แล้ว

```bash
npm install --save-dev typescript
yarn add --dev typescript
```

เมื่อติดตั้งแล้วจะมีโปรแกรม `tsc` ไว้ใช้สำหรับใช้งานกับไฟล์ TypeScript ที่มีนามสกุล `.ts`

```bash
$ tsc # หรือ yarn tsc หรือ npx tsc ถ้าลงแบบไม่ global
Version 4.1.2
Syntax:   tsc [options] [file...]

Examples: tsc hello.ts
          tsc --outFile file.js file.ts
          tsc @args.txt
          tsc --build tsconfig.json
...
```

ทดลองเขียนโปรแกรมง่ายๆ กัน

```typescript
// hello.ts

const user = {
  firstName: "ประหยัด",
  lastName: "จานโอชา",
  job: "Dictator",
}

console.log(`ฉันชื่อ ${user.firstName} ${user.lastname}`) // จงใจสะกด lastName ผิด
console.log(`อาชีพของฉันคือ ${user.job}`)

```

แล้วรันด้วย `tsc` จะเกิด Type Error ขึ้น พร้อมกับแจ้งว่ามีปัญหาที่จุดไหน

```bash
$ tsc hello.ts
hello.ts:7:47 - error TS2551: Property 'lastname' 
does not exist on type '{ firstName: string; lastName: string; job: string; }'. 
Did you mean 'lastName'?

7 console.log(`ฉันชื่อ ${user.firstName} ${user.lastname}`)
                                             ~~~~~~~~

  index.ts:3:3
    3   lastName: "จานโอชา",
        ~~~~~~~~~~~~~~~~~~~
    'lastName' is declared here.


Found 1 error.
```

และเมื่อเราแก้โค้ดจนถูกต้องแล้วรันใหม่ จะได้ไฟล์ JavaScript ออกมา \(ถ้าไม่ได้กำหนดออปชั่นเพิ่มเติม จะได้ชื่อไฟล์เดิม แต่มีนามสกุลไฟล์ `.js` แทน เช่น `hello.ts` -&gt; `hello.js`\)

เบื้องหลังของ Framework ต่างๆ ที่ระบุว่าสนับสนุนการใช้ TypeScript นั้นก็คือมีการใช้เครื่องมืออย่าง `tsc` ในการแปลงโค้ดให้เป็น JavaScript นั่นเอง


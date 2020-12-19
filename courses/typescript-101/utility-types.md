# Utility Types

ขอทิ้งท้ายคอร์ส TypeScript 101 ด้วย Utility Types หรือ Type ตัวช่วยต่างๆ ที่ TypeScript มีให้ใช้งาน

### `Partial<Type>` <a id="recordkeystype"></a>

`Partial<T>` จะรับ Object Type และเปลี่ยน Property ทั้งหมดให้เป็น [Optional](optional-properties.md) เพื่อที่เราจะได้ใช้เฉพาะบาง Property ได้

```typescript
interface Post {
  title: string
  body: string
  imageUrl: string
}

type PostFields = Partial<Post>

// เหมีอนกันกับ
interface PostFields {
  title?: string
  body?: string
  imageUrl?: string
}

function updatePost(post: Post, fields: PostFields) {
  ...
}

const post = { title: "...", body: "...", imageUrl: "..." }

// Update เฉพาะ Body ของ Post
const updatedPost = updatePost(post, { body: "..." }) 
```

ตัวอย่างนี้ใช้ประโยชน์จาก `Partial<Post>` เพื่อให้เวลาที่เราอัพเดตตัว Post โดยไม่ต้องใช้ Field ทั้งหมดก็ได้

### `Pick<Type,Keys>` <a id="recordkeystype"></a>

ใช้เพื่อ Pick \(เลือก\) เฉพาะ Key ของ Property มาเป็น Object Type ใหม่

```typescript
// "เลือก" เฉพาะ Property title และ body
type PostTitleAndBody = Pick<Post, "title" | "body">

// เหมือนกันกับ
interface PostTitleAndBody {
  title: string
  body: string
}

function updatePost(post: Post, fields: PostTitleAndBody) { ... }

updatePost(post, { title: "...", body: "..." })
```

### `Omit<Type,Keys>` <a id="recordkeystype"></a>

ตรงข้ามกับ Pick คือจะยกเว้น Keys ที่ระบุไว้

```typescript
// ใช้ทุก Properties ของ Post "ยกเว้น" title
type PostDetails = Omit<Post, "title">

// เหมือนกันกับ
interface PostDetails {
  body: string
  imageUrl: string
}
```

### `Record<Keys,Type>` <a id="recordkeystype"></a>

สร้าง Object Type ด้วย Property ที่เป็น `Keys` และมี Value เป็นประเภทตาม `Type`

```typescript
type CodeName = "alpha" | "beta" | "charlie"
type Color = "red" | "green" | "blue" | "white" | "black"

// List ต้องเป็น Object ที่มีชี่อ Property เป็น CodeName 
// และ Value เป็น Object { color: Color }
type CodeWithColor = Record<CodeName, { color: Color }>

const codes: CodeWithColor = {
  alpha: { color: "blue" }
  beta: { color: "red" }
}
```

### `Parameters<FunctionType>` <a id="parameterstype"></a>

ดึง Type ของ Parameters ออกมาจาก Function ออกมาเป็น Tuple \(Array\)

```typescript
// (a: number, b: number) => number
function sum(a: number, b: number) { return a + b }

type SumParams = Parameters<sum> // ❌ ต้องใช้ Type ไม่ใช่ใส่ function เข้าไปโดยตรง
type SumParams = Parameters<typeof sum> // ✅ ใช้ typeof เพื่อดึง Type จาก function

// เหมือนกันกับ
type SumParams = [a: number, b: number] // Tuple ที่มี 2 ตัว
```

### `ReturnType<FunctionType>` <a id="returntypetype"></a>

ดึง Type ของค่า Return จาก Function

```typescript
// (a: number, b: number) => number
function sum(a: number, b: number) { return a + b }

type SumReturn = ReturnType<typeof sum> // number

// (msg: string) => void
function log(msg) { console.log(`LOG : ${msg}`) }

type LogReturn = ReturnType<typeof log> // void
```

Utility Types ยังมีอีกหลายตัว ดูทั้งหมดได้จาก [Official Docs](https://www.typescriptlang.org/docs/handbook/utility-types.html) ซึ่งจะช่วยให้เราใช้ประโยชน์จาก Type ที่มีอยู่แล้ว หรือ Import มาจาก Library ต่างๆ ได้โดยไม่ต้องกำหนด Generic Type ที่ซับซ้อนเองทั้งหมด


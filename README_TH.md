# เว็บเกมเรียนของน้องๆ: วิธีติดตั้ง (ทำครั้งเดียว ประมาณ 15 นาที)

ในโฟลเดอร์นี้มีอะไรบ้าง
- `index.html`: หน้าแรก เลือกเกม
- `cat/`: สวนคณิตน้องปุยฝ้าย (ป.4)
- `dragon/`: The Rainbow Dragon (อนุบาล–ป.1)
- `config.js`: ต้องใส่ค่าจาก Firebase (ขั้นที่ 3)
- `firestore.rules`: กฎความปลอดภัยของที่เก็บเซฟ
- `firebase.json`: ไฟล์ตั้งค่าสำหรับเอาเว็บขึ้น Firebase Hosting

## 1. สร้างโปรเจกต์ Firebase (ฟรี)
1. เข้า https://console.firebase.google.com แล้วล็อกอินด้วยบัญชี Google
2. กด **Create a project** ตั้งชื่อ เช่น `kids-games` ปิด Google Analytics ได้
3. ใช้แผน **Spark (ฟรี)** ไม่ต้องใส่บัตรเครดิต

## 2. สร้างที่เก็บเซฟ (Firestore)
1. เมนูซ้าย **Build > Firestore Database** > **Create database**
2. เลือก location `asia-southeast1 (Singapore)` แล้วเลือก **production mode**
3. ไปที่แท็บ **Rules** ลบข้อความเดิมทั้งหมด วางเนื้อหาจากไฟล์ `firestore.rules` แล้วกด **Publish**

## 3. เอาค่า config มาใส่
1. กดรูปเฟือง ⚙️ > **Project settings** > ส่วน **Your apps** > กดไอคอน **</>** (Web) ตั้งชื่ออะไรก็ได้ แล้วกด Register (ไม่ต้องติ๊ก Hosting)
2. จะเห็นโค้ด `firebaseConfig` ให้คัดลอกค่า `apiKey` และ `projectId`
3. เปิดไฟล์ `config.js` แล้วใส่ค่าในเครื่องหมายคำพูด

ค่า apiKey ของ Firebase แบบเว็บเปิดเผยได้ ความปลอดภัยอยู่ที่กฎในขั้นที่ 2

## 4. เอาเว็บขึ้นออนไลน์ (เลือก 1 วิธี)

**วิธี A: ง่ายที่สุด ไม่ต้องติดตั้งอะไร (Netlify Drop)**
1. เข้า https://app.netlify.com/drop
2. ลากทั้งโฟลเดอร์ `site` ไปวาง จะได้ลิงก์ เช่น `https://xxxx.netlify.app`
3. สมัครบัญชี Netlify ฟรีเพื่อเก็บเว็บไว้ถาวร และเปลี่ยนชื่อลิงก์ให้จำง่ายได้ (Site settings > Change site name)

**วิธี B: Firebase Hosting (อยู่ที่เดียวกับที่เก็บเซฟ)**
```
npm install -g firebase-tools
firebase login
cd site
firebase use --add      (เลือกโปรเจกต์ที่สร้างไว้)
firebase deploy --only hosting,firestore:rules
```
จะได้ลิงก์ `https://<project-id>.web.app`

## 5. วิธีใช้งานของน้องๆ
- เปิดลิงก์ เลือกเกม ใส่ **ชื่อผู้เล่น + PIN 4 ตัว** แล้วเล่นได้เลย เกมเซฟออนไลน์ให้เองทุกครั้ง
- เปลี่ยนเครื่องหรือเปลี่ยนเบราว์เซอร์ ใส่ชื่อและ PIN เดิมก็เล่นต่อได้ทันที
- ติดตั้งเป็นไอคอนบนหน้าจอโฮม
  - iPhone/iPad: Safari > ปุ่มแชร์ > **Add to Home Screen**
  - Android: Chrome > ⋮ > **Add to Home screen**
- ถ้าไม่มีเน็ต ยังเล่นได้ เกมจะเก็บไว้ในเครื่องก่อน แล้วเซฟขึ้นออนไลน์ให้เองเมื่อเน็ตกลับมา
- ถ้าลืม PIN: ไม่มีระบบกู้คืน ให้ใช้ชื่อเดิมกับ PIN ใหม่แล้วเริ่มใหม่ (หรือกู้ด้วยรหัสสำรองที่เคยเก็บไว้)

## 6. ส่งลิงก์ใหม่ให้ Claude
ส่งลิงก์เว็บใหม่มา ผมจะเปลี่ยนลิงก์เดิมบน Claude ให้พาไปเว็บใหม่ และพาเซฟล่าสุดของเครื่องนั้นติดไปด้วย

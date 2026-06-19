# 📚 คำแนะนำการอัปโหลด GitHub Pages

## วิธี 1: GitHub Pages (แนะนำ) ⭐

### ขั้นตอน:

#### 1️⃣ สร้าง GitHub Account
- ไปที่ https://github.com
- คลิก **Sign up**
- กรอกข้อมูล (Email, Password, Username)
- ยืนยัน Email

#### 2️⃣ สร้าง New Repository
- คลิก **+** ที่มุมบนขวา
- เลือก **New repository**
- ตั้งชื่อ: `attendance-system` (หรือชื่ออื่นตามต้องการ)
- เลือก **Public** (เพื่อให้ GitHub Pages ใช้งานได้)
- คลิก **Create repository**

#### 3️⃣ อัปโหลดไฟล์
**วิธี A: ผ่าน Web Interface**
1. ไปที่ Repository ที่สร้างใหม่
2. คลิก **Add file** → **Upload files**
3. ลากไฟล์ `attendance_system.html` และ `README.md` เข้าไป
4. คลิก **Commit changes**

**วิธี B: ผ่าน Git Command Line**
```bash
# 1. Clone Repository
git clone https://github.com/YOUR_USERNAME/attendance-system.git

# 2. เข้าโฟลเดอร์
cd attendance-system

# 3. ย้ายไฟล์ HTML มาไว้ที่นี่
# (Copy ไฟล์ attendance_system.html และ README.md)

# 4. Add ไฟล์ทั้งหมด
git add .

# 5. Commit
git commit -m "Initial commit: Add attendance system"

# 6. Push ขึ้น GitHub
git push origin main
```

#### 4️⃣ เปิดใช้งาน GitHub Pages
1. ไปที่ Repository Settings
2. ค้นหา **Pages** ที่เมนูด้านซ้าย
3. ใต้ **Source** เลือก:
   - Branch: `main`
   - Folder: `/ (root)`
4. คลิก **Save**
5. รอสักครู่... GitHub จะเตรียมให้คุณ
6. ดูลิงก์ที่ปรากฏ เช่น: `https://your-username.github.io/attendance-system/`

#### 5️⃣ เข้าถึงระบบ
- เปิด Browser
- ไปที่: `https://your-username.github.io/attendance-system/attendance_system.html`

---

## วิธี 2: GitHub Pages ด้วย Username

### สำหรับผู้ที่ต้องการ URL สั้น

#### ขั้นตอน:
1. สร้าง Repository ชื่อ: `your-username.github.io`
2. อัปโหลดไฟล์ `attendance_system.html`
3. ไป Settings → Pages
4. เลือก Branch `main`
5. เข้าถึงได้ที่: `https://your-username.github.io/attendance_system.html`

---

## วิธี 3: ใช้งานโดยตรง (ไม่ต้องอัปโหลด)

### ขั้นตอน ง่ายๆ:
1. ดาวน์โหลดไฟล์ `attendance_system.html`
2. คลิกขวา → **Open with** → Browser
3. ใช้งานได้เลย!

---

## 🔗 ลิงก์ที่ใช้งาน

### ตัวอย่างหลังจากอัปโหลด:

```
https://your-username.github.io/attendance-system/attendance_system.html
                      ↓                              ↓
                  Username                    ชื่อไฟล์
```

**ชื่อแต่ละส่วน:**
- `your-username` = GitHub Username ของคุณ
- `attendance-system` = Repository ที่สร้าง
- `attendance_system.html` = ไฟล์ HTML

---

## 🆘 ปัญหาที่พบบ่อย

### ❌ GitHub Pages ไม่ทำงาน
**วิธีแก้:**
1. ตรวจสอบว่า Repository เป็น **Public** หรือไม่
2. ตรวจสอบ Settings → Pages → Source ว่าเลือก Branch `main` หรือไม่
3. รอ 5-10 นาที (GitHub อาจใช้เวลา)

### ❌ ไฟล์ไม่พบ (404)
**วิธีแก้:**
1. ตรวจสอบชื่อไฟล์ว่าถูกต้องหรือไม่
2. ตรวจสอบ Case-sensitive (`.html` ต้องเป็นตัวเล็ก)
3. ตรวจสอบว่าไฟล์อยู่ใน Root Folder หรือไม่

### ❌ ข้อมูลหายไป
⚠️ **ข้อมูลจัดเก็บใน Browser เท่านั้น**
- ปิด Browser = ข้อมูลหายไป
- วิธีแก้: Export เป็น Excel/PDF ก่อนปิด Browser

---

## ✨ เคล็ดลับเพิ่มเติม

### 1. สร้าง `.gitignore` (Optional)
```
# .gitignore
node_modules/
.DS_Store
*.log
```

### 2. ใช้ Markdown ใน README
ตัวอักษรหนา: `**bold**`
ตัวอักษรเอียง: `*italic*`
ลิงก์: `[text](url)`

### 3. เพิ่ม Branch Protection
1. Settings → Branches
2. เพิ่ม Rule สำหรับ `main`
3. เลือก "Require pull request reviews"

---

## 📖 อ้างอิงเพิ่มเติม

- GitHub Help: https://docs.github.com
- GitHub Pages: https://pages.github.com
- Markdown Guide: https://www.markdownguide.org

---

## 🎉 เสร็จแล้ว!

ระบบเช็คชื่อของคุณพร้อมใช้งานแล้ว!

**ลิงก์ของคุณ:**
```
https://your-username.github.io/attendance-system/attendance_system.html
```

---

**Last Updated:** 2026
**Version:** 1.0.0

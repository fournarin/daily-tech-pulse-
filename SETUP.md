# 🛠️ Setup Guide — Daily Tech Pulse

ทำตามขั้นตอนนี้ทีละขั้น ใช้เวลาไม่เกิน 10 นาที

---

## ✅ สิ่งที่ต้องเตรียม

- [ ] GitHub account
- [ ] GitHub Personal Access Token (PAT) — สร้างในขั้นตอนที่ 2
- [ ] Gemini API key — สำหรับ AI digest (ไม่บังคับ แต่แนะนำ)

---

## 📋 ขั้นตอนที่ 1 — สร้าง GitHub Repo

1. ไปที่ github.com → **New repository**
2. ตั้งชื่อ: `daily-tech-pulse`
3. เลือก **Public** (ให้คนอื่นเห็น contribution ได้)
4. **อย่า** tick "Add a README" (เราจะ upload ไฟล์เอง)
5. คลิก **Create repository**

---

## 🔑 ขั้นตอนที่ 2 — สร้าง Personal Access Token (PAT)

1. GitHub → รูปโปรไฟล์มุมขวาบน → **Settings**
2. เลื่อนลงสุด → **Developer settings**
3. **Personal access tokens → Tokens (classic)**
4. คลิก **Generate new token (classic)**
5. ตั้งค่า:
   - **Note:** `daily-tech-pulse-bot`
   - **Expiration:** `No expiration`
   - **Scopes ที่ต้องติ๊ก:**
     - ✅ `repo` (ทั้ง group)
     - ✅ `workflow`
6. คลิก **Generate token**
7. **คัดลอก token ไว้ทันที** (ดูได้แค่ครั้งเดียว!)

---

## 🔐 ขั้นตอนที่ 3 — เพิ่ม Secrets ใน Repo

ไปที่ repo → **Settings → Secrets and variables → Actions → New repository secret**

เพิ่ม 2 secrets:

| Secret Name | Value |
|-------------|-------|
| `DAILY_TOKEN` | Token จากขั้นตอนที่ 2 |
| `GEMINI_API_KEY` | API key จาก Google AI Studio (ไม่บังคับ) |

### วิธีขอ Gemini API Key:
1. ไปที่ [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. คลิก **Create API key**
3. คัดลอกและบันทึกเป็น `GEMINI_API_KEY`

> **หมายเหตุ:** Gemini Pro plan (Google One) กับ Gemini API เป็นคนละระบบ — ต้องสร้าง API key แยกจาก AI Studio (ฟรี tier ใช้ได้กับ bot นี้)

---

## 📤 ขั้นตอนที่ 4 — Upload ไฟล์ทั้งหมด

```bash
# Clone repo ที่เพิ่งสร้าง
git clone https://github.com/YOUR_USERNAME/daily-tech-pulse.git
cd daily-tech-pulse

# Copy ไฟล์จาก zip ที่ได้รับมาลงในโฟลเดอร์นี้
# (ตรวจสอบว่ามีไฟล์เหล่านี้ครบ)
# - scripts/main.py
# - .github/workflows/daily_digest.yml
# - README.md
# - requirements.txt
# - reports/.gitkeep

# Push ขึ้น GitHub
git add .
git commit -m "🚀 Initial setup: Daily Tech Pulse Bot"
git push origin main
```

---

## ▶️ ขั้นตอนที่ 5 — เปิด GitHub Actions

1. ไปที่ repo → tab **Actions**
2. ถ้ามีข้อความ "Workflows aren't being run on this repository" → คลิก **I understand, enable workflows**

---

## 🧪 ขั้นตอนที่ 6 — ทดสอบรันครั้งแรก

1. **Actions → 🤖 Daily Tech Pulse → Run workflow → Run workflow**
2. รอประมาณ 1-2 นาที
3. ถ้าสำเร็จ จะเห็น:
   - ✅ Branch ใหม่ถูกสร้างและ merge แล้ว
   - ✅ ไฟล์ `reports/YYYY-MM-DD.md` ใน repo
   - ✅ PR ที่ถูก merge แล้ว
   - ✅ Issue ใหม่ที่ถูกเปิด

---

## 🕗 Schedule

Bot จะรันอัตโนมัติทุกวันราว **08:17 น. เวลาไทย (UTC+7)** พร้อม fallback 09:17 และ 10:17 น. หากรอบแรกไม่ยิง

> GitHub Actions ใช้ **UTC** เท่านั้น และ schedule **ไม่รับประกัน** เวลาเป๊ะ — โดยเฉพาะนาที `:00` ของทุกชั่วโมง (โหลดสูง) อาจถูกเลื่อนหรือข้ามได้

หากต้องการเปลี่ยนเวลา แก้ไขใน `.github/workflows/daily_digest.yml`:
```yaml
- cron: "17 1 * * *"   # 01:17 UTC = 08:17 Bangkok (primary)
- cron: "17 2 * * *"   # 09:17 Bangkok (fallback)
- cron: "17 3 * * *"   # 10:17 Bangkok (fallback)
```

หลังแก้ cron ให้ **push ขึ้น `main`** — GitHub จะ resync scheduler (repo ใหม่มักต้อง push อีกครั้งก่อน cron จะยิงสม่ำเสมอ)

---

## ❓ แก้ปัญหา

| ปัญหา | วิธีแก้ |
|-------|---------|
| Workflow ไม่รัน (cron) | ตรวจว่า Enable workflows แล้ว + workflow อยู่บน branch `main` + push commit ใหม่เพื่อ resync schedule |
| Cron ไม่ยิงแต่ manual รันได้ | ปกติของ GitHub — ใช้ fallback cron ใน workflow หรือรัน manual จาก Actions tab |
| Error: Bad credentials | ตรวจสอบ DAILY_TOKEN ใน Secrets |
| Error: 422 | Branch มีอยู่แล้ว — รอวันพรุ่งนี้หรือลบ branch เก่าออก |
| ไม่มี AI digest | เพิ่ม GEMINI_API_KEY ใน Secrets |

---

*Setup เสร็จแล้ว! Bot จะทำงานเองทุกวัน 🎉*

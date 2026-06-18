# 🛠️ Setup Guide — Daily Tech Pulse

ทำตามขั้นตอนนี้ทีละขั้น ใช้เวลาไม่เกิน 10 นาที

---

## ✅ สิ่งที่ต้องเตรียม

- [ ] GitHub account
- [ ] GitHub Personal Access Token (PAT) — สร้างในขั้นตอนที่ 2
- [ ] Anthropic API key — สำหรับ AI digest (ไม่บังคับ แต่แนะนำ)

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
| `PAT_TOKEN` | Token จากขั้นตอนที่ 2 |
| `ANTHROPIC_API_KEY` | API key จาก console.anthropic.com (ไม่บังคับ) |

### วิธีขอ Anthropic API Key:
1. ไปที่ [console.anthropic.com](https://console.anthropic.com)
2. **API Keys → Create Key**
3. คัดลอกและบันทึกเป็น `ANTHROPIC_API_KEY`

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

Bot จะรันอัตโนมัติทุกวัน **8:00 AM เวลาไทย (UTC+7)**

หากต้องการเปลี่ยนเวลา แก้ไขบรรทัดนี้ใน `.github/workflows/daily_digest.yml`:
```yaml
- cron: '0 1 * * *'   # 01:00 UTC = 08:00 Bangkok
```

---

## ❓ แก้ปัญหา

| ปัญหา | วิธีแก้ |
|-------|---------|
| Workflow ไม่รัน | ตรวจสอบว่า Enable workflows แล้ว |
| Error: Bad credentials | ตรวจสอบ PAT_TOKEN ใน Secrets |
| Error: 422 | Branch มีอยู่แล้ว — รอวันพรุ่งนี้หรือลบ branch เก่าออก |
| ไม่มี AI digest | เพิ่ม ANTHROPIC_API_KEY ใน Secrets |

---

*Setup เสร็จแล้ว! Bot จะทำงานเองทุกวัน 🎉*

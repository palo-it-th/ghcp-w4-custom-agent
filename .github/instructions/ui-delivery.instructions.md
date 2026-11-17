---
applyTo: "ui/**,outputs/**"
---

# มาตรฐานไฟล์ส่งมอบงาน Sprint 2 (Delivery Artifacts Rule)

- สำหรับไฟล์เอกสารใน `outputs/ba/` และ `outputs/qa/`: ต้องระบุรหัส `Change Request ID` (`CR-201` หรือ `CR-202`) และรหัสกฎที่อ้างอิง (`BR-01..03` หรือ `EC-01..03`) ไว้ที่ส่วนหัวของเอกสารเสมอ
- สำหรับไฟล์โค้ดใน `ui/`: ต้องประกาศ CSS Custom Properties (`--bg-surface`, `--accent-primary`, `--radius-md`) ใน `:root` และห้ามเขียน inline style สำหรับสีหลักของปุ่ม

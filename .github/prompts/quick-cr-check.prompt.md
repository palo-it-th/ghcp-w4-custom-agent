---
name: quick-cr-check
description: "สรุปเป้าหมายและรหัส Business Rule ของ task Change Request (CR-201 หรือ CR-202) แบบสั้น 3 บรรทัด (Reusable Prompt · Local harness only)"
---

จากไฟล์ใบงาน Change Request ที่แนบมา:

1. ระบุรหัส task (`CR-201` หรือ `CR-202`) และระดับความเร่งด่วน (`SLA-Red` หรือ `SLA-Amber`)
2. สรุปรหัส Business Rule ที่เกี่ยวข้อง (`BR-01..03` หรือ `EC-01..03`) ไม่เกิน 3 บรรทัด
3. ระบุชื่อไฟล์โค้ดเป้าหมายที่จะต้องตรวจสอบหรือแก้ไข

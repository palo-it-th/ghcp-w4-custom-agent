---
name: test-matrix-designer
description: "ใช้เมื่อต้องเขียนตาราง Test Cases ระบุข้อมูลที่ใช้ทดสอบและผลที่ควรได้ให้ครอบคลุมค่าขอบเขต พร้อมบันทึกบั๊กที่พบจากการอ่านโค้ดเทียบกับใบงานและ Business Rule"
---

# Sprint 2 Release Gate Test Matrix Skill (QA)

เมื่อได้รับโจทย์ให้ออกแบบชุดทดสอบสำหรับ `CR-201` หรือ `CR-202`:

1. **เปิดอ่านเอกสารนโยบายและตรวจโค้ดจริง:**
   - อ่านกฎธุรกิจใน `docs/policies/finance-and-sla-policy.md` (`BR-01..03` หรือ `EC-01..03`) และใบงานใน `docs/change-requests/`
   - เปิดอ่านไฟล์ `ui/preview.html` เพื่อหาจุดที่โค้ด Sprint 1 ปัจจุบันยังทำงานขัดกับกฎ
2. **ตรวจตามเกณฑ์ใน [QA BVA Checklist](references/qa-bva-checklist.md)**
3. **จัดทำเอกสารตามโครงสร้างใน [Test Matrix Template](assets/test-matrix-template.md):**
   - บันทึกไฟล์ลงใน `outputs/qa/cr-201-test-cases.md` (สำหรับ `CR-201`) หรือ `outputs/qa/cr-202-test-cases.md` (สำหรับ `CR-202`)

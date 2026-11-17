---
name: release-gate-audit
description: "ใช้เมื่อต้องตรวจเอกสาร สเปก เคสทดสอบ หรือโค้ดหน้าเว็บก่อนนำระบบขึ้นใช้งานจริง โดยเทียบกับ Business Rule แล้วทำตารางว่าข้อไหนถูกต้อง ข้อไหนต้องแก้ และเพราะอะไร"
---

# Sprint 2 Release Gate Audit Skill (Reviewer & Subagent)

เมื่อได้รับคำขอให้ตรวจสอบ (Audit / Review) เอกสารร่าง (`docs/drafts/`), เอกสาร Spec ของ BA (`outputs/ba/`), ตาราง Test Cases ของ QA (`outputs/qa/`) หรือโค้ด UI ของ Dev (`ui/preview.html`):

1. เปิดอ่านกฎธุรกิจที่เป็นทางการใน `docs/policies/finance-and-sla-policy.md` (`BR-01..03` และ `EC-01..03`) และเกณฑ์การตรวจใน [Audit Rules](references/audit-rules.md)
2. เปิดอ่านไฟล์เป้าหมายที่ผู้ใช้สั่งให้ตรวจ
3. แสดงผลลัพธ์เป็นตาราง **Release Gate Audit Findings** เสมอ โดยระบุคอลัมน์ดังนี้:
   - **หัวข้อ/รหัสกฎที่ตรวจ (`BR-xx` / `EC-xx`)**
   - **เกณฑ์ที่ถูกต้องตาม Policy**
   - **สิ่งที่พบจริงในไฟล์ที่ตรวจ**
   - **สถานะ (`PASS` / `POLICY VIOLATION`)** พร้อมคำแนะนำสั้นๆ
4. ห้ามแก้ไขไฟล์ต้นฉบับด้วยตัวเอง ให้สรุปผลการตรวจเพื่อให้เจ้าของงานตรวจสอบเท่านั้น

---
name: cr-spec-writer
description: "ใช้เมื่อต้องเขียนสเปกจากใบงานขอแก้ไขระบบ โดยเทียบว่าโค้ดทำงานอย่างไร Business Rule ต้องการอะไร แล้วสรุปสิ่งที่ต้องเปลี่ยนและเงื่อนไขการตรวจรับ"
---

# Sprint 2 Change Request Specification Skill (BA)

เมื่อได้รับโจทย์ให้เขียนเอกสาร Change Request Specification (`CR-201` หรือ `CR-202`):

1. **เปิดอ่านเอกสารต้นทางครบทั้ง 3 จุด:**
   - อ่าน Business Rule ที่อนุมัติแล้วใน `docs/policies/finance-and-sla-policy.md` (`BR-01..03` หรือ `EC-01..03`)
   - อ่านใบงานใน `docs/change-requests/CR-201-booking-deposit.md` หรือ `docs/change-requests/CR-202-ecommerce-promo.md`
   - เปิดอ่านโค้ดปัจจุบันใน `ui/preview.html` เพื่อดูว่าโค้ด Sprint 1 กำลังทำงานผิดจากกฎข้อใดบ้าง
2. **ตรวจตามเกณฑ์ใน [BA CR Checklist](references/ba-cr-checklist.md)**
3. **จัดทำเอกสารตามโครงสร้างใน [CR Spec Template](assets/cr-spec-template.md):**
   - บันทึกไฟล์ลงใน `outputs/ba/cr-201-spec.md` (สำหรับ `CR-201`) หรือ `outputs/ba/cr-202-spec.md` (สำหรับ `CR-202`)

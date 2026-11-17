# CR-202 · ระบบคำนวณโค้ดส่วนลดแคมเปญ 11.11 (`SWEET11`) และการควบคุมตะกร้าสินค้า (`Project ชานมหวานร้อย`)

- **Ticket ID:** `CR-202`
- **Project:** `Project ชานมหวานร้อย` · ระบบร้านค้าออนไลน์ (E-commerce App)
- **Priority / SLA:** `SLA-Amber` (ต้องเสร็จทันแคมเปญ 11.11 ในสปรินต์นี้)
- **Target Code File:** `ui/preview.html` (แท็บ `Project ชานมหวานร้อย · E-commerce App`)
- **Policy Reference:** `docs/policies/finance-and-sla-policy.md` (`EC-01`, `EC-02`, `EC-03`)

## ปัญหาที่พบในโค้ด Sprint 1 ปัจจุบัน (`ui/preview.html`)

ทีมส่งโค้ดหน้าร้านค้าและคำนวณตะกร้าจาก Sprint 1 ไว้ใน `ui/preview.html` แล้ว แต่เมื่อตรวจเทียบกับนโยบายแคมเปญ 11.11 (`docs/policies/finance-and-sla-policy.md`) พบจุดที่ยังผิดอยู่ 4 จุด:

1. **โค้ดส่วนลด `SWEET11` ลดซ้อนทับสินค้าที่ลด `-50%` อยู่แล้วได้ (ขัดกับ `EC-01`):**
   - ในโค้ดปัจจุบัน เมื่อเลือกสินค้า `Lolito Luxury Big Sofa` (ซึ่งลด `-50%` อยู่แล้ว) แล้วกรอกโค้ด `SWEET11` ระบบยอมลดเพิ่มอีก 10% ซึ่งทำให้บริษัทขาดทุน!
2. **ปรับจำนวนสินค้าเกิน 5 ชิ้น หรือต่ำกว่า 1 ชิ้นได้ (ขัดกับ `EC-02`):**
   - ตัวนับจำนวนสินค้าในโค้ดปัจจุบันอนุญาตให้กดเพิ่มได้ถึง `99` ชิ้น โดยไม่ได้ล็อกเพดานไว้ที่ `1–5` ชิ้นต่อรายการ
3. **คำสะกดป้ายเรียงลำดับและคำอธิบายสินค้าโซฟายังผิดอยู่ (ขัดกับ `EC-03`):**
   - ป้ายกำกับ Dropdown เรียงลำดับสะกดผิดเป็น **`"Short by"`** แทนที่จะเป็น `"Sort by"`
   - คำอธิบายของโซฟา `Asgaard Sofa` ยังแสดงข้อความลำโพงพกพา **`"Kilburn portable active stereo speaker... Marshall"`**
4. **กรองหมวดหมู่ที่ไม่มีสินค้าแล้วหน้าจอว่างเปล่า (ขัดกับ `EC-03`):**
   - เมื่อเลือกตัวกรองหมวดหมู่ `Lighting (0 items)` พื้นที่รายการสินค้าว่างเปล่าไปเลย ไม่มีข้อความ Empty State หรือปุ่ม `Reset Filters`

## สิ่งที่แต่ละบทบาทต้องทำใน Lab 4.2 & 4.4

- **BA (`ba-analyst`):** ใช้ Skill `cr-spec-writer` อ่านไฟล์นี้คู่กับ `docs/policies/finance-and-sla-policy.md` และ `ui/preview.html` เพื่อเขียนเอกสาร **Change Request Functional Spec (`outputs/ba/cr-202-spec.md`)** ที่ระบุตารางเปรียบเทียบ *พฤติกรรมเดิมในโค้ด Sprint 1 vs พฤติกรรมใหม่ตามกฎ `EC-01..03`* พร้อม Acceptance Criteria
- **QA (`qa-inspector`):** ใช้ Skill `test-matrix-designer` อ่านนโยบาย `EC-01..03` และตรวจโค้ด `ui/preview.html` เพื่อสร้าง **Test Case Matrix & Sprint 1 Bug Log (`outputs/qa/cr-202-test-cases.md`)** ที่ครอบคลุมการซ้อนโค้ด `SWEET11` ในสินค้าแต่ละระดับส่วนลด และค่าขอบเขตจำนวนสินค้า (`0, 1, 5, 6` ชิ้น)
- **Dev (`dev-builder`):** ใช้ Skill `ui-implementer` แก้ไขโค้ดส่วน E-commerce App ใน `ui/preview.html` ให้บล็อกโค้ด `SWEET11` กับสินค้าลด `-50%` (`EC-01`), ล็อกจำนวนสินค้าไว้ที่ `1–5` ชิ้น (`EC-02`), แก้คำผิด `"Sort by"` และคำอธิบายโซฟา รวมถึงเพิ่ม Empty State พร้อมปุ่ม `Reset Filters` (`EC-03`)

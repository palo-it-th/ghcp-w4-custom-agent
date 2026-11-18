# Envydia Sprint 2 · แล็บที่ 4: Custom Agents และ Skills

ยินดีต้อนรับกลับสู่ทีม Envydia ในช่วง Sprint 2 คุณยังไม่โดน layoff แม้หุ้นบริษัทจะตกเล็กน้อยเพราะข่าวฉาวก็ตาม 
ก่อนนำระบบขึ้น Production ทีม Finance และ Marketing ออกนโยบายใหม่ พร้อม Customer Requirement สองรายการสำหรับแก้บั๊กในเว็บแอปจาก Sprint 1

- **`CR-201` · Project หมูกระทะ (Booking App):** ปรับการคำนวณมัดจำตามจำนวนผู้จอง กำหนดเวลาชำระและการคืนเงิน และป้องกันการกดจองซ้ำ ตามกฎ `BR-01..03`
- **`CR-202` · Project ชานมหวานร้อย (E-commerce App):** จำกัดการใช้ส่วนลดและจำนวนสินค้า แก้ข้อความและคำอธิบายสินค้า และเพิ่ม Empty State ตามกฎ `EC-01..03`

นโยบายฉบับเต็มอยู่ที่ `docs/policies/finance-and-sla-policy.md`; รายละเอียดงานอยู่ใน `docs/change-requests/` และเว็บที่ใช้ตรวจหรือแก้อยู่ที่ `ui/preview.html`

## เริ่มต้นใช้งาน

1. เปิดโฟลเดอร์ `hands-on` นี้เป็น Workspace ใน VS Code แล็บนี้ไม่ต้องตั้งค่า MCP หรือเชื่อมต่อ Server ภายนอก
2. เปิด `ui/preview.html` ใน Browser เพื่อดูแอปของทั้งสองโปรเจกต์
3. ใน Chat ของ VS Code สร้าง New Chat แล้วเลือก **Session Target: Local** ก่อนเลือก Agent
4. เปิด [Review Card](labs/design-card.md) และ [Worksheet](labs/worksheet.md) ไว้จดสิ่งที่สังเกต

> **Handoffs:** ปุ่ม Handoff จะสลับไปยัง Agent ปลายทางและส่งคำขอทันที (`send: true`) ก่อนคลิก ให้ตรวจผลงานและตัดสินใจก่อนว่าจะส่งต่อหรือไม่

## กิจกรรม 5 ข้อ · 45 นาที

| Lab | เวลา | กิจกรรม |
|---|---:|---|
| [4.1 ทดลองตรวจงานด้วย Agent ที่เตรียมไว้](labs/4.1-why-agent-and-design-card.md) | 8 นาที | ตรวจเอกสารเดียวกันด้วย Agent มาตรฐานและ `release-auditor` โดยใช้เกณฑ์เดียวกัน แล้วบันทึกผลและเครื่องมือที่เห็น |
| [4.2 ใช้ Role Agent ที่เตรียมไว้](labs/4.2-build-role-agent-and-skills.md) | 12 นาที | เลือก BA, QA หรือ Dev ทำ `CR-201` หรือ `CR-202` และตรวจผลตาม Skill กับขอบเขตของ Agent |
| [4.3 ส่งงานต่อและแบ่งงานให้ Agent อื่น](labs/4.3-subagents-and-role-handoffs.md) | 10 นาที | ให้ `release-auditor` ตรวจเป็น Subagent ใน Context แยก และทดลองส่งต่องานระหว่าง BA → Dev → QA ผ่าน Handoff |
| [4.4 พิสูจน์รั้วกั้นและซ่อม Agent ที่พัง](labs/4.4-prove-guardrails-and-fix-misfires.md) | 10 นาที | ตรวจการกรองเครื่องมือ `tools:`, เรียนรู้ข้อจำกัดการกั้น path และซ่อม `broken-helper.agent.md` |
| [4.5 The Whole Ladder Check และ Share-out](labs/4.5-whole-ladder-check.md) | 5 นาที | สำรวจไฟล์ตั้งค่าในโปรเจกต์ ทบทวนว่าแต่ละกลไกทำอะไร และแชร์สิ่งที่ได้เรียนรู้ |

ทำตามลำดับ หากติดขัดเกิน 2 นาที ให้ขอความช่วยเหลือจากผู้สอน

## บทบาทและไฟล์สำคัญ

| บทบาท | Agent | Skill | งานหลัก |
|---|---|---|---|
| BA | `.github/agents/ba-analyst.agent.md` | `cr-spec-writer` | เปรียบเทียบใบงาน นโยบาย และโค้ด แล้วเขียน Spec |
| QA | `.github/agents/qa-inspector.agent.md` | `test-matrix-designer` | ออกแบบ Test Cases และบันทึกบั๊ก |
| Dev | `.github/agents/dev-builder.agent.md` | `ui-implementer` | แก้ `ui/preview.html` ตาม Acceptance Criteria |
| Auditor | `.github/agents/release-auditor.agent.md` | `release-gate-audit` | ตรวจผลงานแบบอ่านอย่างเดียว |

Agent แต่ละบทบาทมีชุด `tools:` ตามงานที่ได้รับมอบหมาย โดยต้องตรวจรายการเครื่องมือที่ Harness ส่งให้จริง ไม่สรุปว่าข้อจำกัดมีผลจากค่าในไฟล์เพียงอย่างเดียว

ไฟล์ประกอบอื่นที่ใช้ในเวิร์คช็อป:

- `.github/skills/` — Skills และไฟล์ Checklist / Template
- `.github/instructions/ui-delivery.instructions.md` — คำแนะนำเฉพาะไฟล์ UI และ outputs
- `.github/prompts/quick-cr-check.prompt.md` — Prompt ที่เรียกใช้ซ้ำได้
- `.github/copilot-instructions.md` — กติกากลางของ Workspace
- `.vscode/settings.json` — การตั้งค่า Approval Prompt สำหรับ `docs/frozen-scope/`
- `docs/drafts/sprint2-launch-draft.md` — เอกสารร่างที่มีข้อมูลผิด ใช้ใน Lab 4.1
- `docs/frozen-scope/release-signoff.md` — ไฟล์ห้ามแก้ ใช้สาธิตการป้องกันใน Lab 4.4
- `.github/agents/broken-helper.agent.md` — Agent ตัวอย่างที่ตั้งค่าผิดโดยเจตนา ใช้ฝึกซ่อมใน Lab 4.4

**→ เริ่มที่ [Lab 4.1](labs/4.1-why-agent-and-design-card.md)**

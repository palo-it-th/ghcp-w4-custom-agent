# Envydia Sprint 2 · Go-Live Control Room · แล็บที่ 4 (Custom Agents + Agent Skills)

ยินดีต้อนรับทุกท่านกลับสู่บริษัท Start-up ไฟแรง **"Envydia"** ในสัปดาห์ที่ 4 (Sprint 2 — 48 ชั่วโมงก่อนขึ้น Production)!
สัปดาห์ที่แล้ว (W3) เราสร้างหน้าจอชุดแรกของทั้งสองโปรเจกต์ไปเรียบร้อยแล้ว แต่ใน **Sprint 2** นี้ ทีมการเงิน (Finance) และทีมแคมเปญการตลาด (Marketing) เพิ่งประกาศนโยบายใหม่ใน `docs/policies/finance-and-sla-policy.md` และเปิดใบงานด่วน 2 ใบเพื่อแก้โค้ด Sprint 1 ใน `ui/preview.html` ที่ยังมีบั๊กอยู่:

- **`CR-201` · Project หมูกระทะ (Booking Restaurant App):** ปรับระบบคำนวณเงินมัดจำตามจำนวนท่าน (`BR-01`: `1–2 ท่าน = 0 บาท`, `3–6 ท่าน = 300 บาท`, `7–12 ท่าน = 1,000 บาท + บังคับกรอก Notes`, `13+ ท่าน = บล็อกการจองออนไลน์`), กำหนดเวลาชำระมัดจำภายใน `30 นาที` / คืนเงิน 100% เมื่อยกเลิกล่วงหน้า `>= 24 ชม.` (`BR-02`), และปิดปุ่มกดจองทันทีที่ส่งฟอร์มเพื่อกันการกดซ้ำ (`BR-03`)
- **`CR-202` · Project ชานมหวานร้อย (E-commerce App):** ระบบโค้ดส่วนลดแคมเปญ 11.11 (`EC-01`: โค้ด `SWEET11` ลดเพิ่ม 10% เฉพาะสินค้าที่ป้ายลดเดิม `< 50%` ห้ามซ้อนทับโซฟา `Lolito` ที่ลด `-50%` อยู่แล้ว!), ล็อกจำนวนสั่งซื้อ `1–5 ชิ้น` (`EC-02`), และแก้คำผิด `"Short by"` → `"Sort by"`, แก้คำอธิบายโซฟา `Asgaard` ที่หลุดข้อความลำโพง `Housepod Mini / Pineapple` พร้อมเพิ่ม Empty State (`EC-03`)

**Skill ทำงานได้อยู่แล้ว แล้วเราเพิ่ม Agent เมื่อไร?** (สไลด์ 3–4)
1. **ต้องการแค่วิธีทำงานซ้ำ → Skill ก็พอ:** ขั้นตอนเขียน Spec, ออกแบบ Test Matrix, แก้ UI และตรวจ Policy อยู่ใน Skills เรียกจาก Default Agent ก็ได้ ไม่จำเป็นต้องมี Custom Agent เพื่อทำงานเหล่านี้
2. **ต้องการโปรไฟล์บทบาท / เครื่องมือที่ทีมเลือกใช้ซ้ำ → เพิ่ม Custom Agent:** ผู้สร้างต้องเขียนไฟล์ได้ แต่ผู้ตรวจ `release-auditor` ระบุเฉพาะ `read`, `search` ใน `tools:` การเรียก Skill เดิมไม่ได้เปลี่ยนรายการเครื่องมือให้ ข้อ 4.1 จึงใช้ **Skill เดียวกันทั้งสองครั้ง** และข้อ 4.4 ตรวจว่า Harness กรองเครื่องมือจริงหรือไม่
3. **ต้องการส่งต่องาน → เลือกตามเหตุผล:** เปลี่ยนแค่ Checklist เรียก Skill ถัดไปได้; เปลี่ยนผู้รับผิดชอบ / โปรไฟล์ใช้ Agent หรือ Handoff; ต้องการ Context แยกใช้งาน Subagent โดยโปรไฟล์ที่ตั้งชื่อไว้ช่วยให้เรียกผู้ตรวจแบบเดิมซ้ำได้

> **ไม่ใช้คุณภาพคำตอบเป็นหลักฐานเรื่องสิทธิ์:** Skill ก็จัดตารางและระบุน้ำเสียงได้ ส่วนกฎซึนเดเระใน Repo Instructions เป็นเพียงตัวอย่างสอนลำดับความสำคัญของ Body ไม่ใช่เหตุผลที่ทุกงานต้องมี Agent ข้อจำกัด `tools:` ขึ้นกับ Harness และต้องตรวจรายการที่ส่งให้โมเดล ไม่รับประกันจากไฟล์ตั้งค่าอย่างเดียว

| สายงาน (Role) | Custom Agent (`.github/agents/`) | W4 Skills ที่เรียกใช้ (`.github/skills/`) | `tools:` ใน Frontmatter (และสิ่งที่ถูกตัดออก) |
|---|---|---|---|
| **BA (Business Analyst)** | `ba-analyst.agent.md` | `cr-spec-writer` | `['read', 'search', 'edit']` *(ไม่ระบุ `execute`; ตรวจผลจริงในข้อ 4.4)* |
| **QA (Quality Assurance)** | `qa-inspector.agent.md` | `test-matrix-designer` | `['read', 'search', 'edit']` *(ไม่ระบุ `execute`; ตรวจผลจริงในข้อ 4.4)* |
| **Dev (Developer)** | `dev-builder.agent.md` | `ui-implementer` | `['read', 'search', 'edit']` *(ไม่ระบุ `execute`; ตรวจผลจริงในข้อ 4.4)* |
| **Shared (ทุกสายงาน)** | `release-auditor.agent.md` | `release-gate-audit` | **Read-only:** `['read', 'search']` *(ไม่มีทั้ง `edit` และ `execute`!)* |

## ก่อนเริ่ม (2 นาที)

1. เปิดโฟลเดอร์ `hands-on` นี้เป็น **workspace** ใน VS Code (แล็บนี้ทำงานแบบ **Zero-MCP** ไม่ต้องตั้งค่า Token หรือต่อ Server ภายนอก!)
2. ลองเปิดไฟล์ `index.html` หรือ `ui/preview.html` ใน Browser เพื่อดูหน้าตาเว็บแอป Sprint 1 ที่มีทั้งแท็บ **Project หมูกระทะ** และ **Project ชานมหวานร้อย**
3. เปิด Copilot Chat → **New Chat**
4. เปิด [Prepared Agent Review Card](labs/design-card.md) และ [แบบบันทึกผล (Worksheet)](labs/worksheet.md) เตรียมไว้ข้างๆ

> **สำหรับ Local harness:** คำเตือน `Attribute 'skills' is ignored when running locally in VS Code.` เป็นข้อจำกัดของ Frontmatter ไม่ใช่การห้ามใช้ Skill เราเก็บ `skills:` ไว้สอนฝั่ง Copilot และใส่คำสั่งใน Body ของทั้ง 4 Agent ให้อ่าน `SKILL.md` ผ่านลิงก์สำหรับใช้งานทั้งสอง Harness แล้ว ไม่ต้องคัดลอกหรือเปลี่ยน `target` ดูรายละเอียดและวิธียืนยันการอ่านใน [ข้อ 4.2](labs/4.2-build-role-agent-and-skills.md)

## แล็บทั้ง 5 ข้อ · 45 นาที

| ข้อ | นาที | สิ่งที่จะทำและผลลัพธ์ (เชื่อมตรงกับสไลด์ W4) |
|---|---:|---|
| [4.1 Skill เดิม แต่เปลี่ยน Agent](labs/4.1-why-agent-and-design-card.md) | 8 | เทียบ Default Agent + `release-gate-audit` กับ `release-auditor` + **Skill เดิม** บนคำขอเดียวกัน แล้วตอบ 2 ข้อใน **Review Card** ที่สรุปการตั้งค่าไว้ให้แล้ว (สไลด์ 3–4, 15–16) |
| [4.2 ใช้ Role Agent ที่เตรียมไว้ (Agent + Skills)](labs/4.2-build-role-agent-and-skills.md) | 12 | เลือก BA / QA / Dev โดยไม่ต้องคัดลอกไฟล์ รัน `CR-201` หรือ `CR-202` แล้วแยกว่าส่วนไหนมาจาก Skill และโปรไฟล์ Agent เพิ่มอะไร (สไลด์ 5–8) |
| [4.3 หลาย Agents ทำงานร่วมกัน: Subagents & Handoffs](labs/4.3-subagents-and-role-handoffs.md) | 10 | ให้ Role Agent เรียก `release-auditor` เป็น **Subagent** แยก Context ตรวจผลงาน และฝึกส่งไม้ต่อ **BA → Dev → QA → Auditor** ด้วย Handoffs / การสลับ Agent กลางแชต (สไลด์ 7, 12–14) |
| [4.4 พิสูจน์รั้วกั้น `tools:` และซ่อม Agent ที่พัง](labs/4.4-prove-guardrails-and-fix-misfires.md) | 10 | ทดสอบสิ่งที่ `tools:` บล็อกได้จริง (`edit`, `execute`) vs สิ่งที่ `tools:` กั้นโฟลเดอร์ไม่ได้ (`docs/frozen-scope/`), ดูบันได 5 ขั้น และซ่อม `broken-helper.agent.md` (สไลด์ 8–11) |
| [4.5 เดินตรวจบันไดทั้ง 6 ขั้น & Share-out](labs/4.5-whole-ladder-check.md) | 5 | ตรวจไฟล์ครบทุกขั้นของโปรแกรมใน `.github/` (Prompt → Instructions → `applyTo` → Skills → Agents) และสรุปบทเรียน (สไลด์ 17) |

ทำตามลำดับได้เลย ถ้าติดอยู่ที่ขั้นตอนไหนเกิน 2 นาที ให้ยกมือเรียกผู้สอนทันที

## ไฟล์ที่ใช้ในแล็บ

| ไฟล์ / โฟลเดอร์ | หน้าที่ |
|---|---|
| `docs/policies/finance-and-sla-policy.md` | **ใหม่ใน W4:** นโยบายการเงินและโปรโมชัน Sprint 2 (`BR-01..03` และ `EC-01..03`) ที่เป็นแหล่งความจริงสูงสุด |
| `docs/change-requests/` | **ใหม่ใน W4:** ใบงาน `CR-201-booking-deposit.md` (`Project หมูกระทะ`) และ `CR-202-ecommerce-promo.md` (`Project ชานมหวานร้อย`) |
| `ui/preview.html` | **ใหม่ใน W4:** เว็บแอปอินเทอร์แอกทีฟของทั้ง 2 โปรเจกต์จาก Sprint 1 ที่มีบั๊กซ่อนอยู่ 8 จุด รอให้ BA เขียน Spec, QA จับบั๊ก และ Dev แก้ไข |
| `.github/copilot-instructions.md` | กติกากลางของโปรเจกต์ (มีกฎ Frozen Scope ข้อ 4 และกฎสไตล์การพูดซึนเดเระข้อ 5 สำหรับทดสอบว่า Body ของ Agent ชนะเมื่อขัดแย้งกัน) |
| `.github/instructions/ui-delivery.instructions.md` | Path-scoped instructions (`applyTo: "ui/**,outputs/**"`) จากขั้นที่ 4 ของบันได |
| `.github/prompts/quick-cr-check.prompt.md` | Reusable Prompt File สำหรับเช็กรหัสใบงานแบบเร็ว (ขั้นที่ 2 ของบันได) |
| `.github/skills/` | **Skills ชุดใหม่ของ W4** (`cr-spec-writer`, `test-matrix-designer`, `ui-implementer`, `release-gate-audit`) |
| `.github/agents/release-auditor.agent.md` | Custom Agent ผู้ตรวจสอบแบบ Read-only (`tools: ['read', 'search']` — ไม่มี `edit` และไม่มี `execute`) |
| `.github/agents/broken-helper.agent.md` | Custom Agent ที่มีจุดผิดพลาด 3 จุดตามสไลด์ 11 สำหรับฝึกวินิจฉัยและซ่อมในข้อ 4.4 |
| `.github/agents/` | Custom Agent ประจำสายงาน (`ba-analyst.agent.md`, `qa-inspector.agent.md`, `dev-builder.agent.md`) ที่เตรียมไว้พร้อมใช้ในข้อ 4.2 และส่งไม้ต่อในข้อ 4.3 |
| `.vscode/settings.json` | ตั้งค่า Approval Prompt (`chat.tools.edits.autoApprove`) สำหรับโฟลเดอร์ `docs/frozen-scope/` ในข้อ 4.4 |
| `docs/drafts/sprint2-launch-draft.md` | เอกสารร่างสรุปกติกา Sprint 2 ที่เขียนตัวเลขผิดเพี้ยนจากนโยบายจริง สำหรับทดสอบในข้อ 4.1 |
| `docs/frozen-scope/release-signoff.md` | เอกสารขอบเขตงานที่ล็อกแล้ว (ห้ามแก้ไข) สำหรับทดสอบ Guardrail ในข้อ 4.4 |

**→ เริ่ม [ข้อ 4.1 · Skill เดิม แต่เปลี่ยน Agent: ได้อะไรเพิ่ม?](labs/4.1-why-agent-and-design-card.md)**

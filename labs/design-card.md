# Prepared Agent Review Card · อ่านการตั้งค่า Agent ที่เตรียมไว้ (Lab 4.1 · 2 นาที)

> *"A skill is how to do the work. An agent is who does it, and what it may touch."* (สไลด์ 3 & 16)

**ไม่ต้องออกแบบใหม่หรือสร้างไฟล์:** เราเตรียม Agent ให้ครบแล้ว ใช้คำถามออกแบบ 6 ข้อจากสไลด์ 16 เป็นแนวทางตรวจการตั้งค่าที่เตรียมไว้ แล้วตอบ 2 ข้อท้ายการ์ด

---

## 1. เลือกบทบาทและเปิดไฟล์จริง

- [ ] **BA** — [ba-analyst.agent.md](../.github/agents/ba-analyst.agent.md)
- [ ] **QA** — [qa-inspector.agent.md](../.github/agents/qa-inspector.agent.md)
- [ ] **Dev** — [dev-builder.agent.md](../.github/agents/dev-builder.agent.md)

---

## 2. อ่าน 6 จุดที่เตรียมไว้ ไม่ต้องกรอกตารางใหม่

| จุดที่อ่าน | BA | QA | Dev |
|---|---|---|---|
| **1. Goal · Body** | เขียน CR Spec ใน `outputs/ba/` | เขียน Test Matrix / Bug Log ใน `outputs/qa/` | แก้ `ui/preview.html` แล้วรายงาน |
| **2. Skills it uses** | `cr-spec-writer` | `test-matrix-designer` | `ui-implementer` |
| **3. Tools & model** | `read`, `search`, `edit`; ไม่ระบุ `execute` | เหมือน BA | เหมือน BA |
| **4. Where it stops · Body** | เขียน Spec แล้ว `STOP`; ไม่แก้ UI | เขียน Test Matrix แล้ว `STOP`; ไม่แก้ UI | แก้ UI แล้ว `STOP`; ให้คนตรวจใน Browser |
| **5. Hands off / delegates to** | ส่งให้ Dev หรือ Auditor | ส่งให้ Auditor | ส่งให้ QA หรือ Auditor |
| **6. Check it** | Spec เทียบ As-Is / To-Be | เคสขอบเขตและบั๊กตรง Policy | ลอง UI ตามเคส `CR-201` / `CR-202` |

**แยกหน้าที่ของการตั้งค่าแต่ละส่วน:**
- Checklist, Template และวิธีทำงานอยู่ใน **Skill** เรียกจาก Agent มาตรฐานก็ได้
- `skills:` ใช้โหลด Skill ใน **Copilot harness** เท่านั้น; Local อาจเตือนว่า ignored แต่ Agent ทุกบทบาทมีลิงก์ใน Body สั่งให้อ่าน `SKILL.md` และทำตามไฟล์เดียวกันอยู่แล้ว ดู [คำอธิบายและวิธีตรวจในข้อ 4.2](4.2-build-role-agent-and-skills.md)
- `tools:` อยู่ใน **Agent profile**; ในข้อ 4.3 ต้องดูว่า Harness ใช้ข้อจำกัดจริงอย่างไร ไม่ดูแค่คำตอบปฏิเสธ
- `STOP` และ “แก้เฉพาะโฟลเดอร์นี้” ใน Body เป็น **asks** ไม่ใช่ตัวล็อกเครื่องมือหรือโฟลเดอร์
- ทั้ง 3 Agent ไม่ได้กำหนด `model:` จึงใช้ Model ที่เลือกในแชต
- ยังไม่เปิด Subagent ในตอนเริ่มต้น จะเพิ่ม `'agent'` ในข้อ 4.4; `handoffs:` เตรียมไว้แล้วสำหรับ Local harness

## 3. ตอบสั้นๆ เพียง 2 ข้อ

1. **ถ้าใช้ Skill เดียวกันกับ Default Agent งานส่วนไหนยังทำได้เหมือนเดิม?** ยกขั้นตอนหรือ Template 1 อย่างจาก `SKILL.md`:
   - คำตอบ:
2. **ทีมต้องการการตั้งค่าบทบาทหรือเครื่องมืออะไรเพิ่ม จึงคุ้มที่จะเลือก Agent นี้?** ยกค่าจาก `.agent.md` 1 อย่าง และระบุว่าเป็น **asks** หรือเป็นข้อจำกัดเครื่องมือที่ต้องตรวจใน Harness:
   - คำตอบ:

> ถ้าต้องการแค่เขียน Spec / Test Matrix / แก้ UI ด้วยวิธีเดิม และไม่ได้ต้องการเปลี่ยนบทบาทหรือชุดเครื่องมือ **ใช้ Skill อย่างเดียวก็พอ** ไม่จำเป็นต้องสร้าง Custom Agent ทุกงาน

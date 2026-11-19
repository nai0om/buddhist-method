# Buddhist Method — skill สำหรับ Claude

Skill ที่นำหลักธรรมในพระพุทธศาสนา 6 ข้อ มาใช้เป็นวินัยการทำงานของ Claude (หรือ LLM อื่นๆ) แต่ละหลักจับ failure mode ที่ LLM พังบ่อย: เชื่อ pattern แทนที่จะ verify, แก้อาการแทนที่จะแก้เหตุ, ยอมตามแรงกดดันแทนที่จะดูหลักฐาน

> 🇬🇧 Read [README.md](README.md) for the English version

## มีอะไรในนี้

Skill (`SKILL.md` + `references/`) ที่ให้ Claude ใช้เป็น checklist:

| หลัก | จับ failure mode |
|------|------------------|
| **กาลามสูตร** (Kalāma) | พูดข้อเท็จจริงจากความจำ training data โดยไม่ verify |
| **โยนิโสมนสิการ** (Yoniso) | แก้ที่อาการ ไม่ใช่ที่เหตุ |
| **สติ-สัมปชัญญะ** (Sati-Sampajañña) | ทำต่อจาก state ที่จำได้ ทั้งที่ของจริงเปลี่ยนแล้ว |
| **อนัตตา** (Anatta) | ติด draft แรก ไม่ยอมเขียนใหม่ |
| **ปหานะ** (Pahāna) | workaround ที่ซ่อนบั๊ก แทนที่จะตัดเหตุ |
| **อุเบกขา** (Upekkhā) | ยอมตาม user เมื่อโดน push หรือลนลานเมื่อเครื่องมือ fail |

พร้อม reference สำหรับสถานการณ์ยากกว่า:
- **อริยสัจ 4** เป็นกรอบ debug (`references/ariyasacca-debug.md`)
- **อปายโกศล** — รู้ว่ากำลังเสื่อม / anti sunk-cost
- **อัปปมาทะ** — ความไม่ประมาทในงานยาว
- **สัปปุริสธรรม 3 ใน 7** — รู้ตน / รู้กาล / รู้บริษัท
- **อัตถะ 2 ระดับ** — ทิฏฐธัมมิกัตถะ vs สัมปรายิกัตถะ (ประโยชน์ปัจจุบัน vs อนาคต)
- **มัชฌิมาปฏิปทา** — ทางสายกลางในการ sizing solution

## ทำไมเก็บชื่อบาลี/ไทย ไว้

ชื่อบาลีไม่ได้เก็บไว้เพื่อตกแต่ง แต่เป็น mnemonic — ชื่อสั้นที่ดึง pattern ครบทั้งชุดออกมาในทีเดียว "โยนิโสมนสิการ" ดึงวินัยทั้งหมดเรื่องการตั้งจิตไปหาเหตุ ขณะที่ "root cause analysis" ดึงไม่หมด

เหมือนวิศวกรเรียก "sigmoid" ไม่เรียก "ฟังก์ชันโค้งๆ" — ชื่อคือ infrastructure

skill นี้**ไม่ใช่**กรอบศาสนา ไม่ต้องเชื่อ ไม่ต้องปฏิบัติธรรมเพื่อใช้ มันคือ checklist ที่มีรากทางวัฒนธรรม นำเสนออย่างตรงไปตรงมา ถ้าอยากศึกษาหลักธรรมในความลึกจริงๆ อ่านพระไตรปิฎก — skill นี้ไม่ได้อ้างจะสอน

## วิธีใช้

### กับ Claude Code (แบบ plugin แนะนำ)

พิมพ์สองคำสั่งนี้ใน Claude Code:

```
/plugin marketplace add nai0om/buddhist-method
/plugin install buddhist-method@buddhist-method
```

Plugin จาก marketplace ภายนอกไม่อัปเดตเอง ถ้าอยากได้เวอร์ชันใหม่ เปิด `/plugin` เลือก **Marketplaces** เลือก `buddhist-method` แล้วกด **Enable auto-update** หรืออัปเดตเองด้วย `claude plugin marketplace update buddhist-method` ตามด้วย `claude plugin update buddhist-method@buddhist-method`

ถ้าเคยลงด้วย `git clone` มาก่อน ให้ลบ `~/.claude/skills/buddhist-method` ทิ้ง ไม่งั้น skill จะโหลดซ้ำสองตัว และเพราะแบบ plugin ไม่มีไฟล์ `~/.claude/skills/buddhist-method/SKILL.md` ทุก `CLAUDE.md` ที่ชี้ path นั้น (การลงแบบ manual ข้างล่างใส่ไว้ใน `~/.claude/CLAUDE.md` และหัวข้อ "ทำให้ active ตลอด" ก็มีอีกอัน) ให้ใช้ pointer นี้แทน:

```markdown
## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill
before responding.
```

### กับ agent อื่น (Codex, Cursor, Gemini CLI, Windsurf, …)

ลงผ่าน [Skills CLI](https://github.com/vercel-labs/skills):

```
npx skills add nai0om/buddhist-method
```

เติม `-g` เพื่อลงให้ user ทั้งเครื่องแทน project ปัจจุบัน หรือ `-a <agent>` เพื่อเลือก agent ตัวเดียว

### ลงเองแบบ manual กับ Claude Code

Paste prompt นี้ลง Claude Code — clone skill และ wiring `~/.claude/CLAUDE.md` ครั้งเดียวจบ:

```
Install the buddhist-method skill:
1. Run: git clone https://github.com/nai0om/buddhist-method ~/.claude/skills/buddhist-method
2. Open ~/.claude/CLAUDE.md (create it if it does not exist) and append:

## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill at
~/.claude/skills/buddhist-method/SKILL.md before responding.
```

หลังจากนั้น Claude Code จะ reference skill นี้โดยอัตโนมัติทุก session

### กับ Claude product อื่น

ที่ไหนรองรับ skill ก็วางไฟล์ลงได้เลย โครงสร้างมาตรฐาน (`SKILL.md` มี YAML frontmatter + `references/`)

### ใช้เป็น reference เฉยๆ ก็ได้

`SKILL.md` กับ `references/` อ่านเดี่ยวๆ ได้ ไม่ต้องมี Claude แต่ละหลักมี **trigger** (ใช้เมื่อไร) กับ **action** (ทำอะไร) ใช้เป็น checklist ส่วนตัวก็ได้

### ทำให้ active ตลอด (ทางเลือก)

ปกติ Claude จะโหลด skill on-demand — เห็น description แล้วตัดสินใจเองว่าจะอ่าน `SKILL.md` เต็มๆ ไหม ขึ้นกับงานตรงหน้า แบบนี้พอสำหรับการใช้งานทั่วไป และเก็บ context budget ไว้ใช้กับเรื่องอื่น

ถ้าอยากให้ skill active ตลอดไม่ว่าทำงานอะไร เพิ่ม pointer สั้นๆ ลงใน `CLAUDE.md`:

```markdown
## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill at
~/.claude/skills/buddhist-method/SKILL.md before responding.
```

ใส่ได้สองที่:

- **`CLAUDE.md` ใน project root** — ทำงานเฉพาะใน project นั้น
- **`~/.claude/CLAUDE.md`** — ทำงานทุก project ของ Claude Code

Pointer สั้นแค่ไม่กี่บรรทัด ไม่กิน context มาก Claude ยังโหลด body ของ skill ตอน trigger ติดเหมือนเดิม — แค่การันตีว่า skill อยู่ในสายตา Claude เสมอ

## โครงสร้าง

```
buddhist-method/
├── .claude-plugin/
│   ├── plugin.json                       # manifest ของ Claude Code plugin
│   └── marketplace.json                  # ให้ /plugin marketplace add หาเจอ
├── SKILL.md                              # 6 หลัก core + dispatch
├── README.md                             # เวอร์ชันอังกฤษ
├── README.th.md                          # ไฟล์นี้
├── LICENSE                               # MIT
└── references/
    ├── ariyasacca-debug.md               # อริยสัจ 4 เป็นกรอบ debug
    └── extended-principles.md            # 5 หลักรอง
```

## License

MIT — ใช้ แก้ไข แจกต่อได้เสรี ดู [LICENSE](LICENSE)

## ร่วมพัฒนา

เปิดรับ issue และ pull request โดยเฉพาะ:
- failure mode ที่ 6 หลักปัจจุบันยังจับไม่ได้
- trigger ที่ดีกว่า (สถานการณ์เฉพาะที่ควรกระตุ้นแต่ละหลัก)
- การแปลเป็นภาษาอื่นที่รากของหลักธรรมยังมีชีวิตอยู่

ถ้าจะเสนอหลักใหม่ ขอให้แสดง:
1. failure mode เฉพาะที่หลักนั้นจับ
2. trigger กับ action ที่เป็นรูปธรรม
3. ทำไมหลักที่มีอยู่ยังจับไม่ได้

มาตรฐานของ skill นี้คือ**ความกระชับ** — เพิ่มหลักง่าย แต่ที่ยากคือรักษาจำนวนให้น้อยพอที่จะใช้จริง

# Hướng dẫn thêm skill mới

Skill là file markdown mô tả cách làm một việc cụ thể. AI đọc và làm theo. Không cần code — chỉ cần viết rõ ràng.

---

## Cấu trúc file

```
skills/
└── tên-skill-của-bạn/
    └── SKILL.md          ← bắt buộc
    └── reference.md      ← tuỳ chọn, nếu SKILL.md quá dài
    └── scripts/          ← tuỳ chọn, nếu có script tiện ích
```

Tên thư mục = tên skill. Dùng `chữ-thường-nối-gạch`. Không dùng ký tự đặc biệt.

---

## SKILL.md tối thiểu

```markdown
---
name: tên-skill
description: Use when [mô tả KÍCH HOẠT — tình huống nào thì dùng skill này]
---

# Tiêu đề Skill

## Tổng quan

[Skill này dùng để làm gì, nguyên tắc cốt lõi là gì — 1-2 câu]

## Khi nào dùng

- [Tình huống A]
- [Tình huống B]
- Không dùng khi: [ngoại lệ rõ ràng]

## Cách làm

[Các bước cụ thể. Nếu có code, viết code thực tế — không phải placeholder]

## Lỗi thường gặp

| Lỗi | Cách sửa |
|-----|---------|
| ... | ... |
```

---

## Quy tắc viết `description`

`description` là thứ AI đọc đầu tiên để quyết định có load skill không. Viết sai thì skill sẽ không bao giờ được dùng.

**Bắt buộc:**
- Bắt đầu bằng `Use when...`
- Viết ngôi thứ ba (không dùng "tôi", "bạn")
- Mô tả **khi nào dùng** — không mô tả skill làm gì

**Không được:**
- Tóm tắt quy trình trong description (AI sẽ làm theo description thay vì đọc skill)
- Quá chung chung ("helps with code")

```yaml
# Sai — tóm tắt quy trình
description: Use for code review — check style, security, then approve or block

# Sai — quá chung
description: Helps with reviewing code

# Đúng — chỉ mô tả trigger
description: Use when completing a feature or before merging to main branch
```

---

## Ví dụ thực tế: Skill commit message

Bạn hay quên viết commit message đúng format? Tạo skill:

```
skills/
└── writing-commit-messages/
    └── SKILL.md
```

```markdown
---
name: writing-commit-messages
description: Use when about to create a git commit and need to write the commit message
---

# Writing Commit Messages

## Format

```
<type>: <mô tả ngắn>

<body tuỳ chọn — giải thích tại sao, không phải làm gì>
```

## Types

| Type | Khi nào |
|------|---------|
| `feat` | Thêm tính năng mới |
| `fix` | Sửa bug |
| `refactor` | Refactor, không thêm tính năng hay sửa bug |
| `test` | Thêm hoặc sửa test |
| `chore` | Cập nhật dependencies, config |
| `docs` | Chỉ thay đổi documentation |

## Ví dụ

```bash
feat: add dark mode toggle to settings page
fix: prevent double-submit on payment form
refactor: extract validation logic to separate module
```

## Quy tắc

- Dòng đầu tối đa 72 ký tự
- Dùng imperative mood ("add" không phải "added")
- Không kết thúc bằng dấu chấm
- Body giải thích WHY, không phải WHAT
```

---

## Ví dụ thực tế: Skill cho công cụ cụ thể

Ví dụ bạn hay dùng Prisma và muốn AI biết cách dùng đúng:

```markdown
---
name: using-prisma
description: Use when writing database queries, migrations, or schema changes in a project using Prisma ORM
---

# Using Prisma

## Quick reference

**Query:**
```typescript
const user = await prisma.user.findUnique({ where: { id } })
const users = await prisma.user.findMany({ where: { active: true } })
```

**Create/Update:**
```typescript
await prisma.user.create({ data: { email, name } })
await prisma.user.update({ where: { id }, data: { name } })
```

**Migration:**
```bash
npx prisma migrate dev --name describe-change
npx prisma generate
```

## Lưu ý

- Sau khi thay đổi schema, luôn chạy `prisma generate`
- Dùng `prisma.$transaction` khi cần atomic operations
- Không dùng `prisma.$queryRaw` trừ khi thực sự cần
```

---

## Các loại skill hữu ích cho solo dev

| Loại | Ví dụ |
|------|-------|
| **Tool cụ thể** | `using-prisma`, `using-stripe`, `using-redis` |
| **Quy ước project** | `project-conventions`, `api-response-format` |
| **Workflow lặp lại** | `writing-commit-messages`, `creating-migrations` |
| **Checklist** | `pre-deploy-checklist`, `security-checklist` |
| **Domain knowledge** | `payment-flow`, `auth-patterns` |

**Không cần viết skill cho:**
- Thứ đã được document tốt bởi library (AI đã biết)
- Convention chỉ dùng 1 lần
- Thứ có thể enforce bằng linter/config — dùng config thay vì skill

---

## Sau khi viết skill

**Kiểm tra hoạt động:**

1. Mở session Claude Code mới (hoặc `/clear`)
2. Gõ thứ gì đó nên trigger skill của bạn
3. AI có tự gọi skill không?

Nếu không trigger — kiểm tra lại `description`, thêm keyword rõ hơn.

**Nếu AI làm theo description thay vì nội dung skill:**

Description đang tóm tắt quy trình. Viết lại description chỉ mô tả trigger condition.

---

## Checklist nhanh trước khi dùng

- [ ] Tên thư mục dùng `chữ-thường-nối-gạch`
- [ ] `description` bắt đầu bằng `Use when...`
- [ ] `description` viết ngôi thứ ba
- [ ] `description` không tóm tắt quy trình
- [ ] Code trong skill là code thực tế, không phải placeholder
- [ ] Test trong session mới — skill có tự trigger không?

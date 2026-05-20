# Superpowers — Hướng dẫn Setup (Solo Dev Edition)

Đây là bản fork tối ưu cho **solo developer** — bỏ quy trình nặng của bản gốc, giữ lại những gì thực sự có giá trị: TDD, debugging có hệ thống, và verification trước khi báo xong.

---

## Cách hoạt động

Khi bắt đầu session, plugin tự inject skill `using-superpowers` vào context của AI. Từ đó, AI biết khi nào cần dùng skill nào và tự gọi chúng — bạn không cần làm gì thêm.

**Workflow thực tế:**

```
Bạn: "Thêm tính năng X"
AI: đánh giá scope → hỏi 1-3 câu nếu cần → viết plan → code TDD → verify → xong
```

Không có ceremony. Task đơn giản thì đi thẳng vào code.

---

## Cài đặt

### Claude Code

**Cách 1 — Marketplace chính thức (bản gốc):**

```bash
/plugin install superpowers@claude-plugins-official
```

**Cách 2 — Cài từ fork này (bản solo dev):**

```bash
/plugin install /đường/dẫn/đến/superpowers
```

Ví dụ nếu bạn clone vào `~/projects/superpowers`:

```bash
/plugin install ~/projects/superpowers
```

Sau khi cài, plugin tự kích hoạt từ session tiếp theo. Kiểm tra bằng cách gõ:

```bash
/plugin list
```

Bạn sẽ thấy `superpowers` trong danh sách.

---

### Cursor

Mở **Cursor Agent chat**, gõ:

```
/add-plugin superpowers
```

Hoặc vào **Settings → Plugins** → tìm kiếm "superpowers" → Install.

Để dùng bản fork này thay bản gốc, copy thư mục `.cursor-plugin/` vào project của bạn:

```
your-project/
└── .cursor-plugin/
    └── plugin.json   ← trỏ đến skills của fork này
```

---

### Codex CLI

Mở Codex CLI, vào plugin search:

```bash
/plugins
```

Tìm `superpowers` → chọn **Install Plugin**.

**Hoặc cài từ fork này:**

```bash
# Clone fork về máy nếu chưa có
git clone https://github.com/your-username/superpowers ~/projects/superpowers

# Cài plugin local
/plugin install ~/projects/superpowers
```

Bật multi-agent support trong `~/.codex/config.toml` (cần cho một số skill):

```toml
[features]
multi_agent = true
```

### Codex App

Vào **Plugins** trong sidebar → tìm `Superpowers` trong mục Coding → click **+** → làm theo hướng dẫn.

---

## Skills có trong bản này

| Skill | Khi nào dùng |
|-------|-------------|
| `brainstorming` | Trước khi code — hiểu yêu cầu, đánh giá scope |
| `writing-plans` | Có requirements → tạo task list hoặc plan doc |
| `executing-plans` | Thực thi plan từng bước |
| `test-driven-development` | Implement bất kỳ feature hoặc bugfix |
| `verification-before-completion` | Trước khi báo "xong" |
| `systematic-debugging` | Khi gặp bug, test fail, hành vi lạ |
| `finishing-a-development-branch` | Khi code xong, chọn merge/PR/giữ |
| `requesting-code-review` | Trước khi merge feature lớn |
| `receiving-code-review` | Nhận và xử lý feedback review |
| `using-git-worktrees` | Làm việc parallel trên nhiều branch |
| `dispatching-parallel-agents` | Chạy nhiều task độc lập song song |
| `writing-skills` | Viết skill mới cho hệ thống này |

---

## Workflow nhanh

### Task đơn giản (< 30 phút)

```
Bạn: "Fix bug X" hoặc "Thêm hàm Y"
AI: [hỏi tối đa 1 câu nếu thực sự cần] → code → test → commit
```

### Task vừa (vài giờ)

```
Bạn: "Xây dựng feature Z"
AI: hỏi 2-3 câu → confirm approach → tạo todo list → TDD từng bước → verify → commit
```

### Task phức tạp (multi-day)

```
Bạn: "Redesign module A"
AI: explore codebase → thảo luận design → viết spec doc → tạo plan → thực thi → review → merge
```

---

## Cập nhật

Vì đây là fork local, cập nhật bằng cách pull từ upstream nếu cần:

```bash
cd ~/projects/superpowers
git remote add upstream https://github.com/obra/superpowers
git fetch upstream
git merge upstream/main
```

Sau đó reinstall plugin:

```bash
# Claude Code
/plugin uninstall superpowers
/plugin install ~/projects/superpowers
```

---

## Khác biệt so với bản gốc

| Bản gốc | Bản solo dev này |
|---------|-----------------|
| Mọi task đều cần full spec | Có 3 tier: Quick / Standard / Complex |
| Viết design doc cho todo list | Chỉ viết doc cho task phức tạp |
| 3 agents/task (implementer + 2 reviewers) | Thực thi inline, không overhead |
| Hỏi nhiều câu một lượt | Tối đa 1-3 câu tuỳ scope |
| "1% chance → check skill" | Chỉ check skill khi clearly applies |

TDD, verification, và systematic debugging giữ nguyên — đây là chất lượng thực sự, không phải ceremony.

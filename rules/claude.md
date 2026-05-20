# Platform: Claude Code

## Tools
| Dùng khi | Tool |
|----------|------|
| Invoke skill | `Skill` |
| Track tasks | `TodoWrite` |
| Đọc file | `Read` |
| Tạo/ghi file | `Write` |
| Sửa file | `Edit` |
| Chạy lệnh | `Bash` |
| Tìm kiếm | `Grep`, `Glob` |
| Tìm kiếm web | `WebSearch`, `WebFetch` |

## Scope Assessment (làm trước tiên)

| Tier | Dấu hiệu | Hành động |
|------|----------|-----------|
| **Quick** | < 30 phút, yêu cầu rõ, 1-2 file | Tối đa 1 câu hỏi → code ngay |
| **Standard** | Vài giờ, có unknowns | 2-3 câu hỏi → confirm → code |
| **Complex** | Multi-day, nhiều unknowns | Full brainstorming skill |

## Bắt buộc
- **TDD**: viết test fail trước, sau đó mới implement
- **Verify**: chạy test/build trước khi báo xong — không claim thành công khi chưa có evidence
- **Không hỏi nhiều hơn scope cần**

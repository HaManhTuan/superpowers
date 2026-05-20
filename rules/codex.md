# Platform: Codex

## Tools
| Dùng khi | Tool |
|----------|------|
| Invoke skill | skills load natively — đọc và làm theo |
| Track tasks | `update_plan` |
| Spawn agent | `spawn_agent` + `wait_agent` + `close_agent` |
| Đọc file | native file tools |
| Chạy lệnh | native shell tools |

## Lưu ý Codex
- Multi-agent yêu cầu `multi_agent = true` trong `~/.codex/config.toml`
- Sandbox có thể chặn push/branch — commit xong rồi thông báo user push qua App UI
- Detached HEAD: không thể branch/push — dùng App's "Create branch" hoặc "Hand off to local"
- Đặt tên branch và viết commit message sẵn để user copy

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

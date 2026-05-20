# Platform: Cursor

## Tools
| Dùng khi | Tool |
|----------|------|
| Invoke skill | `skill` (chữ thường) |
| Track tasks | `todowrite` |
| Đọc file | `read_file` |
| Sửa file | `edit_file` |
| Tạo file | `create_file` |
| Chạy lệnh | `run_terminal_cmd` |
| Tìm kiếm code | `codebase_search`, `grep_search` |
| Tìm file | `file_search` |

## Lưu ý Cursor
- Cursor Agent tự động có file context — không cần đọc lại những file đã mở
- Dùng `codebase_search` trước khi `grep_search` cho keyword rộng
- Terminal command chạy trong project root

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

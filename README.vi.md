# AUDITOR 100X — Hướng dẫn tiếng Việt

Trang chủ tiếng Việt: [Giao diện Visual FoxPro](https://xulytiengviet.github.io/auditor/).

> Giao diện FoxPro là **tài liệu trực quan và mô phỏng cục bộ**. Trang GitHub Pages không gọi AI API, không kiểm tra bảo mật thật, không truy cập hoặc sửa repository của người xem.

## 1. Dự án làm gì?

Repository `xulytiengviet/auditor` chứa mã và báo cáo về **100x Agentic Engineer Pipeline**. Có hai phương án sử dụng:

1. **100x CLI** — kết hợp Claude Code và một harness, gồm **Phân tích → Triển khai → Kiểm thử → Rà soát**.
2. **DeepSeek multi-agent Python** — chạy các tác vụ nghiên cứu được cấu hình sẵn hoặc tệp JSON; giới hạn số tác vụ đồng thời bằng `--agents`.

Tên “auditor” ở đây không có nghĩa GitHub Pages là công cụ quét website trực tiếp.

## 2. Giao diện Visual FoxPro

- Project Manager: danh mục trái để chuyển giữa sáu nhóm tài liệu.
- Command Window: lệnh có thể sao chép; không tự thực thi.
- Property Inspector: tên, loại công cụ và chế độ hiện tại.
- Data Grid: tổng hợp các quality gates và thành phần hệ thống.
- Mô phỏng 4 bước: nhấn **F5** và xem nhật ký tiến trình; kết quả không phải PASS.
- Tải tệp TXT ghi nhật ký minh họa; không có dữ liệu API.
- Phím tắt: F1 trợ giúp, F5 mô phỏng, Esc về tổng quan, Alt+I mở cài đặt.

## 3. Chạy DeepSeek pipeline trên Windows PowerShell

Yêu cầu Python 3.9+, Git, mạng và một API key hợp lệ nếu thực thi thật.

~~~powershell
git clone https://github.com/xulytiengviet/auditor.git
cd auditor
python -m pip install httpx
cd pipeline
python runner.py --preset code_review --topic "Python code quality" --agents 5 --budget 5 --dry-run
~~~

Khi đã xem bản mô phỏng và muốn chạy thật, thiết lập khóa trong biến môi trường của PowerShell:

~~~powershell
$env:DEEPSEEK_API_KEY = "NHAP_KHOA_CUA_BAN"
python runner.py --preset code_review --topic "Python code quality" --agents 5 --budget 5
~~~

Không đưa khóa thật vào mã nguồn, commit hoặc website. Chạy thật có thể phát sinh chi phí.

## 4. Chạy 100x CLI với Bash

Khuyến nghị Linux/macOS hoặc WSL2 trên Windows. CLI yêu cầu thêm các chương trình hệ thống, trong đó có Claude Code CLI, `jq`, `git` và `bc`.

~~~bash
git clone https://github.com/xulytiengviet/auditor.git
cd auditor
chmod +x 100x
./100x doctor
./100x init
./100x gate
~~~

Để chạy luồng bốn bước, trong thư mục dự án mục tiêu sau khi có thể gọi lệnh `100x`, dùng:

~~~bash
100x run "Add input validation to all API endpoints"
~~~

## 5. Các cổng kiểm tra được mô tả

| Ngôn ngữ | Quality gates tham khảo |
|---|---|
| JavaScript / TypeScript | Prettier, ESLint, tsc, Vitest, Semgrep, Gitleaks, npm audit |
| Rust | cargo fmt, clippy, test, audit, Gitleaks |
| Go | gofmt, go vet, test, govulncheck, Gitleaks |
| Python | ruff, mypy, pytest, Semgrep, Gitleaks |

Các bước chỉ hoạt động nếu dependencies và cấu hình thực tế cho phép. Đọc log để xác định PASS/FAIL.

## 6. Tài liệu

- [README gốc](README.md)
- [Runbook](100x-Pipeline-Runbook.md)
- [Lệnh DeepSeek](PIPELINE-INSTRUCTIONS.md)
- [Sơ đồ pipeline](autonomous-pipeline.html)
- [Sơ đồ kiểm toán bảo mật](sc-audit-pipeline.html)
- [Trang landing tiếng Anh đã lưu](landing-modern.html)

## 7. Ghi nhận nguồn

Tệp [LICENSE](LICENSE) của repository sử dụng giấy phép **MIT**, ghi `Copyright (c) 2026 theluckystrike`. Mã gốc tham chiếu [theluckystrike/100xagenticdev](https://github.com/theluckystrike/100xagenticdev).

Giao diện chỉ lấy cảm hứng thị giác từ **Visual FoxPro / Windows 9x**; không chứa trình biên dịch FoxPro và không đại diện cho thương hiệu hay sản phẩm chính thức của Microsoft.

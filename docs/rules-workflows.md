# Phân tích chi tiết về Rules và Workflows

Dựa trên nội dung từ bài viết, dưới đây là phân tích chi tiết về **Rules (Quy tắc)** và **Workflows (Luồng công việc)**:

## 1. Rules (Quy tắc)

Rules là các hướng dẫn bạn tạo ra để điều chỉnh hành vi của Agent phù hợp với phong cách và yêu cầu cụ thể của bạn (ví dụ: "Luôn viết code bằng TypeScript", "Sử dụng Tailwind CSS").

- **Mục đích**: Cung cấp ngữ cảnh ổn định ở cấp độ câu lệnh (prompt level).
- **Phân loại & Lưu trữ**:
  - **Global Rules (Toàn cục)**: Áp dụng cho mọi dự án. Được lưu tại `~/.gemini/GEMINI.md`.
  - **Workspace Rules (Dự án)**: Áp dụng riêng cho dự án hiện tại. Được lưu trong thư mục `.agent/rules` hoặc thư mục gốc của dự án.
- **Cách kích hoạt**:
  - **Always On**: Luôn luôn tự động áp dụng.
  - **Manual**: Chỉ kích hoạt khi bạn nhắc đến tên quy tắc (ví dụ: `@rule-name`).
- **Định dạng**: File Markdown, giới hạn 12.000 ký tự. Có thể tham chiếu các file khác trong quy tắc bằng `@filename`.

## 2. Workflows (Luồng công việc)

Workflows là chuỗi các bước được định nghĩa trước để hướng dẫn Agent thực hiện một quy trình phức tạp hoặc lặp đi lặp lại (ví dụ: "Review code, chạy test, và merge PR").

- **Mục đích**: Hướng dẫn Agent ở cấp độ tiến trình (trajectory level) với các bước rõ ràng.
- **Cách sử dụng**:
  - Được định nghĩa trong các file `.md` (thường trong `.agent/workflows`).
  - Kích hoạt bằng lệnh gạch chéo `/tên-workflow` (ví dụ: `/deploy-wiki`).
- **Tính năng đặc biệt**:
  - **Lồng ghép**: Một Workflow có thể gọi một Workflow khác.
  - **Tự tạo**: Bạn có thể yêu cầu Agent tự tạo Workflow dựa trên lịch sử hội thoại của bạn.
  - **Tự động chạy**: Sử dụng chú thích `// turbo` hoặc `// turbo-all` để cho phép Agent tự động thực thi các lệnh terminal mà không cần hỏi lại.

## Tóm lại

- Sử dụng **Rules** khi bạn muốn Agent _luôn nhớ_ làm điều gì đó (như phong cách code, quy ước đặt tên).
- Sử dụng **Workflows** khi bạn muốn Agent _thực hiện_ một chuỗi hành động cụ thể theo trình tự.

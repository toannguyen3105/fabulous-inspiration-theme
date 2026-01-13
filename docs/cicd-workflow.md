# Quy trình CI/CD và Tài liệu

## 1. Kiểm soát chất lượng (CI - Continuous Integration)

Chúng ta sử dụng GitHub Actions để tự động kiểm tra chất lượng code trước khi merge.

### Workflow: Theme Check

- **File kích hoạt**: `.github/workflows/theme-check.yml`
- **Thời điểm chạy**:
  - Khi có Pull Request vào nhánh `main`.
  - Khi push code vào nhánh `develop` (hoặc các nhánh feature).
- **Hành động**:
  - Cài đặt môi trường Ruby và Shopify CLI.
  - Chạy lệnh `shopify theme check`.
- **Quy tắc**:
  - Nếu `theme check` báo lỗi (Error): GitHub sẽ chặn không cho Merge PR.
  - Phải sửa hết lỗi mới được Merge.

## 2. Tự dộng hóa tài liệu (CD - Continuous Deployment)

Hệ thống tài liệu được lưu trữ ngay trong mã nguồn để dễ dàng quản lý phiên bản cùng với code.

### Workflow: Sync Docs to Wiki

- **File kích hoạt**: `.github/workflows/deploy-wiki.yml`
- **Thời điểm chạy**: Khi có code mới được push vào nhánh `main` và có thay đổi trong thư mục `docs/`.
- **Hành động**:
  - Tự động copy nội dung từ thư mục `docs/` của repo.
  - Đẩy lên trang **GitHub Wiki** của dự án.
- **Lợi ích**:
  - Viết tài liệu bằng Markdown ngay trong VS Code.
  - Không cần vào giao diện web của Wiki để sửa thủ công.
  - Tài liệu luôn khớp với phiên bản code hiện tại.

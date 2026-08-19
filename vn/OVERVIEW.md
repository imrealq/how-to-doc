# Docs

Tạo/sửa file trong `docs/`: đọc [../AGENTS.md](../AGENTS.md) trước.

Đọc theo thứ tự `api/` → `database/` → `infrastructure/` — hiểu hệ
thống làm gì trước, rồi mới tra chi tiết dữ liệu/hạ tầng khi cần.

- `api/` — luồng nghiệp vụ theo domain, theo [000_templates/API_TEMPLATE.md](../000_templates/API_TEMPLATE.md), bắt đầu từ [api/000_OVERVIEW.md](api/000_OVERVIEW.md)
- `database/` — sơ đồ quan hệ + changelog schema, theo [000_templates/DATABASE_TEMPLATE.md](../000_templates/DATABASE_TEMPLATE.md)
- `infrastructure/` — thành phần hạ tầng, theo [000_templates/INFRASTRUCTURE_TEMPLATE.md](../000_templates/INFRASTRUCTURE_TEMPLATE.md), bắt đầu từ [infrastructure/000_TOPOLOGY.md](infrastructure/000_TOPOLOGY.md)

Template dùng chung cho mọi ngôn ngữ nằm ở [../000_templates/](../000_templates/)
(viết bằng tiếng Anh). Tạo file mới: copy đúng template tương ứng, giữ
nguyên số mục và thứ tự, viết nội dung bằng tiếng Việt.

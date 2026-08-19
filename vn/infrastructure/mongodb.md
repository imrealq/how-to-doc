# MongoDB

## 1. Lịch sử thay đổi

| Ngày       | Thay đổi                                                                                      | Vì sao                                                   |
| ---------- | --------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| 2026-08-19 | Thay `{ new: true }` (deprecated) bằng `{ returnDocument: 'after' }` ở mọi `findOneAndUpdate` | Mongoose cảnh báo option cũ sẽ bị loại bỏ                |
| 2026-08-12 | Thêm `checkOverload` — log số connection + memory mỗi 5s, cảnh báo nếu vượt `numCores * 5`    | Cần giám sát tải kết nối thủ công, chưa có công cụ ngoài |
| 2026-08-11 | Tạo `init.mongodb.js` (singleton), `maxPoolSize: 50`                                          | Kết nối chính, dùng chung toàn bộ hệ thống               |

## 2. Dùng để làm gì

Data store chính — lưu toàn bộ entity nghiệp vụ (Shop, Product, Cart,
Order...). Xem sơ đồ quan hệ đầy đủ ở
[database/SCHEMA.md](../database/SCHEMA.md).

## 3. Lưu ý vận hành

- Kết nối là **singleton** (`Database.getInstance()`) — chỉ 1 connection
  pool cho toàn bộ app, `maxPoolSize: 50`.
- Không có retry/backoff khi kết nối lỗi lúc khởi động — chỉ log lỗi ra
  console (`catch(err) => console.log(...)`), app vẫn tiếp tục chạy dù
  Mongo chưa sẵn sàng (request nào chạm DB sẽ tự timeout riêng lẻ).
- `checkOverload` chỉ log cảnh báo, không tự ngắt kết nối hay từ chối
  request khi vượt ngưỡng — mang tính quan sát, không phải cơ chế bảo vệ
  chủ động.

## 4. Liên kết và tham khảo

- `src/dbs/init.mongodb.js`
- `src/configs/config.mongodb.js`
- `src/helpers/check.connection.js`

**Được dùng bởi:** tất cả domain nghiệp vụ (Access, Product, Inventory,
Discount, Cart, Order) — qua Mongoose model của từng entity.

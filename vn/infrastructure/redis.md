# Redis

## 1. Lịch sử thay đổi

| Ngày       | Thay đổi                                                                 | Vì sao                                                         |
| ---------- | ------------------------------------------------------------------------ | -------------------------------------------------------------- |
| 2026-08-19 | Thêm `redisLock.js` (distributed lock, `SET NX PX` + Lua script release) | Cần khóa dùng chung giữa nhiều instance server khi trừ tồn kho |
| 2026-08-19 | Tạo `init.redis.js` (singleton, `ioredis`)                               | Kết nối Redis đầu tiên trong hệ thống                          |

## 2. Dùng để làm gì

Distributed lock cho thao tác trừ tồn kho — chặn 2 request cùng lúc trừ
kho 1 sản phẩm khi có nhiều instance server chạy song song. Xem
[inventory.md](../api/inventory.md).

## 3. Lưu ý vận hành

- Kết nối là **singleton** (`RedisDatabase.getInstance()`), không retry
  thủ công — dựa vào cơ chế reconnect mặc định của `ioredis`.
- Lỗi kết nối chỉ log ra console (`client.on('error', ...)`), không có
  circuit breaker hay fallback khi Redis không khả dụng — nếu Redis chết,
  `acquireLock` sẽ luôn thất bại (trả `null` sau khi hết retry), khiến
  toàn bộ thao tác trừ tồn kho bị chặn.
- Khóa có TTL 10s — nếu process giữ khóa crash giữa chừng mà chưa kịp
  release, khóa tự hết hạn sau 10s, không bị treo vĩnh viễn.

## 4. Liên kết và tham khảo

- `src/dbs/init.redis.js`
- `src/configs/config.redis.js`
- `src/helpers/redisLock.js`

**Được dùng bởi:**

- `Inventory` — `acquireLock`/`releaseLock` trong `reservationInventory`

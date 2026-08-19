# Overview

## Sơ đồ tổng — 1 đơn hàng đi qua bao nhiêu domain

```mermaid
flowchart LR
    Access["Access<br/>login"] --> Product["Product<br/>đăng bán"]
    Product -->|tự tạo| Inventory[Inventory]
    Cart["Cart<br/>thêm giỏ"] --> Checkout["Checkout<br/>tính giá"]
    Checkout -->|đọc giá thật| Product
    Checkout -->|verify + tính giảm| Discount[Discount]
    Checkout -->|giữ chỗ, có rollback| Inventory
    Checkout --> Order["Order<br/>lưu đơn"]
    Order -->|dọn giỏ| Cart
    Order -->|đánh dấu đã dùng| Discount
    Order -.hủy, hoàn kho.-> Inventory
```

Chi tiết từng domain: [access.md](access.md), [product.md](product.md),
[inventory.md](inventory.md), [discount.md](discount.md),
[cart.md](cart.md), [checkout.md](checkout.md), [order.md](order.md),
[core.md](core.md).

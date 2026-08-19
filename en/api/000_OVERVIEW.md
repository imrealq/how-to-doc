# Overview

## Overall diagram — how many domains 1 order passes through

```mermaid
flowchart LR
    Access["Access<br/>login"] --> Product["Product<br/>list item"]
    Product -->|auto-creates| Inventory[Inventory]
    Cart["Cart<br/>add to cart"] --> Checkout["Checkout<br/>price it"]
    Checkout -->|reads real price| Product
    Checkout -->|verify + apply discount| Discount[Discount]
    Checkout -->|reserve stock, with rollback| Inventory
    Checkout --> Order["Order<br/>save order"]
    Order -->|clear cart| Cart
    Order -->|mark as used| Discount
    Order -.cancel, release stock.-> Inventory
```

Per-domain detail: [access.md](access.md), [product.md](product.md),
[inventory.md](inventory.md), [discount.md](discount.md),
[cart.md](cart.md), [checkout.md](checkout.md), [order.md](order.md),
[core.md](core.md).

# WitleShop Online Retail System — ERD

Database/Data Analysis assignment for the WitleShop online retail case study.

## Overview

This repository contains the Entity-Relationship Diagram (ERD) and supporting documentation for the database structure described in the assignment brief.

The design covers:

- Customers and their registered delivery addresses
- Products, categories, and suppliers
- Customer orders
- Order line items
- Payments
- Deliveries

## ERD

The complete ERD is available in [`erd/ERD.md`](erd/ERD.md). GitHub renders the Mermaid diagram directly in the file.

### Main relationships

| Relationship | Cardinality | Purpose |
|---|---|---|
| Customer → Address | 1:M | A customer can register multiple delivery addresses. |
| Customer → Order | 1:M | A customer can place multiple orders. |
| Category → Product | 1:M | Each product belongs to one category. |
| Supplier → Product | 1:M | Each product is supplied by one supplier. |
| Order → OrderItem | 1:M | An order can contain multiple products. |
| Product → OrderItem | 1:M | A product can appear in multiple orders. |
| Order ↔ Product | M:N | Resolved through `OrderItem`. |
| Order → Payment | 1:1 | Each order has one payment record. |
| Order → Delivery | 1:1 | Each order has one delivery record. |
| Address → Delivery | 1:M | A registered address can be used for multiple deliveries. |

## Entities

### Customer
- `CustomerID` — Primary Key
- `FullName`
- `Email` — Unique
- `PhoneNumber`
- `RegistrationDate`

### Address
- `AddressID` — Primary Key
- `CustomerID` — Foreign Key
- `AddressLine1`
- `AddressLine2`
- `City`
- `Province`
- `PostalCode`

### Category
- `CategoryID` — Primary Key
- `CategoryName`

### Supplier
- `SupplierID` — Primary Key
- `SupplierName`

### Product
- `ProductID` — Primary Key
- `ProductName`
- `Description`
- `Price`
- `StockQuantity`
- `CategoryID` — Foreign Key
- `SupplierID` — Foreign Key

### Order
- `OrderID` — Primary Key
- `CustomerID` — Foreign Key
- `OrderDate`
- `OrderStatus` — Pending, Shipped, Delivered, Cancelled
- `TotalAmount`

### OrderItem
- `OrderItemID` — Primary Key
- `OrderID` — Foreign Key
- `ProductID` — Foreign Key
- `Quantity`
- `UnitPrice`

`OrderItem` resolves the many-to-many relationship between orders and products.

### Payment
- `PaymentID` — Primary Key
- `OrderID` — Foreign Key, Unique
- `PaymentDate`
- `PaymentMethod` — Card, EFT, PayFast
- `PaymentStatus`
- `AmountPaid`

### Delivery
- `DeliveryID` — Primary Key
- `OrderID` — Foreign Key, Unique
- `AddressID` — Foreign Key
- `DeliveryDate`
- `DeliveryStatus`
- `CourierName`
- `TrackingNumber`

## Important modelling decision: delivery address

The assignment requires a delivery to use one of the customer's registered addresses. The model therefore connects `Delivery.AddressID` to `Address.AddressID`, while `Address.CustomerID` identifies the customer who owns the registered address. `Delivery.OrderID` identifies the order being delivered.

This preserves the assignment's requirement without introducing a separate `DeliveryAddress` entity.

## Important modelling decision: Order–Product M:N

An order can contain multiple products, and a product can appear in multiple orders. This is a many-to-many relationship, so it is resolved using the associative entity `OrderItem`.

`OrderItem` also stores `Quantity` and `UnitPrice`, which are attributes of the individual product line in an order.

## Assignment alignment

The ERD identifies the entities, primary keys, foreign keys, relationships, and cardinalities requested by the assignment brief. The design stays within the scope of the supplied WitleShop case study and does not add unrelated e-commerce entities.

## Files

```text
witleshop-erd/
├── README.md
├── erd/
│   ├── ERD.md
│   └── witleshop-erd.mmd
└── docs/
    └── relational-design.md
```

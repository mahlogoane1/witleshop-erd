# Relational Design Notes

## Primary keys

| Entity | Primary key |
|---|---|
| Customer | CustomerID |
| Address | AddressID |
| Category | CategoryID |
| Supplier | SupplierID |
| Product | ProductID |
| Order | OrderID |
| OrderItem | OrderItemID |
| Payment | PaymentID |
| Delivery | DeliveryID |

## Foreign keys

| Entity | Foreign key | References |
|---|---|---|
| Address | CustomerID | Customer.CustomerID |
| Product | CategoryID | Category.CategoryID |
| Product | SupplierID | Supplier.SupplierID |
| Order | CustomerID | Customer.CustomerID |
| OrderItem | OrderID | Order.OrderID |
| OrderItem | ProductID | Product.ProductID |
| Payment | OrderID | Order.OrderID |
| Delivery | OrderID | Order.OrderID |
| Delivery | AddressID | Address.AddressID |

## Constraints represented by the design

- Customer.Email is unique.
- Payment.OrderID is unique, supporting the assignment's 1:1 Order–Payment relationship.
- Delivery.OrderID is unique, supporting the assignment's 1:1 Order–Delivery relationship.
- Product belongs to one Category and one Supplier.
- Delivery references a registered Address.
- OrderItem resolves the Order–Product many-to-many relationship.

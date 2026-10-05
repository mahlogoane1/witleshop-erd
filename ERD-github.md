# WitleShop ERD

## Entity-Relationship Diagram

```mermaid
erDiagram
    CUSTOMER ||--|{ ADDRESS : registers
    CUSTOMER ||--|{ ORDER : places
    CATEGORY ||--|{ PRODUCT : contains
    SUPPLIER ||--|{ PRODUCT : supplies
    ORDER ||--|{ ORDER_ITEM : contains
    PRODUCT ||--|{ ORDER_ITEM : appears_in
    ORDER ||--|| PAYMENT : has
    ORDER ||--|| DELIVERY : has
    ADDRESS ||--o{ DELIVERY : used_for

    CUSTOMER {
        int CustomerID PK
        string FullName
        string Email UK
        string PhoneNumber
        date RegistrationDate
    }

    ADDRESS {
        int AddressID PK
        int CustomerID FK
        string AddressLine1
        string AddressLine2
        string City
        string Province
        string PostalCode
    }

    CATEGORY {
        int CategoryID PK
        string CategoryName
    }

    SUPPLIER {
        int SupplierID PK
        string SupplierName
    }

    PRODUCT {
        int ProductID PK
        string ProductName
        string Description
        decimal Price
        int StockQuantity
        int CategoryID FK
        int SupplierID FK
    }

    ORDER {
        int OrderID PK
        int CustomerID FK
        date OrderDate
        string OrderStatus
        decimal TotalAmount
    }

    ORDER_ITEM {
        int OrderItemID PK
        int OrderID FK
        int ProductID FK
        int Quantity
        decimal UnitPrice
    }

    PAYMENT {
        int PaymentID PK
        int OrderID FK, UK
        date PaymentDate
        string PaymentMethod
        string PaymentStatus
        decimal AmountPaid
    }

    DELIVERY {
        int DeliveryID PK
        int OrderID FK, UK
        int AddressID FK
        date DeliveryDate
        string DeliveryStatus
        string CourierName
        string TrackingNumber
    }
```

## Cardinality notes

- One customer registers one or more addresses.
- One customer places one or more orders.
- One category contains one or more products.
- One supplier supplies one or more products.
- One order contains one or more order items.
- One product can appear in zero or many order items.
- Order and Product are therefore M:N through OrderItem.
- Each order has exactly one payment and each payment belongs to exactly one order.
- Each order has exactly one delivery and each delivery belongs to exactly one order.
- A registered address can be used for zero or many deliveries.

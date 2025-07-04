# # 🛒 E-commerce System - Fawry Quantum Internship Challenge

A comprehensive e-commerce system implementation in Java that handles product management, shopping cart functionality, and checkout processes with advanced features like expiration dates, shipping calculations, and inventory management.

## 📋 Table of Contents

- [Features](#features)
- [System Architecture](#system-architecture)
- [Installation & Setup](#installation--setup)
- [Usage Examples](#usage-examples)
- [API Reference](#api-reference)
- [Test Cases](#test-cases)
- [Design Patterns](#design-patterns)
- [Assumptions](#assumptions)
- [Contributing](#contributing)

## ✨ Features

### Core Functionality
- ✅ **Product Management** - Define products with name, price, and quantity
- ✅ **Expiration Handling** - Support for perishable products (Cheese, Biscuits) vs non-perishable (TV, Mobile)
- ✅ **Shipping Logic** - Smart shipping for physical products with weight-based calculations
- ✅ **Digital Products** - Support for non-shippable items (Mobile Scratch Cards)
- ✅ **Shopping Cart** - Add products with quantity validation
- ✅ **Checkout Process** - Complete order processing with receipt generation

### Advanced Features
- 🔒 **Inventory Management** - Real-time stock validation
- 📅 **Expiration Tracking** - Automatic expired product detection
- 📦 **Smart Shipping** - Weight-based shipping fee calculation
- 💰 **Payment Processing** - Balance validation and deduction
- 📊 **Receipt Generation** - Detailed checkout summaries
- 🚫 **Error Handling** - Comprehensive validation and error messages

## 🏗️ System Architecture

### Class Hierarchy

```
Product (Abstract)
├── PerishableProduct (Implements: Expirable, Shippable)
├── NonPerishableShippableProduct (Implements: Shippable)
└── DigitalProduct

Interfaces:
├── Expirable
├── Shippable
└── ShippingService
```

### Key Components

| Component | Responsibility |
|-----------|----------------|
| **Product** | Base class for all products |
| **Cart** | Shopping cart management |
| **Customer** | Customer information and balance |
| **ECommerceSystem** | Main system orchestrator |
| **ShippingService** | Shipping calculations and processing |

## 🚀 Installation & Setup

### Prerequisites
- Java 8 or higher
- No external dependencies required

### Quick Start

1. **Clone or download** the `ECommerceDemo.java` file
2. **Compile** the Java file:
   ```bash
   javac ECommerceDemo.java
   ```
3. **Run** the demo:
   ```bash
   java ECommerceDemo
   ```

## 💡 Usage Examples

### Basic Usage
```java
// Create products
Product cheese = new PerishableProduct("Cheese", 100, 10, LocalDate.now().plusDays(7), 0.2);
Product tv = new NonPerishableShippableProduct("TV", 500, 3, 15.0);
Product scratchCard = new DigitalProduct("Mobile Scratch Card", 10, 100);

// Create customer
Customer customer = new Customer("John Doe", 2000);

// Create cart and add items
Cart cart = new Cart();
cart.add(cheese, 2);
cart.add(tv, 1);
cart.add(scratchCard, 1);

// Checkout
ECommerceSystem ecommerce = new ECommerceSystem();
ecommerce.checkout(customer, cart);
```

### Challenge Example
```java
// Original challenge example
cart.add(cheese, 2);
cart.add(tv, 3);
cart.add(scratchCard, 1);
checkout(customer, cart);
```

**Expected Output:**
```
** Shipment notice **
2x Cheese 400g
3x TV 45000g
Total package weight 45.4kg

** Checkout receipt **
2x Cheese 200
3x TV 1500
1x Mobile Scratch Card 10
----------------------
Subtotal 1710
Shipping 474
Amount 2184
END.
```
#### PerishableProduct
```java
PerishableProduct(String name, double price, int quantity, LocalDate expirationDate, double weight)
```
- For products that expire and require shipping
- Examples: Cheese, Biscuits, Yogurt

#### NonPerishableShippableProduct
```java
NonPerishableShippableProduct(String name, double price, int quantity, double weight)
```
- For durable products that require shipping
- Examples: TV, Mobile, Laptop

#### DigitalProduct
```java
DigitalProduct(String name, double price, int quantity)
```
- For digital products that don't require shipping
- Examples: Mobile Scratch Cards, Game Cards

### Cart Operations

#### Adding Items
```java
cart.add(Product product, int quantity)
```
- Validates stock availability
- Checks expiration dates
- Throws `IllegalArgumentException` for invalid operations

#### Checkout Process
```java
ecommerce.checkout(Customer customer, Cart cart)
```
- Validates cart contents
- Calculates shipping fees
- Processes payment
- Updates inventory
- Generates receipt

## 🧪 Test Cases

The system includes comprehensive test cases covering:

### ✅ Success Scenarios
- **Mixed Cart Checkout** - Various product types
- **Digital Products Only** - No shipping required
- **Heavy Items** - High shipping costs
- **Perishable Products** - Expiration handling

### ❌ Error Scenarios
- **Empty Cart** - Validation error
- **Insufficient Balance** - Payment failure
- **Expired Products** - Blocked from purchase
- **Out of Stock** - Inventory validation
- **Invalid Quantities** - Stock limit enforcement

## 🎯 Design Patterns

### Strategy Pattern
- **ShippingService** interface allows different shipping strategies
- **StandardShippingService** implements weight-based calculations

### Factory Pattern
- Product creation through constructors
- Type-specific behavior through inheritance

### Template Method Pattern
- **Product** base class defines common behavior
- Subclasses implement specific logic

## 📝 Assumptions

### Business Logic
- **Base shipping fee**: 20 units + 10 units per kg
- **Weight units**: Kilograms for calculations, grams for display
- **Payment**: Immediate balance deduction
- **Inventory**: Real-time stock updates

### Technical Assumptions
- **Date handling**: LocalDate for expiration tracking
- **Precision**: Double for prices and weights
- **Concurrency**: Single-threaded operations assumed
- **Persistence**: In-memory storage only

### Product Categories
- **Perishable**: Cheese, Biscuits, Yogurt (expire + ship)
- **Non-Perishable**: TV, Mobile, Laptop (ship only)
- **Digital**: Scratch Cards, Game Cards (no shipping)

## 🔧 Error Handling

The system provides detailed error messages for:

| Error Type | Message Example |
|------------|----------------|
| Empty Cart | "Cart is empty" |
| Insufficient Balance | "Customer's balance is insufficient" |
| Expired Product | "Product Cheese is expired" |
| Out of Stock | "Product TV is out of stock" |
| Invalid Quantity | "Insufficient quantity for Cheese. Available: 5, Requested: 10" |

## 📊 Sample Output

```
=== ORIGINAL CHALLENGE EXAMPLE ===
Customer balance before checkout: 2000
** Shipment notice **
2x Cheese 400g
3x TV 45000g
Total package weight 45.4kg
** Checkout receipt **
2x Cheese 200
3x TV 1500
1x Mobile Scratch Card 10
----------------------
Subtotal 1710
Shipping 474
Amount 2184
Customer balance after payment: -184
END.
```
## 📄 License

This project is created for the Fawry Quantum Internship Challenge and is available for educational purposes.
---

**Developed for Fawry Quantum Internship Challenge** 🚀
```
Author: Yousef Hussien Awad | Date: July 2025 | Version: 1.0.0

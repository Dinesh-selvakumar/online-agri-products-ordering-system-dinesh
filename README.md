# Online Agri Products Ordering System

**Student:** Dinesh S | **Register No:** 2503917720521027 | **Course:** B.Tech | **Subject:** Software Engineering

A command-line application built with Python 3 and SQLite that lets farmers and buyers browse an agri products catalogue (seeds, fertilizers, pesticides, tools and produce), build a cart, place orders and track them, while staff manage products, stock and order status.

## Problem Statement and Objectives

Agri input suppliers who take orders by phone or on paper face wrong orders, wrong bills, stock mismatches and no way to follow an order after it is placed.

Objectives:
- Keep a product catalogue with price, unit and live stock.
- Register customers (farmers / buyers) with validated details.
- Build a cart and calculate the bill (GST and delivery fee) automatically.
- Place orders, reduce stock, and track each order until delivery.
- Reject invalid input with clear messages instead of crashing.

## Features / Modules Implemented

| Module | File | What it does |
|---|---|---|
| Validators | `aos/validators.py` | Name, email, phone, address, price, stock, quantity, category, unit and ID checks |
| Database | `aos/database.py` | SQLite connection and schema (5 tables) |
| Products | `aos/products.py` | Add, list, search, restock, remove products |
| Customers | `aos/customers.py` | Register and list customers |
| Cart | `aos/cart.py` | Add/remove items, stock checks, bill with GST and delivery fee |
| Orders | `aos/orders.py` | Place order, status updates, cancel, order history, active orders |
| CLI | `aos/cli.py` | Interactive menu with error handling |

Business rules:
- GST of 5% on the subtotal; delivery fee Rs. 60, free when the subtotal is Rs. 1000 or more.
- Between 1 and 100 of one product per order; a product cannot be added beyond its stock, and an out-of-stock product cannot be added.
- Stock is reduced when an order is placed and restored when an order is cancelled.
- Order status flow: Placed -> Packed -> Out for Delivery -> Delivered. Only a `Placed` order can be cancelled.
- A product that is part of an active order cannot be removed; product names and prices are saved with each order.

## Technology Stack and Tools

- Python 3 (standard library only: `sqlite3`, `unittest`, `datetime`, `re`, `math`)
- SQLite 3
- Git and GitHub for version control

## Prerequisites and Installation

1. Install Python 3.9 or newer (`python --version`).
2. Install Git (`git --version`).
3. Clone the repository:

```
git clone https://github.com/Dinesh-selvakumar/online-agri-products-ordering-system.git
cd online-agri-products-ordering-system
```

No external libraries are needed, so there is nothing else to install.

## How to Run the Application

```
python main.py
```

The program creates `agri_orders.db` in the current folder on first run (set the `AOS_DB` environment variable to use a different file). Choose an option by typing its number; type `m` to show the menu again and `0` to exit.

## Sample Inputs and Outputs

```
Enter choice: 1
Product name: Tomato Seeds
Category (Seeds/Fertilizers/Pesticides/Tools/Produce): Seeds
Unit (kg/litre/packet/piece/bag): packet
Price per unit (Rs.): 120
Stock quantity: 50
Product added with ID 1.

Enter choice: 9
Customer ID: 1
ID  Product                 Qty     Price    Amount
1   Tomato Seeds              2    120.00    240.00
2   Organic Compost           1    160.00    160.00
Subtotal : Rs. 400.00
GST (5%) : Rs. 20.00
Delivery : Rs. 60.00
Total    : Rs. 480.00

Enter choice: 8
Customer ID: 1
Product ID: 3
Quantity: 9
Error: Only 5 piece of 'Garden Spade' in stock.
```

## Testing Performed and Results

```
python -m unittest -v
```

36 tests cover validators, products, customers, cart and orders (valid input, invalid input and business rules). Result: **36 of 36 passed**.

## Known Limitations and Possible Future Enhancements

Limitations:
- Command-line interface only; one user at a time.
- No login or roles; payment is not processed.
- Single supplier; local SQLite database.

Future enhancements:
- Web front end (Flask) with farmer and admin login.
- Online payment integration (UPI / card).
- Seasonal offers, bulk-order discounts, and SMS/email order notifications.
- Report export to CSV/PDF.

## Team Details and Individual Contributions

| Member | Register No | Contribution |
|---|---|---|
| Dinesh S | 2503917720521027 | Individual project: design, implementation, testing, Git workflow and documentation |

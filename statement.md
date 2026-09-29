# Fresh Basket Grocery Store Application

This script is a simple desktop grocery billing application built using Python's **Tkinter** library. It allows users to browse an item catalog, add items to a virtual shopping cart with specific quantities, remove items, and generate a final structured invoice bill including taxes.

## Source Code

```python
import tkinter as tk
from tkinter import messagebox

# Grocery inventory items with format -> ID: [Name, Price]
items = {
    1: ["Milk", 2.50],
    2: ["Bread", 1.80],
    3: ["Eggs", 3.20],
    4: ["Chips", 10.50],
    5: ["Chocolate", 5.50],
    6: ["Apple", 4.00],
    7: ["Jam", 10.00],
    8: ["Curd", 15.65],
}

cart = {}

def add_to_cart():
    selected = item_list.curselection()
    if not selected:
        messagebox.showwarning("No item", "Please select an item first.")
        return
    item_id = list(items.keys())[selected[0]]
    qty = int(qty_box.get())
    cart[item_id] = cart.get(item_id, 0) + qty
    show_cart()

def remove_from_cart():
    selected = cart_list.curselection()
    if not selected:
        messagebox.showwarning("No item", "Select an item in the cart to remove.")
        return
    item_id = list(cart.keys())[selected[0]]
    del cart[item_id]
    show_cart()

def show_cart():
    cart_list.delete(0, tk.END)
    total = 0
    for item_id, qty in cart.items():
        name, price = items[item_id]
        cost = price * qty
        total += cost
        cart_list.insert(tk.END, f"{name} x{qty} = ₹{cost:.2f}")
    total_label.config(text=f"Subtotal: ₹{total:.2f}")

def checkout():
    name = name_entry.get().strip()
    phone = phone_entry.get().strip()
    
    if name == "":
        messagebox.showerror("Error", "Please enter your name.")
        return
    if not (phone.isdigit() and len(phone) == 10):
        messagebox.showerror("Error", "Phone number must be 10 digits.")
        return
    if len(cart) == 0:
        messagebox.showinfo("Empty cart", "Your cart is empty.")
        return
        
    subtotal = 0
    bill = f"Customer: {name}\nPhone: {phone}\n\n"
    for item_id, qty in cart.items():
        item_name, price = items[item_id]
        cost = price * qty
        subtotal += cost
        bill += f"{item_name} x{qty} = ₹{cost:.2f}\n"
        
    tax = subtotal * 0.05
    grand_total = subtotal + tax
    
    bill += "-" * 28
    bill += f"\nSubtotal: ₹{subtotal:.2f}"
    bill += f"\nTax (5%): ₹{tax:.2f}"
    bill += f"\nTotal Bill: ₹{grand_total:.2f}"
    bill += "\n\nThank you for shopping! Do visit again."
    
    messagebox.showinfo("Final Bill", bill)
    cart.clear()
    show_cart()

# Application Window Setup
window = tk.Tk()
window.title("Fresh Basket Grocery Store")
window.geometry("550x500")
window.config(bg="#eaf7ea")

tk.Label(window, text="FRESH BASKET GROCERY STORE", font=("Times New Roman", 16, "bold"), bg="#eaf7ea", fg="#2e7d32").pack(pady=10)

# Customer details section
details = tk.Frame(window, bg="#eaf7ea")
details.pack()

tk.Label(details, text="Name:", bg="#eaf7ea").grid(row=0, column=0, sticky="e")
name_entry = tk.Entry(details, width=25)
name_entry.grid(row=0, column=1, pady=3)

tk.Label(details, text="Phone:", bg="#eaf7ea").grid(row=1, column=0, sticky="e")
phone_entry = tk.Entry(details, width=25)
phone_entry.grid(row=1, column=1, pady=3)

# Middle Section for Catalog and Cart
middle = tk.Frame(window, bg="#eaf7ea")
middle.pack(pady=10)

# Left Side: Product List
left = tk.Frame(middle, bg="#eaf7ea")
left.grid(row=0, column=0, padx=10)

tk.Label(left, text="Items", font=("Times New Roman", 12, "bold"), bg="#eaf7ea").pack()
item_list = tk.Listbox(left, width=22, height=10)
for name, price in items.values():
    item_list.insert(tk.END, f"{name} - ₹{price:.2f}")
item_list.pack()

qty_row = tk.Frame(left, bg="#eaf7ea")
qty_row.pack(pady=5)
tk.Label(qty_row, text="Qty:", bg="#eaf7ea").pack(side="left")
qty_box = tk.Spinbox(qty_row, from_=1, to=20, width=5, state="readonly")
qty_box.pack(side="left")

tk.Button(left, text="Add to Cart", bg="#4caf50", fg="white", width=15, command=add_to_cart).pack()

# Right Side: Shopping Cart View
right = tk.Frame(middle, bg="#eaf7ea")
right.grid(row=0, column=1, padx=10)

tk.Label(right, text="Your Cart", font=("Times New Roman", 12, "bold"), bg="#eaf7ea").pack()
cart_list = tk.Listbox(right, width=26, height=10)
cart_list.pack()

total_label = tk.Label(right, text="Subtotal: ₹0.00", bg="#eaf7ea", font=("Times New Roman", 11, "bold"))
total_label.pack(pady=5)

tk.Button(right, text="Remove Item", bg="#e57373", fg="white", width=15, command=remove_from_cart).pack()

# Bottom Section: Final Checkout
tk.Button(window, text="Checkout", bg="#2e7d32", fg="white", font=("Times New Roman", 12, "bold"), width=20, command=checkout).pack(pady=10)

window.mainloop()
```

## Application Specifications

### 1. Features
* **Customer Identification**: Input fields for customer Name and a validated 10-digit Phone number.
* **Product Browsing**: A clean interface populated dynamically from an internal item inventory dictionary.
* **Quantity Controller**: A spinbox preventing keyboard input errors by constraining values between 1 and 20.
* **Dynamic Cart Operations**: Allows sequential addition and full removal of selected grocery elements.
* **Auto-calculating Subtotal**: Instantly updates visible running subtotals inside the application dashboard layout.
* **Taxation Summary**: Applies a **5% sales tax** dynamically upon calculation checkout actions.

### 2. UI Layout Elements
* **Theme Styling**: Uses soft-green color themes (`#eaf7ea` background, `#2e7d32` titles) fitting a "Fresh Grocery" ecosystem theme.
* **Typography**: Consistent implementation using "Times New Roman" styling fonts structured across logical visual headers.

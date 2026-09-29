# Fresh Basket Grocery 🛒

A super simple, text-based grocery cart program written in Python. 

I took a single file of messy spaghetti code and chopped it up into clean, separate modules so it’s actually easy to read, maintain, and update. The program handles welcoming the customer, displaying the inventory, updating item quantities, and calculating a 5% tax at checkout.

---

## 📂 Project Structure

Instead of stuffing all the code into one massive script, the logic is split into 4 clean, single-purpose files:

* **`config.py`**: Holds the core data, including the grocery items dictionary, the price list, and the empty shopping cart dictionary.
* **`customer.py`**: Handles the initial onboarding. It prints a big welcome message and prompts the shopper for their name and phone number.
* **`operations.py`**: The engine room. It contains the logic for looking up item IDs, adding items to the cart safely without crashing, and formatting the final bill.
* **`main.py`**: The central driver. It imports all the other modules and runs the main `while True` loop to keep the interactive menu ticking.

---

## 🚀 How to Run It

1. Open your terminal or command prompt in this project folder.
2. Run the main script:
   ```bash
   python main.py
   ```
3. Use the interactive menu prompts:
   * Press **`1`** to see what's currently in stock.
   * Press **`2`** to add an item to your bag using its ID.
   * Press **`3`** to double-check what you've picked so far.
   * Press **`4`** to grab your receipt, calculate tax, and close the program.

---

## ☁️ Running on Google Colab?

If you are running this project inside a Google Colab notebook and want to download all the files to your local machine as a single zip archive, paste this snippet into a new cell and run it:

```python
import zipfile
from google.colab import files

# Pack everything up real quick
files_to_zip = ["config.py", "customer.py", "operations.py", "main.py", "README.md"]

with zipfile.ZipFile("fresh_basket.zip", "w") as my_zip:
    for file in files_to_zip:
        my_zip.write(file)

# Download it straight to your computer
files.download("fresh_basket.zip")
```

import pandas as pd
import numpy as np

class Pizza:
    # ... (same as before)

class Customer:
    # ... (same as before)

class Order:
    # ... (same as before)

# Creating customers, pizzas, and orders
customer1 = Customer("Alice", "123-456-7890")
customer2 = Customer("Bob", "987-654-3210")

pizza1 = Pizza("Margherita", "medium", ["tomato", "cheese"])
pizza2 = Pizza("Pepperoni", "large", ["tomato", "cheese", "pepperoni"])
pizza3 = Pizza("Veggie", "small", ["tomato", "cheese", "mushrooms", "peppers", "onions"])

order1 = Order(customer1)
order1.add_pizza(pizza1)
order1.add_pizza(pizza2)

order2 = Order(customer2)
order2.add_pizza(pizza3)

# Creating a pandas DataFrame to store order data
order_data = []
for order in [order1, order2]:
    order_data.append({
        "Customer Name": order.customer.name,
        "Phone": order.customer.phone,
        "Pizzas": [pizza.name for pizza in order.pizzas],
        "Total": order.calculate_total()
    })

order_df = pd.DataFrame(order_data)

# Analyzing order data with numpy and pandas
average_total = np.mean(order_df["Total"])
most_popular_pizza = order_df["Pizzas"].explode().mode()[0]
customer_with_highest_total = order_df.loc[order_df["Total"].idxmax()]

# Displaying analysis results
print("Order Data:\n", order_df)
print("\nAverage Total: $", average_total)
print("Most Popular Pizza:", most_popular_pizza)
print("Customer with Highest Total:\n", customer_with_highest_total)

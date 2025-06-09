import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

# Set seaborn style
sns.set(style="whitegrid")

# 1. Total Sales by Product Category
sales_by_category = df.groupby("Product Category")["Total Purchase Amount"].sum().sort_values(ascending=False)

# 2. Average Sales by Product Category
avg_sales_by_category = df.groupby("Product Category")["Total Purchase Amount"].mean().sort_values(ascending=False)

# 3. Sum of Total Purchase Amount by Payment Method
payment_method_data = df.groupby("Payment Method")["Total Purchase Amount"].sum()

# 4. Average sales by Customer Age and Gender
avg_sales_by_age_gender = df.groupby(["Customer Age", "Gender"])["Total Purchase Amount"].mean().reset_index()

# Plotting
fig, axs = plt.subplots(2, 2, figsize=(16, 10))

# Bar chart - Total Sales by Product Category
sns.barplot(x=sales_by_category.values, y=sales_by_category.index, ax=axs[0, 0], color="royalblue")
axs[0, 0].set_title("Total Sales by Product Category")
axs[0, 0].set_xlabel("Total Sales")

# Bar chart - Average Sales by Product Category
sns.barplot(x=avg_sales_by_category.values, y=avg_sales_by_category.index, ax=axs[0, 1], color="skyblue")
axs[0, 1].set_title("Average Sales by Product Category")
axs[0, 1].set_xlabel("Avg Sales")

# Pie chart - Payment Method
axs[1, 0].pie(payment_method_data.values, labels=payment_method_data.index, autopct='%1.1f%%', startangle=140)
axs[1, 0].set_title("Total Purchase Amount by Payment Method")

# Line chart - Avg Sales by Age and Gender
sns.lineplot(data=avg_sales_by_age_gender, x="Customer Age", y="Total Purchase Amount", hue="Gender", ax=axs[1, 1])
axs[1, 1].set_title("Average Sales by Customer Age and Gender")
axs[1, 1].set_ylabel("Avg Sales")

plt.tight_layout()
plt.show()

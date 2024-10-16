# Pandas Library Learning

This repository showcases my learning progress with the Pandas library and CSV module in Python. The project demonstrates how to create, manipulate, and save book sales data using these tools.

## Description

The provided Python script performs the following tasks:
1. **Create Initial DataFrame**: Creates a DataFrame with initial book data including titles, authors, publication years, genres, and sales.
2. **Add Additional Book Data**: Defines and appends a second DataFrame with additional book data to the existing CSV file.
3. **Read Existing CSV**: Reads the existing CSV file to ensure data integrity.
4. **Add Price Information**: Adds price information and calculates taxes, total revenue, and profit after tax.
5. **Rename Columns**: Renames the columns for better clarity.
6. **Save Updated Data**: Saves the updated DataFrame back to the CSV file.

## Usage

1. Clone the repository to your local machine.
    ```sh
    git clone https://github.com/your-username/Pandas-Library-Learning.git
    cd Pandas-Library-Learning
    ```

2. Ensure you have Pandas installed in your Python environment.
    ```sh
    pip install pandas
    ```

3. Run the `pandas_learning.py` script to execute the data processing.
    ```sh
    python pandas_learning.py
    ```

## Example Code

```python
import pandas as pd  # Import the pandas library

# Create a DataFrame with initial book data
df_books = pd.DataFrame({
    'Title': ['Python for Beginners', 'Advanced Machine Learning', 'Data Science Essentials', 'Mystery of the Lost City', 'Thrilling Adventures'],
    'Author': ['Jane Doe', 'John Smith', 'Emily Johnson', 'Chris Davis', 'Alex Brown'],
    'Publication Year': [2020, 2018, 2019, 2017, 2021],
    'Genre': ['Programming', 'Technology', 'Data Science', 'Mystery', 'Adventure'],
    'Sales': [1000, 350, 150, 3000, 1200]  # Adjusted Sales to match Prices
})

# Define additional book data as a dictionary
df_books_additional = pd.DataFrame({
    'Title': ['Learning Python', 'Deep Learning with Python', 'Data Analysis with Python', 'Python Machine Learning', 'Python for Data Science'],
    'Author': ['Mark Lutz', 'François Chollet', 'Wes McKinney', 'Sebastian Raschka', 'Jake VanderPlas'],
    'Publication Year': [2021, 2019, 2022, 2020, 2018],
    'Genre': ['Programming', 'Artificial Intelligence', 'Data Science', 'Machine Learning', 'Data Science'],
    'Sales': [800, 900, 700, 650, 750]  # Adjusted Sales to match Prices
})

# Save the initial DataFrame to a CSV file
df_books.to_csv('Book_store_data.csv', index=False)

# Append the new DataFrame to the existing CSV file without writing the header again
df_books_additional.to_csv('Book_store_data.csv', mode='a', index=False, header=False)

# Read the existing CSV file
df = pd.read_csv('Book_store_data.csv')

# Add the new 'Price Before Tax' column
df['Price Before Tax'] = [9.97, 29.99, 37.99, 3.50, 9.99, 16.57, 38.99, 17.60, 22.39, 29.48]

# Calculate the Tax using lambda
df['Tax'] = df['Price Before Tax'].apply(lambda price: round(price * 0.07, 2))

# Calculate the Price after Tax
df['Price After Tax'] = round(df['Price Before Tax'] + df['Tax'], 2)

# Calculate Revenue
df['Revenue'] = df['Price Before Tax'] * df['Sales']

# Calculate Profit after Tax
df['Profit After Tax'] = round(df['Revenue'] - (df['Sales'] * df['Tax']), 2)

# Rename the DataFrame columns with clearer names
df.columns = ['Title', 'Author', 'Year Published', 
              'Genre Category', 'Units Sold', 'Price Before Tax (USD)', 
              'Sales Tax (USD)', 'Price After Tax (USD)', 'Total Revenue (USD)', 
              'Net Profit After Tax (USD)']

# Further rename specific columns for better clarity
df.rename(columns={'Title': 'Book Title', 'Author': 'Author Name'}, inplace=True)

# Save the updated DataFrame back to the CSV file
df.to_csv('Book_store_data.csv', index=False)

# Read the updated CSV file to verify
print(df)

Acknowledgements
Pandas Documentation
CSV Module Documentation

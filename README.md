# Web Scraping Amazon Data

This project demonstrates how to scrape product information from an Amazon HTML page using Python. The scraper extracts details such as product names, prices, reviews, quantity sold in the past month, ratings, and original prices. The scraped data is stored in a CSV file for easy analysis and further use.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Files](#files)
5. [Contributing](#contributing)
6. [License](#license)

## Project Overview

This project is designed to scrape product data from an Amazon product page in HTML format using **BeautifulSoup**. The script will extract the following information for each product:
- **Product Name**
- **Product Price**
- **Product Reviews**
- **Quantity Sold in the Past Month**
- **Product Ratings**
- **Original Price**

Once the data is extracted, it is saved into a CSV file (`Amazon_Product_Details.csv`) for easy access and further analysis.

## Installation

### Requirements

Before running the project, make sure you have **Python 3.x** installed along with the required libraries.

#### Required Libraries:
- **beautifulsoup4**
- **pandas**

You can install the required libraries by running the following commands in your terminal:

```pip install beautifulsoup4```
```pip install pandas```

**Prerequisites:**
A local Amazon HTML file to scrape. You will need to download an Amazon product page's HTML file and provide its path.
Usage

1. Clone the repository
   
To start using this project, clone the repository to your local machine:

git clone https://github.com/yourusername/amazon-product-scraper.git

2. Download the Amazon HTML file
   
Manually download an Amazon product page's HTML. After downloading, place the file in the directory where the Python script is located. For example, the script reads the file using the following path:

```
with open(r"D:\DATA ANALYTICS\python 2\Amazon_volleyball40.html", 'r', encoding='utf8') as file:
    soup = BeautifulSoup(file, 'html.parser')
```
Make sure the file path matches the location of your HTML file.

3. Run the script
   
Execute the script in your Python environment. The script will scrape product data from the Amazon HTML file and save it into a CSV file (Amazon_Product_Details.csv).

To run the script, use the following Python code:

```
from bs4 import BeautifulSoup
import pandas as pd

# Read and parse the HTML file
with open(r"D:\DATA ANALYTICS\python 2\Amazon_volleyball40.html", 'r', encoding='utf8') as file:
    soup = BeautifulSoup(file, 'html.parser')

# Lists to store the extracted data
product_names = []
product_prices = []
product_reviews = []
quantity_for_pastmonth = []
ratings = []
original_price = []

# Find all product containers
divs = soup.find_all('div', class_="sg-col-inner")
print(f"Found {len(divs)} product divs")  # Debugging line

# Extract details for each product
for div in divs:
    # Product Name
    name_element = div.find('span' , class_="a-size-base-plus a-color-base a-text-normal")
    product_name = name_element.get_text(strip=True) if name_element else " "
    product_names.append(product_name)
    print(f"Product Name: {product_name}") # Debugging line

    # Product Price
    price_element = div.find('span', class_="a-price-whole")
    product_price = price_element.get_text(strip=True) if price_element else " "
    product_prices.append(product_price)
    print(f"Product Price: {product_price}") # Debugging line

    # Product Reviews
    review_element = div.find('span', class_="a-size-base")
    product_reviews_text = review_element.get_text(strip=True) if review_element else " "
    product_reviews.append(product_reviews_text)
    print(f"Product Reviews: {product_reviews_text}") # Debugging line

    # Product Quantity for Past Month
    quantity_element = div.find('span', class_="a-size-base a-color-secondary")
    product_quantity_text = quantity_element.get_text(strip=True) if quantity_element else " "
    quantity_for_pastmonth.append(product_quantity_text)
    print(f"Product Quantity: {product_quantity_text}") # Debugging line

    # Product Ratings
    rating_element = div.find('span', class_="a-icon-alt")
    product_rating_text = rating_element.get_text(strip=True) if rating_element else " "
    ratings.append(product_rating_text)
    print(f"Product Ratings: {product_rating_text}") # Debugging line

    # Original Price
    originalprice = div.find_all('span', class_="a-offscreen")
    originalprice_element = originalprice[1] if len(originalprice) > 1 else None
    product_original_text = originalprice_element.get_text(strip=True) if originalprice_element else " "
    original_price.append(product_original_text)
    print(f"Product Original Price: {product_original_text}") # Debugging line

# Create a DataFrame and save to CSV
data = {
    'Product_Name': product_names,
    'Product_Price': product_prices,
    'Product_Reviews': product_reviews,
    'Product_Quantity': quantity_for_pastmonth,
    'Product_Ratings': ratings,
    'Original_Price': original_price
}

df = pd.DataFrame(data)
output_path = r'D:\DATA ANALYTICS\Amazon files2\Amazon_Product_Details.csv'
df.to_csv(output_path, index=False)
print(f"Data saved to {output_path}")
```
After running the script, you will find the CSV file (Amazon_Product_Details.csv) in the specified directory containing all the scraped data.

# Files
**Web Scraping Amazon Data:** Python script that scrapes the Amazon HTML page and extracts product details

**Amazon_volleyball40.html:** HTML file containing the Amazon product page data (manually downloaded)

**Amazon_Product_Details.csv:** CSV file containing the scraped product data (generated after running the script)

# Contributing
Feel free to fork this project and submit pull requests with any improvements or suggestions.

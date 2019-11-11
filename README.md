
# One-to-Many and Many-to-Many Joins - Lab

## Introduction

In this lab, you'll practice your knowledge of one-to-many and many-to-many relationships!

## Objectives

You will be able to:
* Explain one-to-many and many-to-many joins as well as implications for the size of query results
* Query data using one-to-many and many-to-many joins

## One-to-Many and Many-to-Many Joins
<img src='images/Database-Schema.png' width="600">

## Connect to the Database


```python
import sqlite3
import pandas as pd
conn = sqlite3.connect('data.sqlite')
cur = conn.cursor()
```

## Employees and their Office (a One-to-One join)

Return a dataframe with all of the employees including their first name and last name along with the city and state of the office that they work out of (if they have one). Include all employees and order them by their first name, then their last name.


```python
cur.execute('SELECT firstName, lastName, city, state FROM offices JOIN employees USING(officeCode) ORDER BY firstName, lastName ASC;')
df = pd.DataFrame(cur.fetchall())
df.columns = [i[0] for i in cur.description]
print('Number of results:', len(df))
df
```

    Number of results: 23





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>firstName</th>
      <th>lastName</th>
      <th>city</th>
      <th>state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Andy</td>
      <td>Fixter</td>
      <td>Sydney</td>
      <td></td>
    </tr>
    <tr>
      <td>1</td>
      <td>Anthony</td>
      <td>Bow</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Barry</td>
      <td>Jones</td>
      <td>London</td>
      <td></td>
    </tr>
    <tr>
      <td>3</td>
      <td>Diane</td>
      <td>Murphy</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Foon Yue</td>
      <td>Tseng</td>
      <td>NYC</td>
      <td>NY</td>
    </tr>
    <tr>
      <td>5</td>
      <td>George</td>
      <td>Vanauf</td>
      <td>NYC</td>
      <td>NY</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Gerard</td>
      <td>Bondur</td>
      <td>Paris</td>
      <td></td>
    </tr>
    <tr>
      <td>7</td>
      <td>Gerard</td>
      <td>Hernandez</td>
      <td>Paris</td>
      <td></td>
    </tr>
    <tr>
      <td>8</td>
      <td>Jeff</td>
      <td>Firrelli</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <td>9</td>
      <td>Julie</td>
      <td>Firrelli</td>
      <td>Boston</td>
      <td>MA</td>
    </tr>
    <tr>
      <td>10</td>
      <td>Larry</td>
      <td>Bott</td>
      <td>London</td>
      <td></td>
    </tr>
    <tr>
      <td>11</td>
      <td>Leslie</td>
      <td>Jennings</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <td>12</td>
      <td>Leslie</td>
      <td>Thompson</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <td>13</td>
      <td>Loui</td>
      <td>Bondur</td>
      <td>Paris</td>
      <td></td>
    </tr>
    <tr>
      <td>14</td>
      <td>Mami</td>
      <td>Nishi</td>
      <td>Tokyo</td>
      <td>Chiyoda-Ku</td>
    </tr>
    <tr>
      <td>15</td>
      <td>Martin</td>
      <td>Gerard</td>
      <td>Paris</td>
      <td></td>
    </tr>
    <tr>
      <td>16</td>
      <td>Mary</td>
      <td>Patterson</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <td>17</td>
      <td>Pamela</td>
      <td>Castillo</td>
      <td>Paris</td>
      <td></td>
    </tr>
    <tr>
      <td>18</td>
      <td>Peter</td>
      <td>Marsh</td>
      <td>Sydney</td>
      <td></td>
    </tr>
    <tr>
      <td>19</td>
      <td>Steve</td>
      <td>Patterson</td>
      <td>Boston</td>
      <td>MA</td>
    </tr>
    <tr>
      <td>20</td>
      <td>Tom</td>
      <td>King</td>
      <td>Sydney</td>
      <td></td>
    </tr>
    <tr>
      <td>21</td>
      <td>William</td>
      <td>Patterson</td>
      <td>Sydney</td>
      <td></td>
    </tr>
    <tr>
      <td>22</td>
      <td>Yoshimi</td>
      <td>Kato</td>
      <td>Tokyo</td>
      <td>Chiyoda-Ku</td>
    </tr>
  </tbody>
</table>
</div>



## Customers and their Orders (a One-to-Many join)

Return a dataframe with all of the customers' first and last names along with details for each of their order numbers, order dates, and statuses.


```python
cur.execute("""
    SELECT customerName, contactFirstName, contactLastName, customerNumber, orderNumber, orderDate, status 
    FROM customers 
    JOIN orders 
    USING(customerNumber);""")
df = pd.DataFrame(cur.fetchall())
df.columns = [i[0] for i in cur.description]
print('Number of results:', len(df))
df
```

    Number of results: 326





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customerName</th>
      <th>contactFirstName</th>
      <th>contactLastName</th>
      <th>customerNumber</th>
      <th>orderNumber</th>
      <th>orderDate</th>
      <th>status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Atelier graphique</td>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>103</td>
      <td>10123</td>
      <td>2003-05-20</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Atelier graphique</td>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>103</td>
      <td>10298</td>
      <td>2004-09-27</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Atelier graphique</td>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>103</td>
      <td>10345</td>
      <td>2004-11-25</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Signal Gift Stores</td>
      <td>Jean</td>
      <td>King</td>
      <td>112</td>
      <td>10124</td>
      <td>2003-05-21</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Signal Gift Stores</td>
      <td>Jean</td>
      <td>King</td>
      <td>112</td>
      <td>10278</td>
      <td>2004-08-06</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>321</td>
      <td>Diecast Collectables</td>
      <td>Valarie</td>
      <td>Franco</td>
      <td>495</td>
      <td>10243</td>
      <td>2004-04-26</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>322</td>
      <td>Kelly's Gift Shop</td>
      <td>Tony</td>
      <td>Snowden</td>
      <td>496</td>
      <td>10138</td>
      <td>2003-07-07</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>323</td>
      <td>Kelly's Gift Shop</td>
      <td>Tony</td>
      <td>Snowden</td>
      <td>496</td>
      <td>10179</td>
      <td>2003-11-11</td>
      <td>Cancelled</td>
    </tr>
    <tr>
      <td>324</td>
      <td>Kelly's Gift Shop</td>
      <td>Tony</td>
      <td>Snowden</td>
      <td>496</td>
      <td>10360</td>
      <td>2004-12-16</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <td>325</td>
      <td>Kelly's Gift Shop</td>
      <td>Tony</td>
      <td>Snowden</td>
      <td>496</td>
      <td>10399</td>
      <td>2005-04-01</td>
      <td>Shipped</td>
    </tr>
  </tbody>
</table>
<p>326 rows × 7 columns</p>
</div>



## Customers and their Payments (another One-to-Many join)

Return a dataframe with all of the customers' first and last names along with details about their payments' amount and date of payment. Sort these results in descending order by the payment amount.


```python
cur.execute("""
    SELECT customerName, contactFirstName, contactLastName, customerNumber, checkNumber, paymentDate, amount 
    FROM customers 
    JOIN payments 
    USING(customerNumber) 
    ORDER BY amount DESC;""")
df = pd.DataFrame(cur.fetchall())
df.columns = [i[0] for i in cur.description]
print('Number of results:', len(df))
df
```

    Number of results: 273





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customerName</th>
      <th>contactFirstName</th>
      <th>contactLastName</th>
      <th>customerNumber</th>
      <th>checkNumber</th>
      <th>paymentDate</th>
      <th>amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>FunGiftIdeas.com</td>
      <td>Violeta</td>
      <td>Benitez</td>
      <td>462</td>
      <td>GC60330</td>
      <td>2003-11-08</td>
      <td>9977.85</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Australian Gift Network, Co</td>
      <td>Ben</td>
      <td>Calaghan</td>
      <td>333</td>
      <td>JK479662</td>
      <td>2003-10-17</td>
      <td>9821.32</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Auto-Moto Classics Inc.</td>
      <td>Leslie</td>
      <td>Taylor</td>
      <td>198</td>
      <td>FI192930</td>
      <td>2004-12-06</td>
      <td>9658.74</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Australian Collectables, Ltd</td>
      <td>Sean</td>
      <td>Clenahan</td>
      <td>471</td>
      <td>AB661578</td>
      <td>2004-07-28</td>
      <td>9415.13</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Mini Auto Werke</td>
      <td>Roland</td>
      <td>Mendel</td>
      <td>452</td>
      <td>HG635467</td>
      <td>2005-05-03</td>
      <td>8807.12</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>268</td>
      <td>Mini Gifts Distributors Ltd.</td>
      <td>Susan</td>
      <td>Nelson</td>
      <td>124</td>
      <td>CQ287967</td>
      <td>2003-04-11</td>
      <td>11044.30</td>
    </tr>
    <tr>
      <td>269</td>
      <td>Dragon Souveniers, Ltd.</td>
      <td>Eric</td>
      <td>Natividad</td>
      <td>148</td>
      <td>KM172879</td>
      <td>2003-12-26</td>
      <td>105743.00</td>
    </tr>
    <tr>
      <td>270</td>
      <td>Blauer See Auto, Co.</td>
      <td>Roland</td>
      <td>Keitel</td>
      <td>128</td>
      <td>DI925118</td>
      <td>2003-01-28</td>
      <td>10549.01</td>
    </tr>
    <tr>
      <td>271</td>
      <td>Online Diecast Creations Co.</td>
      <td>Dorothy</td>
      <td>Young</td>
      <td>363</td>
      <td>IS232033</td>
      <td>2003-01-16</td>
      <td>10223.83</td>
    </tr>
    <tr>
      <td>272</td>
      <td>Mini Gifts Distributors Ltd.</td>
      <td>Susan</td>
      <td>Nelson</td>
      <td>124</td>
      <td>AE215433</td>
      <td>2005-03-05</td>
      <td>101244.59</td>
    </tr>
  </tbody>
</table>
<p>273 rows × 7 columns</p>
</div>



## Orders, Order details and Product Details (a Many-to-Many Join)

Return a dataframe with all of the customers' first and last names along with the product names, quantities, and date ordered for each of the customers and each of their orders. Sort these in descending order by the order date.

- Note: This will require joining 4 tables! This can be tricky! Give it a shot, and if you're still stuck, turn to the next section where you'll see how to write subqueries that can make complex queries such as this much simpler!


```python
cur.execute("""
    SELECT customerName, contactFirstName, contactLastName, customerNumber, 
            productName, quantityOrdered, orderDate
    FROM products 
    JOIN orderdetails 
    USING(productCode)
    JOIN orders
    USING(orderNumber)
    JOIN customers
    USING(customerNumber)
    ORDER BY orderDate DESC;""")
df = pd.DataFrame(cur.fetchall())
df.columns = [i[0] for i in cur.description]
print('Number of results:', len(df))
df
```

    Number of results: 2996





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customerName</th>
      <th>contactFirstName</th>
      <th>contactLastName</th>
      <th>customerNumber</th>
      <th>productName</th>
      <th>quantityOrdered</th>
      <th>orderDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Euro+ Shopping Channel</td>
      <td>Diego</td>
      <td>Freyre</td>
      <td>141</td>
      <td>1952 Alpine Renault 1300</td>
      <td>50</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <td>1</td>
      <td>La Rochelle Gifts</td>
      <td>Janine</td>
      <td>Labrune</td>
      <td>119</td>
      <td>1962 LanciaA Delta 16V</td>
      <td>38</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Euro+ Shopping Channel</td>
      <td>Diego</td>
      <td>Freyre</td>
      <td>141</td>
      <td>1958 Setra Bus</td>
      <td>49</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <td>3</td>
      <td>La Rochelle Gifts</td>
      <td>Janine</td>
      <td>Labrune</td>
      <td>119</td>
      <td>1957 Chevy Pickup</td>
      <td>33</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Euro+ Shopping Channel</td>
      <td>Diego</td>
      <td>Freyre</td>
      <td>141</td>
      <td>1940 Ford Pickup Truck</td>
      <td>54</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>2991</td>
      <td>Blauer See Auto, Co.</td>
      <td>Roland</td>
      <td>Keitel</td>
      <td>128</td>
      <td>1938 Cadillac V-16 Presidential Limousine</td>
      <td>46</td>
      <td>2003-01-09</td>
    </tr>
    <tr>
      <td>2992</td>
      <td>Online Diecast Creations Co.</td>
      <td>Dorothy</td>
      <td>Young</td>
      <td>363</td>
      <td>1917 Grand Touring Sedan</td>
      <td>30</td>
      <td>2003-01-06</td>
    </tr>
    <tr>
      <td>2993</td>
      <td>Online Diecast Creations Co.</td>
      <td>Dorothy</td>
      <td>Young</td>
      <td>363</td>
      <td>1911 Ford Town Car</td>
      <td>50</td>
      <td>2003-01-06</td>
    </tr>
    <tr>
      <td>2994</td>
      <td>Online Diecast Creations Co.</td>
      <td>Dorothy</td>
      <td>Young</td>
      <td>363</td>
      <td>1932 Alfa Romeo 8C2300 Spider Sport</td>
      <td>22</td>
      <td>2003-01-06</td>
    </tr>
    <tr>
      <td>2995</td>
      <td>Online Diecast Creations Co.</td>
      <td>Dorothy</td>
      <td>Young</td>
      <td>363</td>
      <td>1936 Mercedes Benz 500k Roadster</td>
      <td>49</td>
      <td>2003-01-06</td>
    </tr>
  </tbody>
</table>
<p>2996 rows × 7 columns</p>
</div>



## Summary

In this lab, you practiced your knowledge of one-to-many and many-to-many relationships!

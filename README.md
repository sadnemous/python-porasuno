## python-porasuno
### 1. Setup Virtual Environment:
(MY-INP)
```bash
cat>init
#create virtual env
if [ ! -d $PWD/venv ]; then
  mkdir $PWD/venv
fi

python3 -m venv $PWD/venv
. $PWD/venv/bin/activate
CTRL+C
. ./init
# if you have requirement.txt run following command
pip install -r requirement.txt
```
(MY-INP)
Once you are done, you may consider deactivating the environment by running `deactivate` command.
`deactivate` is a function which gets sourced into the environment during activating virtual environment.
To see the function detail run this command before deactivating the virtual environment:
`type deactivate`

### 2. Why does pip list generate a more comprehensive list than pip freeze? 
[Knowledge Source](https://stackoverflow.com/questions/18966564/pip-freeze-vs-pip-list)
```bash
$ pip list
feedparser (5.1.3)
pip (1.4.1)
setuptools (1.1.5)
wsgiref (0.1.2)
$ pip freeze
feedparser==5.1.3
wsgiref==0.1.2
```
Pip's documentation states:

|pip <option>|Description|
|---|---|
|freeze|Output installed packages in requirements format.|
|list|List installed packages.|

#### Usage
One may generate a requirements.txt via:

`pip freeze > requirements.txt`
A user can use this requirements.txt file to install all the dependencies. For instance:

`pip install -r requirements.txt`
The packages need to be in a specific format for pip to understand, such as:

#### requirements.txt
```
feedparser==5.1.3
wsgiref==0.1.2
django==1.4.2
...
```
That is the "requirements format".

Here, `django==1.4.2` implies install `django` version 1.4.2 (even though the latest is 1.6.x). <br>
If you do not specify ==1.4.2, the latest version available would be installed.
#### Final thought (MY-INP)
 - if I know which lib I need I can include in requirement.txt
 - once I am done with my work, I can run `pip freeze > requirement.txt` and share my work along with requirement.txt


### 3. connecting to mysql
To read a table from MySQL in Python, you can use the following steps:
1. Install the necessary library:
   `pip install mysql-connector-python`
2. Connect to the database:
```python
import mysql.connector

mydb = mysql.connector.connect(
  host="your_database_host",
  user="your_username",
  password="your_password",
  database="your_database_name"
)

mycursor = mydb.cursor()
```
3. Execute a query:
 ```python
   mycursor.execute("SELECT * FROM your_table_name")
   ```
4. Fetch the results:
```python
myresult = mycursor.fetchall()

for x in myresult:
  print(x)
5. Close the connection:
```python
mydb.close()
```


<b>Alternative method using pandas:</b><br>
If you want to work with the data in a pandas DataFrame, you can use the `read_sql_query()` function:
```python
import pandas as pd

df = pd.read_sql_query("SELECT * FROM your_table_name", mydb)
print(df)
```


#### Complete Code of my try-out (MY-INP)
my requirement.txt
```
mysql-connector-python==9.1.0
numpy==2.2.1
pandas==2.2.3
python-dateutil==2.9.0.post0
pytz==2024.2
six==1.17.0
tzdata==2024.2
```

read_mysql.py
```python
#!/usr/bin/env python3
import mysql.connector
import pandas as pd

mydb = mysql.connector.connect(
  host="localhost",
  user="soumen",
  password="das",
  database="mydb"
)

mycursor = mydb.cursor()
mycursor.execute("SELECT * FROM myInfo")
myresult = mycursor.fetchall()
for x in myresult:
  print(x)

mydb.close()
```


output
```
(1, 'HUAJIN', 'QIN')
(2, 'MARTHA', 'LEBDO')
(3, 'GARCIA', 'LUKE')
(4, 'RAINA', 'SAMAY')
(5, 'DIA', 'MIRZA')
```

#### collecting in dataframe and display
`$cat read_mysql_to_pd.py`
```python
#!/usr/bin/env python3
import pandas as pd
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="soumen",
  password="das",
  database="mydb"
)

mycursor = mydb.cursor()
# Execute a query
query = "SELECT * FROM myInfo"
mycursor.execute(query)

# Fetch all results
results = mycursor.fetchall()

# Create a DataFrame
df = pd.DataFrame(results, columns=mycursor.column_names)

# Close the connection
mydb.close()

print(df)
```

Output:
```
   ID FirstName LastName
0   1    HUAJIN      QIN
1   2    MARTHA    LEBDO
2   3    GARCIA     LUKE
3   4     RAINA    SAMAY
4   5       DIA    MIRZA
```










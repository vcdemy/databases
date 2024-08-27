# MySQL使用簡介

要使用 Python 讀取 MySQL 資料庫中的數據，可以使用`PyMySQL`或`mysql-connector-python`這兩個常用的 MySQL 套件。以下將介紹如何使用這兩個套件來讀取 MySQL 資料庫中的數據。

## 1. 使用`PyMySQL`

### 1.1 安裝`PyMySQL`

你也可以使用`PyMySQL`來連接和讀取 MySQL 資料庫：

```bash
pip install pymysql
```

### 1.2 連接到 MySQL 並讀取數據

以下是使用 PyMySQL 來讀取 MySQL 資料庫中的數據的範例：

```python
import pymysql

# 連接到 MySQL 資料庫
conn = pymysql.connect(
    host="localhost",
    user="your_username",
    password="your_password",
    database="your_database",
    port=3307 # 預設 MySQL 埠號是 3306，如果你使用的是不同的埠號，請在這裡指定
)

# 創建 cursor
cursor = conn.cursor()

# 執行 SQL 查詢
cursor.execute("SELECT * FROM your_table")

# 獲取所有查詢結果
rows = cursor.fetchall()

# 打印每一行
for row in rows:
    print(row)

# 關閉 cursor 和連接
cursor.close()
conn.close()
```


## 2. 使用`mysql-connector-python`

### 2.1 安裝`mysql-connector-python`

首先，你需要安裝`mysql-connector-python`：

```bash
pip install mysql-connector-python
```

### 2.2 連接到 MySQL 並讀取數據

以下是如何使用`mysql-connector-python`讀取 MySQL 資料庫中的數據：

```python
import mysql.connector

# 連接到 MySQL 資料庫
conn = mysql.connector.connect(
    host="localhost",
    user="your_username",
    password="your_password",
    database="your_database",
    port=3307 # 預設 MySQL 埠號是 3306，如果你使用的是不同的埠號，請在這裡指定
)

# 創建 cursor
cursor = conn.cursor()

# 執行 SQL 查詢
cursor.execute("SELECT * FROM your_table")

# 獲取所有查詢結果
rows = cursor.fetchall()

# 打印每一行
for row in rows:
    print(row)

# 關閉 cursor 和連接
cursor.close()
conn.close()
```

### 3. 程式碼說明

`conn`：建立與 MySQL 資料庫的連接。

`cursor`：通過游標執行 SQL 語句並獲取結果。

`execute()`：用來執行 SQL 語句。

`fetchall()`：獲取所有查詢結果。你也可以使用 fetchone() 來逐行檢索結果。

`close()`：完成操作後，關閉游標和連接。

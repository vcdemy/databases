# SQLite使用簡介

在 Python 中，可以使用內建的`sqlite3`模組來與 SQLite 資料庫進行交互。SQLite 是一個輕量級的資料庫管理系統，適合小型應用和嵌入式使用。以下是如何使用 Python 與 SQLite 進行基本資料庫操作的介紹。

## 1. 連接到 SQLite 資料庫

你需要先連接到一個 SQLite 資料庫。如果該資料庫文件不存在，SQLite 會自動創建一個新的文件。

```python
import sqlite3

# 連接到 SQLite 資料庫，如果資料庫不存在則會自動創建
conn = sqlite3.connect('example.db')

# 創建一個 cursor 物件，通過它來執行 SQL 語句
cursor = conn.cursor()
```

## 2. 創建表格

你可以使用`cursor.execute()`方法來執行 SQL 語句。下面是如何創建一個名為`users`的表格。

```python
# 創建 users 表格
cursor.execute('''
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL,
        age INTEGER NOT NULL
    )
''')

# 保存 (commit) 變更
conn.commit()
```

## 3. 插入數據

可以使用`INSERT INTO`語句來插入數據到表格中。

```python
# 插入一條數據
cursor.execute('''
    INSERT INTO users (name, age)
    VALUES (?, ?)
''', ('Alice', 30))

# 插入多條數據
users = [
    ('Bob', 24),
    ('Charlie', 29)
]
cursor.executemany('''
    INSERT INTO users (name, age)
    VALUES (?, ?)
''', users)

# 保存變更
conn.commit()
```

## 4. 查詢數據

可以使用`SELECT`語句來查詢資料庫中的數據。

```python
# 查詢所有 users
cursor.execute('SELECT * FROM users')
rows = cursor.fetchall()

# 打印查詢結果
for row in rows:
    print(row)
```

## 5. 更新數據
使用`UPDATE`語句來更新表格中的數據。

```python
# 更新一條數據
cursor.execute('''
    UPDATE users
    SET age = ?
    WHERE name = ?
''', (32, 'Alice'))

# 保存變更
conn.commit()
```

## 6. 刪除數據
使用`DELETE`語句來刪除表格中的數據。

```python
# 刪除一條數據
cursor.execute('''
    DELETE FROM users
    WHERE name = ?
''', ('Bob',))

# 保存變更
conn.commit()
```

## 7. 關閉連接
完成操作後，請務必關閉 cursor 和資料庫連接。

```python
# 關閉 cursor 和連接
cursor.close()
conn.close()
```
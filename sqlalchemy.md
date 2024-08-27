# sqlalchemy使用簡介

使用`sqlalchemy`有一個很大的好處，如果之後想要變更資料庫伺服器，程式碼只需要改資料庫的網址，其他的程式碼大致上不太需要修改。

## 安裝 sqlalchemy

```python
pip install sqlalchemy
```

依想要連接的資料庫，可能需要安裝不同的資料庫連接套件。

譬如：

```python
# mysql
pip install pymysql
# 或
pip install mysql.connector
```

```python
# postgresql
pip install psycopg2

# 或安裝 psycopg2-binary
# psycopg2-binary會同時安裝postgresql相依的前端程式庫，但佈署時建議安裝psycopg2。
pip install psycopg2-binary
```

## 連線資料庫

```python
from sqlalchemy import create_engine

engine_url = "dialect+driver://username:password@host:port/database"
engine = create_engine(engine_url, echo=True)
```

`create_engine()`: 用來建立資料庫引擎。資料庫引擎會連接資料庫，並執行SQL指令。

`echo=True`: 會將執行的SQL語句列印到標準輸出，方便debug。

## 定義模型

```python
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import Column, Integer, String

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String)
    age = Column(Integer)

```

`declarative_base()`: 用來產生ORM模型的Base Class。

## 建立資料表

```python
Base.metadata.create_all(engine)
```

## 建立及使用 Session

```python
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
session = Session()
```

在 SQLAlchemy 中，通常會使用 Session 來管理與資料庫的交互，這是因為 Session 提供了一個緩衝區，允許你在提交（commit）之前累積多個操作。這有助於控制交易和減少資料庫的直接操作次數。

```python
user1 = User('John', 25)
user2 = User('Mary', 20)
user3 = User('Alex', 28)

session.add(user1)
session.add_all([user2, user3])
session.commit()
```

上面的例子中，只有在`session.commit()`執行時，資料才會真的被加入到資料庫中。



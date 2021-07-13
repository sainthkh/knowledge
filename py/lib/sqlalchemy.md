# sqlalchemy

## connect engine

```py
from sqlalchemy import create_engine
from sqlalchemy.engine.url import URL

engine = create_engine("sqlite+pysqlite:///:memory:", echo=True, future=True)

db_url = URL(
    drivername="mysql+mysqldb",
    username=cf.db_id,
    password=cf.db_passwd,
    host=cf.db_ip,
    port=cf.db_port,
    database='daily_buy_list'
)
engine = create_engine(db_url)
```

## Execute SQL statement

```py
from sqlalchemy import text

with engine.connect() as conn:
    result = conn.execute(text("select 'hello world'"))
    print(result.all())
```

[Implicit or connectionless execution is deprecated since 2.0](https://docs.sqlalchemy.org/en/14/core/connections.html#dbengine-implicit).

```py
result = engine.execute(text("select username from users"))
for row in result:
    print("username:", row['username'])
```

Commit changes. Use `conn.commit()`.

```py
with engine.connect() as conn:
    conn.execute(text("CREATE TABLE some_table (x int, y int)"))
    conn.execute(
        text("INSERT INTO some_table (x, y) VALUES (:x, :y)"),
        [{"x": 1, "y": 1}, {"x": 2, "y": 4}]
    )
    conn.commit()
```

What is the `text()` function? => [check this doc](https://docs.sqlalchemy.org/en/14/core/tutorial.html#using-textual-sql).
-> summary: By default, `conn.execute()` accepts Python objects created with SQL Language Expression. Because of that, use `text()` when you want to use SQL in text directly.


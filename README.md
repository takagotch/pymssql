### pymssql
---
http://www.pymssql.org/en/latest/

```py
from os import getenv
import pymssql

server = getenv("PYMSSQL_TEST_SERVER")
user = getenv("PYMSSWL_TEST_USERNAME")
password = getenv("PYMSSQL_TEST_PASSWORD")

conn = pymssql.connect(server, user, password, "tempdb")
cursor = conn.cursor()
cursor.execute("""
  id INT NOT NULL,
  name VATCHAR(100),
  salesrep VARCHAR(100),
  PRIMARY KEY(id)
""")
cursor.executemany(
  "INSERT INTO persons VALUES (%d, %s, %s)",
  [(1, 'John Smith', 'John Doe'),
    (2, 'Jane Doe', 'Joe Dog'),
    (3, 'Mike T.', 'Sarah H.')])
conn.commit()

cursor.execute('SELECT * FROM persons WHERE salesrep=%s', 'John Doe')
row = cursor.fetchone()
while row:
  print("ID=%d, Name=%s" % (row[0], row[1]))
  row = cursor.fetchone()
  
conn.close()

conn = pymssql.connect(
  host=r'dbhostname\myinstance',
  user=r'companydomain\username',
  password=PASSWORD,
  database='DatabaseOfInterest'
)

conn = pymssql.connect(server, user, password, "tempdb")
cursor = conn.cursor()
cursor.execute('SELECT * FROM persons WHERE salesrep=%s', 'John Doe')
for row in cursor:
  print('row = %r ' % (row,))
conn.close()

cl = conn.cursor()
cl.execute('SELECT * FROM persons')

c2 = conn.cursor()
c2.execute('SELECT * FROM persons WHERE salesrep=%s', 'John Doe')

print( "all persons" )
print( c1.fetchall() )

print( "John Doe" )
print( c2.fetchall() )

c1.execute('SELECT ... ')
cl_list = cl.fetchall()

c2.execute('SELECT ... ')
c2_list = c2.fetchall()

conn = pymssql.connect(server, user, password, "tempdb")
cursor = conn.cursor(as_dict=True)

cursor.execute('SELECT * FROM persons WHERE salesrep=%s', 'John Doe')
for row in cursor:
  print("ID=%d, Name=%s" % (row['id'], row['name']))
conn.close()

with pymssql.connect(server, user, password, "tempdb") as conn:
  with conn.cursor(as_dict=True) as cursor:
    cursor.execute('SELECT * FROM persons WHERE salesrep=%s', 'John Doe')
    for row in cursor:
      print("ID=%d, Name=%s" % (row['id'], row['name']))

with pymssql.connect(server, user, password, "tempdb") as conn:
  with conn.cursor() as cursor:
    cursor.execute("""
    CREATE PROCEDURE FindPerson
      @name VARCHAR(100)
    AS BEGIN
      SELECT * FROM persons WHERE name = @name
    END
    """)
    cursor.callproc('FIndPerson', ('Jane Doe',))
    for row in cursor:
      print("ID=%d, Name=%s" % (row['id'], row['name']))

import gevent.socket
import ppymssql

def wait_callback(read_fileno):
  gevent.socket.wait_read(read_fileno)
pymssql.set_wait_callback(wait_callback)
```

```
```

```
```

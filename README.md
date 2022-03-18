# Oracle_connection_Python

### Trên windows,
 #### Cài Oracle:
 Theo link này: https://cx-oracle.readthedocs.io/en/latest/user_guide/installation.html
 trong đó có cả cách dùng cài với proxy
 
 ```bash
 python -m pip install --proxy=10.228.10.14:3128  cx_Oracle
 python -m pip install --proxy=http://ics.foxconn.com/nsbg.pac  cx_Oracle --upgrade --user
 
 python -m pip install cx_Oracle --upgrade --user
    If you are behind a proxy, add a proxy server to the command, for example add --proxy=http://proxy.example.com:80
 
 ```
 
The easiest solution is as follows:
Download 64-bit version of oracle instantClient (Phiên bản hiện tại: instantclient-basic-windows.x64-21.3.0.0.0) from: https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html
Copy the dll files in the instantclient directory to the python directory (Thư mục có chứa python.exe)

#### Code mẫu

```python

import cx_Oracle

HostName='10.220.81.xx'
PortNumber='xxxx'
service_name='vnap'

user=r'xxxx'
password='xxxxx'
dsn_tns = cx_Oracle.makedsn(HostName, PortNumber, service_name)
 # if needed, place an 'r' before any parameter in order to address special characters such as '\'.
conn = cx_Oracle.connect(user=user, password=password, dsn=dsn_tns) 
# if needed, place an 'r' before any parameter in order to address special characters such as '\'. 
#  For example, if your user name contains '\',
#  you'll need to place 'r' before the user name: user=r'User Name'

c = conn.cursor()
c.execute("select * from MES4.R_STATION_WIP where emp_no like '+%'")
 # use triple quotes if you want to spread your query across multiple lines
# c.execute('select * from MES4.R_STATION_WIP where STATION_FLAG =1') # use triple quotes if you want to spread your query across multiple lines
for row in c:
    print (row) # this only shows the first two columns. To add an additional column you'll need to add , '-', row[2], etc.
conn.close()

```






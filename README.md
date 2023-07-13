# DoWell-Connection
#### Dowellwellconnection API is used to do basic database operations. We can do the following operations
- fetch
- find
- insert
- update 

#### Url:
```shell
http://uxlivinglab.pythonanywhere.com/
```
#### Method:
```shell
POST
```

#### Request data format:

```python
{
  "cluster": "provided_cluster",
  "database": "provided_databse_name",
  "collection": "provided_collection",
  "document": "provided_document",
  "team_member_ID": "provided_team_member_id",
  "function_ID": "provided_function_id",
  "command": "update", # can be 'fetch', 'find', 'insert'
  "field": { 
  },
  'update_field':{
    
   },
  "platform": "provided_platform",

}

```

#### Fetch data from database
```'command'``` needs to be ```fetch``` and
```'field'``` is a key value pair, the matching data/rows with the field value will be fetched from the database.

For example the below ```command``` and ```field``` will fetch all the data/rows which has ```India``` as country from database.
```python
  {
    ...
    ...
    'command': 'fetch',
    'field':{
      'country': 'India',
    },
    ...
    ...
  }
    
```

##### Response
```python
  {
    'isSuccess':True,
    'data': data, # available only if 'isSuccess' is True
    'error': 'some error cause string', # available only if 'isSuccess' is False
  }
```

#### Find data from database
```'command'``` needs to be ```fetch``` and
```'field'``` is a key value pair, the first matching data/rows with the field value will be fetched from the database.

For example the below ```command``` and ```field``` will fetch the first data/row which has ```India``` as country from database.
```python
{
    ...
    ...
    'command': 'find',
    'field':{
      'country': 'India',
    },
    ...
    ...
 }
```


##### Response
```python
  {
    'isSuccess':True,
    'data': data, # available only if 'isSuccess' is True
    'error': 'some error cause string', # available only if 'isSuccess' is False
  }
```

#### Insert data in database
```'command'``` needs to be ```insert``` and
```'field'``` is a key value pair, the value of the ```field``` option will be saved in the database.

For example the below ```command``` and ```field``` will insert ``` { 'country': 'India','age': 20} ``` in database
```python
{
    ...
    ...
    'command': 'insert',
    'field':{
      'country': 'India',
      'age': 20,
    },
    ...
    ...
}
```     
    
##### Response
```python
  {
    'isSuccess':True,
    'inserted_id': 'inserted id', # available only if 'isSuccess' is True
    'error': 'some error cause string', # available only if 'isSuccess' is False
  }
```

#### Update data in database
```'command'``` needs to be ```update``` and
```'fields'``` is a key value pair, the row  mathing the given ```field``` option will be updated
```'update_field'``` is a key value pair containing the update value
For example the below ```command``` and ```field``` will insert update ``` { 'country': 'India','age': 20} ``` row/data in database with     { 'country': 'India', 'age': 9999}

```python
{
    ...
    ...
    'command': 'insert',
    'field':{
      'country': 'India',
      'age': 20,
    },
    'update_field': {
        'country': 'India',
        'age': 9999,
    }
    ...
    ...
 }
```

##### Response
```python
  {
    'isSuccess':True,
    'error': 'some error cause string', # available only if 'isSuccess' is False
  }
```


### Curl command example of the request:
```curl
curl -X POST  -H 'content-type: application/json' -d '{"cluster": "FB", "database": "mongodb", "collection": "day001", "document": "QNPS", "team_member_ID": "1234567890123456", "function_ID": "ABCDE", "command": "insert", "field": {"name": "Rafi", "phone": "1234", "age": "26", "language": "English", "gender": "Male"},"update_field":{}, "platform": "bangalore"}' http://uxlivinglab.pythonanywhere.com/
```
### Python example of the request:

```python
import json
import requests

url = "http://uxlivinglab.pythonanywhere.com/"
data={
  "cluster": "FB",
  "database": "mongodb",
  "collection": "day001",
  "document": "QNPS",
  "team_member_ID": "1234567890123456",
  "function_ID": "ABCDE",
  "command": "update",
  "field": {
    "name": "Joy",
    "phone": "1234",
    "age": "26",
    "language": "English",
    "gender": "Male",
  },
  'update_field':{
    "name": "Joy update",
    "phone": "123456",
    "age": "26",
    "language": "Englis",

   },
  "platform": "bangalore",

}
headers = {'content-type': 'application/json'}

response = requests.post(url, json =data,headers=headers)
print(response.text)

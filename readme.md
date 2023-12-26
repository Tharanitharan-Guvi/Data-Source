# JSON

1. JSON was created by David Crawford in the labs of Yahoo!
2. JSON - JavaScript Objectt Notation
3. JSON are a small readable format for structure the data and transmitting across the network. It is very efficient for searching and accessing information. It can be worked with different programming languages and applications.
4. It is used to transmit the data between the server and the web application. 
5. All major companies use JSON to transmit data these days.
6. Initially, XML (Extended Markup Language) is also used to do the same job. But it has been replaced with JSON on majority of the feilds, banking and secure applications. 
7. JSON comprised of Key and Value pairs in a list. (In terms of python, we can say JSON are just list of dictionaries)


You can convert Python objects of the following types, into JSON strings:

- dict
- list
- tuple
- string
- int
- float
- True
- False
- None


- 3rd Party Data transference we use API servers especially with JSON.
- API - Application Programming Interface
- API Servers works on endpoints/URL with the help of HTTP Methods
    - GET
    - POST
    - PATCH
    - DELETE
- API server there is no need for username and password for the database as you have the URL / endpoints.


API Architecture:
=================

1. REST API
    - REST = Representational State Transfer
    - These API servers are based on JSON data
    - They are very easy to create and use.
    - It is based on the Client - Server model.
    - This architecture is a stateless architecture which means that it does not store data not its status between each request

2. SOAP API
    - SOAP = Simple Object Access Protocol
    - Based on the XML data
    - It is highly structured and secure as compared to REST
    - It works with various different types of protocols like HTTP, TCP/IP, SMTP and so on.


```python
import json

with open('data.json', 'r') as file:
    data = file.read()

python_obj = json.loads(data)


for item in python_obj:
    print(item['name'])
```

Python Module Needed - Requests

pip install requests


```python
import requests

class LatLong:

    def __init__(self, url):
        self.url = url
        self.response = requests.get(url)
    
    def server_status(self):
        return self.response.status_code

    def fetch_data(self):
        try:
            if self.server_status() == 200:
                return self.response.json()
            else:
                print(self.server_status())
        except:
            print("Error")
    
    def getName(self):
        result = []
        for item in self.fetch_data():
            result.append(item['name'])
        return result

    def getLat(self):
        result = []
        for item in self.fetch_data():
            result.append(item['address']['geo']['lat'])
        return result

    def getLong(self):
        result = []
        for item in self.fetch_data():
            result.append(item['address']['geo']['lng'])
        return result


url = 'https://jsonplaceholder.typicode.com/users'
obj = LatLong(url)
print(obj.getName())
```
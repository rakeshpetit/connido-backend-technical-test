# conindo-backend

> Backend API for Articles

## About

This project uses [Feathers](http://feathersjs.com). An open source web framework for building modern real-time applications.

## Getting Started

Getting up and running is as easy as 1, 2, 3 and 4.

1. Make sure you have [NodeJS](https://nodejs.org/) and [npm](https://www.npmjs.com/) installed.
2. Install your dependencies

    ```
    cd path/to/conindo-backend; npm install
    ```
3. Install mongodb and make sure it is accepting connections from 127.0.0.1:27017
4. Start your app

    ```
    npm start
    ```
5. Start making the API calls once the server is started. The AJAX calls are provided as helpers to make the calls appropriately. POST, PUT and DELETE is available only for authenticated users. GET request can be done without authentication.

## Testing

Simply run `npm test` and all your tests in the `test/` directory will be run.


**API call for user creation**

$.ajax({  
            type: "POST",  
            url: "http://localhost:3030/users",  
            data: {
  strategy: 'local',
  firstName: 'Rakesh',
  lastName: 'Arunachalam',
  email: 'rakeshpetit@gmail.com',
  password: 'rak123'
},  
            success: function(dataString) { 
                console.log('User created'); 
            }  
        });

**API call for user authentication**

$.ajax({  
            type: "POST",  
            url: "http://localhost:3030/authentication",  
            data: {
  strategy: 'local',
  email: 'rakeshpetit@gmail.com',
  password: 'rak123'
},  
            success: function(dataString) { 
                console.log('User authenticated'); 
            }  
        });    

**API call to get articles**

$.ajax({  
            type: "GET",  
            url: "http://localhost:3030/articles",
            success: function(dataString) { 
                console.log('Get articles success', dataString.data); 
            }  
        });

**API call to get articles with pagination where articles from 6 through 15 are fetched - Pagination**

$.ajax({  
            type: "GET",  
            url: "http://localhost:3030/articles?$limit=10&$skip=5",
            success: function(dataString) { 
                console.log('Get articles success', dataString.data); 
            }  
        });      

**API call to get articles by author**

$.ajax({  
            type: "GET",  
            url: "http://localhost:3030/articles?author[$in]=Rakesh",
            success: function(dataString) { 
                console.log('Get articles success', dataString.data); 
            }  
        }); 

**API call to get articles by title**

$.ajax({  
            type: "GET",  
            url: "http://localhost:3030/articles?title[$in]=My%20Post",
            success: function(dataString) { 
                console.log('Get articles success', dataString.data); 
            }  
        });

**API call to get articles by author and title**

$.ajax({  
            type: "GET",  
            url: "http://localhost:3030/articles?title[$in]=My%20Post&author[$in]=Rakesh",
            success: function(dataString) { 
                console.log('Get articles success', dataString.data); 
            }  
        });

**API call to post articles where token generated in authentication call to be passed**

let token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6ImFjY2VzcyJ9.eyJ1c2VySWQiOiI1YmFjOTNhM2U5ZjVlYjJiZTAwMTkzYjAiLCJpYXQiOjE1MzgwMzg3ODIsImV4cCI6MTUzODEyNTE4MiwiYXVkIjoiaHR0cHM6Ly9jb25uaW5kby5jb20iLCJpc3MiOiJyYWtlc2giLCJzdWIiOiJhbm9ueW1vdXMiLCJqdGkiOiJhZDJjYjk5Mi03OGQ1LTQxNzktYTgwOS0zZGY4ZmNiNTU0NWMifQ.cJjl6u0kSyQhJ2OILcRNAkenhGYXqtT3pWkgnY8QJQY';

$.ajax({  
            type: "POST",  
            url: "http://localhost:3030/articles",
            data: {
  title: 'My Post',
  content: 'This is my first Post',
  author: 'Rakesh'
},  
            success: function(dataString) { 
                console.log('Post articles success'); 
            },            
  beforeSend: function(xhr, settings) { xhr.setRequestHeader('Authorization','Bearer ' + token); }  
        });    

**API call to update articles where token generated in authentication call to be passed**

const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6ImFjY2VzcyJ9.eyJ1c2VySWQiOiI1YmFjOTNhM2U5ZjVlYjJiZTAwMTkzYjAiLCJpYXQiOjE1MzgwMzg3ODIsImV4cCI6MTUzODEyNTE4MiwiYXVkIjoiaHR0cHM6Ly9jb25uaW5kby5jb20iLCJpc3MiOiJyYWtlc2giLCJzdWIiOiJhbm9ueW1vdXMiLCJqdGkiOiJhZDJjYjk5Mi03OGQ1LTQxNzktYTgwOS0zZGY4ZmNiNTU0NWMifQ.cJjl6u0kSyQhJ2OILcRNAkenhGYXqtT3pWkgnY8QJQY';

$.ajax({  
            type: "PUT",  
            url: "http://localhost:3030/articles/5bacc4ab2222d82a2c1ef50b",
            data: {
  title: 'My modified Post',
  content: 'This is my modified Post',
  author: 'Rakesh'
},  
            success: function(dataString) { 
                console.log('Update articles success'); 
            },            
  beforeSend: function(xhr, settings) { xhr.setRequestHeader('Authorization','Bearer ' + token); }  
        }); 

**API call to delete articles where token generated in authentication call to be passed**

const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6ImFjY2VzcyJ9.eyJ1c2VySWQiOiI1YmFjOTNhM2U5ZjVlYjJiZTAwMTkzYjAiLCJpYXQiOjE1MzgwMzg3ODIsImV4cCI6MTUzODEyNTE4MiwiYXVkIjoiaHR0cHM6Ly9jb25uaW5kby5jb20iLCJpc3MiOiJyYWtlc2giLCJzdWIiOiJhbm9ueW1vdXMiLCJqdGkiOiJhZDJjYjk5Mi03OGQ1LTQxNzktYTgwOS0zZGY4ZmNiNTU0NWMifQ.cJjl6u0kSyQhJ2OILcRNAkenhGYXqtT3pWkgnY8QJQY';

$.ajax({  
            type: "DELETE",  
            url: "http://localhost:3030/articles/5bacc4ab2222d82a2c1ef50b",
            data: {
},  
            success: function(dataString) { 
                console.log('Delete articles success'); 
            },            
  beforeSend: function(xhr, settings) { xhr.setRequestHeader('Authorization','Bearer ' + token); }  
        });   


## Backend Technical Test

You have been asked to implement a __REST API__ that allows its consumers to create *articles*. Each *article* has a `title`, `content`, `author's name`, `date created` and `date updated`.

### Functional requirements

1. Implement an endpoint to *create* an article
2. Implement an endpoint to *get all* articles (paginated)

### Non functional Requirements

1. Implement using **JavaScript ES6**
2. Test coverage using any testing framework (TDD or BDD)
3. Use a **NoSQL** datastore (any)
4. Write instructions of how to run the application in `README.md`

### Bonus Features:

1. Implement an endpoint to *search* articles by *author's name* and/or *title*.
2. Use **Typescript**.
3. Use **mocha** and **chai** for testing.
4. Use **MongoDB** as datastore.

### Delivery of your solution

Fork this repository and implement your solution on the fork. Once you are happy with your solution, please email us the link to your fork.            
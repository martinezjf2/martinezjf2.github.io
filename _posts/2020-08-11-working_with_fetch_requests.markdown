---
layout: post
title:      "Working with Fetch()_Requests"
date:       2020-08-12 02:17:09 +0000
permalink:  working_with_fetch_requests
---


## What is Fetch in JavaScript?

Fetch can be used for contacting and interacting with a Applications Programming Interface to retrieve data.

## Types of Requests

1.	“GET” requests are used to tell the API “Hey, I want to get some information from you!”
2.	“POST” requests tell the API “I have a piece of data that I want to append to you”
3.	“PATCH/PUT” requests tell the API “I need to edit some information about the data”
4.	“DELETE” requests tell the API exactly what it sounds like — We want to delete a piece of data.


## Getting Started

Fetch is a JavaScript function that accepts two arguments which takes in a stringified URL and the second one is optional that will contain information about your request. If no second argument is provided, JavaScript will automatically expect a “GET” request. 


#### `fetch("http://localhost:3000/users")`

## Promises

When making a fetch request, it will always return a promise if the request was successful. However, the first promise that fetch sends is not as great looking. 

#### `fetch("http://localhost:3000/users")`
####       `.then(rsp => console.log(rsp))`

This would return a response as shown below:

`Response {type: "cors", url: "http://localhost:3000/users", redirected: false, status: 200, ok: true, …}
body: (...)
bodyUsed: false
headers: Headers {}
ok: true
redirected: false
status: 200
statusText: "OK"
type: "cors"
url: "http://localhost:3000/users"
__proto__: Response`

As shown, the status was successful, but does not show the data of the API.

In order to see our data, we would need to parse it into something that JavaScript can read by converting it to JSON. However, by converting it to JSON, the method also returns another promise. Now we can actually work with the next promise.

#### `fetch("http://localhost:3000/users")`
####       `.then(rsp => (rsp => rsp.json())`
####       `.then(rsp => console.log(rsp))`

The last promise will return the data we want to manipulate within our objects.

(`45) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]`

`0: {id: 2, first_name: "Jacqulyn", last_name: "Jones", created_at: "2020-07-30T00:46:54.608Z", updated_at: "2020-07-30T00:46:54.608Z"}`

`1: {id: 3, first_name: "Ching", last_name: "Rice", created_at: "2020-07-30T00:46:54.612Z", updated_at: "2020-07-30T00:46:54.612Z"}`

`2: {id: 4, first_name: "Marcel", last_name: "Leffler", created_at: "2020-07-30T00:46:54.616Z", updated_at: "2020-07-30T00:46:54.616Z"}`

`3: {id: 5, first_name: "Lynwood", last_name: "Bechtelar", created_at: "2020-07-30T00:46:54.619Z", updated_at: "2020-07-30T00:46:54.619Z"}`

`4: {id: 6, first_name: "Chadwick", last_name: "Crist", created_at: "2020-07-30T00:46:54`

### Here's The "Catch"

What if there is an error? How can I see what my error can be?

Well, we have to know what statuses does our request send us which are Successful, Pending, and Rejected.

By using the .catch() method, we can create an error, alerting us if our request was either not successful of rejected.

Here is a video on how we can implement the [catch method](http://https://www.youtube.com/watch?v=cuEtnrL9-H0&t=4s)

Pretty Simple?


---
title: "Rest Api 101"
date: 2019-12-27T16:17:50+06:00
draft: true
authors:
- Ashraful Islam Nixon
tags:
- REST
- API
- HATEOAS
- RPC
- SOAP
- REQUEST
- RESPONSE
categories:
- REST API
---

## So what is an API:
Formal answer is : An **application programming interface** (**API**) is an interface or communication between different parts of a computer program intended to simplify the implementation and maintenance of software. [link](https://en.wikipedia.org/wiki/Application_programming_interface)

But the way I try to understand API is like this, 
```
Like an UI supports interactions between computer and human, 
Through API(s) softwares can talk, take actions, make interactions in between themselves.
```
## API type In Brief:
Programming languages, client libraries all may have api which can be comsumed/extended by the consumers(developers, third party applications). But for today we will discuss API on top of HTTP only.

There are lots of APIs on HTTP. Like,
- RPC (Remote Proccedure Call) [Resource 1](https://en.wikipedia.org/wiki/XML-RPC) [Resource 2](https://en.wikipedia.org/wiki/JSON-RPC)
- [REST (Representaional State Transfer)](https://en.wikipedia.org/wiki/Representational_state_transfer)
- [SOAP (Simple Object Access Protocol)](https://en.wikipedia.org/wiki/SOAP)
and more.

# What makes an API RESTful:

### HATEOAS
To be honest, now a days APIs are not properly RESTful. 
For an API to be properly restful it's needs to comply with [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS) (Hypermedia as the Engine of Application State). What does it means actually? 
API should be self explanatory. API provider should provide a single endpoint to it's consumers, the consumer should able to understand, access everything from that endpoint, including next endpoints and it's functionalities.
Example:

#### Request:
```
GET /accounts/nixon1333/ HTTP/1.1
Host: bank.example.com
Accept: application/vnd.acme.account+json
...
```
#### Response:
```
HTTP/1.1 200 OK
Content-Type: application/vnd.acme.account+json
Content-Length: ...
{
    "account": {
        "account_id": nixon1333,
        "balance": {
            "currency": "bdt",
            "value": 100.00
        },
        "links": {
            "deposit": "/accounts/nixon1333/deposit",
            "withdraw": "/accounts/nixon1333/withdraw",
            "transfer": "/accounts/nixon1333/transfer",
            "close": "/accounts/nixon1333/close"
        }
    }
}
```
So from here we can see an API consumer can navigate to next apis using the `links` property from **response**.
To maintain this type of structure is very hard and time consuming. So most of the developers including me try to avoid this type structures and try to adapt rest of the features of REST and build RESTful API!

### Core Elements:
There are 3 core elements in REST which makes an API RESTful.
1. **Resources** are the data model API providers wants to share via API. Like `User` model, `Wallet` model, `Players` model etc.
2. **Operations** are the actions API consumers will do with the resources. Like `Create User`, `Delete Wallet Account`, `Get the List of Players` etc.
3. **Representaions** are simply is what and how API consumers get to see the output of their actions. Like how the consumer will see the list of `Players` or what will be shown after an `User` being created/deleted. will the responses shown in json,xml or something else.

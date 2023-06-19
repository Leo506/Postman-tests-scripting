# How to write complex test cases
Common postman tests doesn't give you ability to test complex scenarios when you need to send some requests to
setup data (e.g. create account, create order), request for test and requests for clean up (e.g. delete account, delete order).
Anyway you can test these scenarios. All you need for this - create collection (or folder) with requests for scenario.
Here the example:

## Preparation
I have an API in postman. According to [this article](https://blog.postman.com/api-testing-tips-from-a-postman-professional/) I keep my 
API specification separate from tests.

![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/80e1a115-73b5-4d7c-ac70-f1e9e8acb6b4)

In `Tests` collection I created folder called `Accounts`. So here will be placed tests releated to account resource.

![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/33289106-6d10-4702-a6b9-397d0887343d)

## Test case
I would like to check that if I try to create account with same email I will get `409` response. I created folder for this test case

![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/6efbd168-f47d-48ea-a7ac-c40bbe52fccc)


## Creating requests
Now I create some requests for my test case.
- First request - it is "setup" request for creating account
  
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/b517761c-220b-421e-8150-78e099cc7f4e)
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/c6929c91-0963-4396-8193-a6f0a0cedebd)
  
- Second request - it is "test" request where I check that response status code is `409`
  
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/a8e2a78d-e0aa-453a-96dc-73172b015523)
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/c3e255a9-4dd9-4938-9d8c-36d661373581)
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/6f77ba28-d450-4c25-bac2-a4fc35779214)
  
- Last request - "clean up" request for deleting account created by first request
  
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/c26cadb4-67a3-42a8-be75-4104db43b68c)

## Using variables
As you can spot in last request I use varialbe `accountId`. Where from I get it? I set it in first request

![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/c53b41e6-9d96-4692-9f8b-126fdf09afd3)

You can use variables to transfer data from one request to another.

## Run tests
Let's run test case and ensure that all works as we expected.

- Click `Run collection` on `Tests` collection
  
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/7698acc2-2555-4a4b-9570-3b67162876f4)

- In `Runner` menu select requests you would like to run
  
  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/b96dd966-2d19-4f4f-bdd1-d1a529e5ba01)

- Click `Run <Collection Name>`

- View results

  ![image](https://github.com/Leo506/Postman-tests-scripting/assets/64748654/ccee265e-f9d9-417c-8c13-1e0bc83ef8e3)


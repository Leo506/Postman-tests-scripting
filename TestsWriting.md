# Tests writing

## Base syntax
```javascript
pm.test("Test name", function() {
    // test body
});
```

## How to check response status code?
```javascript
pm.response.to.have.status(200);
```

## How to get specific response body property (in json)?
```javascript
const responseJson = pm.response.json();
const id = responseJson.id;  // id - is specific property
```

## How to get request body specific property (in json)?
```javascript
const jsonRequest = JSON.parse(pm.request.body.raw);
console.log(jsonRequest.firstName);  // firstName = is specific property
```

## How to run another request from test?
```javascript
const deleteRequest = {
    url: `request url`,
    method: 'request method',
    header: {
        'Content-Type': 'application/json'
    },
    body: {
        mode: 'raw',
        raw: JSON.stringify({
            firstName: 'firstName'
        })
    }
};
pm.sendRequest(deleteRequest, (error, response) => {});
```
More here: [postman docs](https://learning.postman.com/docs/writing-scripts/script-references/postman-sandbox-api-reference/#sending-requests-from-scripts)

## Using dynamic variables for random values
To get random value you can use dynamic variables:
```javascript
pm.variables.replaceIn('{{$randomFirstName}}');
```

Here the example of Pre-request script for randomizing request body data:
```javascript
const firstName = pm.variables.replaceIn('{{$randomFirstName}}');
const lastName = pm.variables.replaceIn('{{$randomLastName}}');
const email = pm.variables.replaceIn('{{$randomEmail}}');

pm.request.header = {
    'Content-Type': 'application/json'
};
pm.request.body =  {
    mode: 'raw',
    raw: JSON.stringify({
        "firstName": firstName,
        "lastName": lastName,
        "email": email,
        "role": "USER",
        "password": "qwerty123"
    })
};
```
Here full list of dynamic variables: [postman docs](https://learning.postman.com/docs/writing-scripts/script-references/variables-list/)

## JSON schema validation
Here the simple example of checking if response body consists all required properties (`id`, `firstName`, `lastName`, `email`, `role`):
```javascript
const schema = {
    required: ['id', 'firstName', 'lastName', 'email', 'role']
};
pm.response.to.have.jsonSchema(schema);
```
More here: [postman docs](https://learning.postman.com/docs/writing-scripts/script-references/test-examples/#validating-response-structure)

## Links
- https://learning.postman.com/docs/writing-scripts/test-scripts/
- https://learning.postman.com/docs/writing-scripts/script-references/test-examples/#parsing-response-body-data
- https://learning.postman.com/docs/writing-scripts/script-references/postman-sandbox-api-reference/#sending-requests-from-scripts
- https://learning.postman.com/docs/writing-scripts/script-references/variables-list/
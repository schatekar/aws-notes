
# Avoiding "malformed lambda proxy response" error

1. Check that you are returning a properly formed response object from the callback. Let's say you want want to return the following JSON object
```
let person = {
    firstName: "firstName",
    lastName: "lastName"
}
```

If you return the above object like below

```
callback(null, person);
```
you will most likely be hit with a `502` error with a message in the logs says `malformed lambda proxy response`. This is because, API gateway lambda proxy integration expects the lambda to return a properly formed response object which must specify at least the status code and HTTP body like below

```
let response = {
    statusCode: 200
    body: person
}

callback(null, response);
```

2. 

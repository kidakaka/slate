---
title: API Reference for Singularity

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the lending API for Singularity! You can use our API to automate your lending process with our API endpoints.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

For getting developer keys for UAT and Production environments, please drop an email to prasad@singularitycredit.com.


# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Personal Loan

## Dedupe Check

```ruby
require 'uri'
require 'net/http'

url = URI("http:///%7B%7BReq_URL%7D%7D/api/v1/dedupe")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request["cache-control"] = 'no-cache'
request["postman-token"] = '0ae2699a-c937-1b1e-2fbf-84dd7134acff'
request.body = "{\n  \"mobile\": \"9823394322\",\n  \"email\": \"sachit@homecapital.in\",\n  \"pan\": \"DYYPK7129D\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPConnection("")

payload = "{\n  \"mobile\": \"9823394322\",\n  \"email\": \"sachit@homecapital.in\",\n  \"pan\": \"DYYPK7129D\"\n}"

headers = {
    'content-type': "application/json",
    'cache-control': "no-cache",
    'postman-token': "c43a8082-2abe-84ff-d1cc-5a10a63080fa"
    }

conn.request("POST", "%7B%7BReq_URL%7D%7D/api/v1/dedupe", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```shell
curl -X POST \
  http:///%7B%7BReq_URL%7D%7D/api/v1/dedupe \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 53a1b458-824f-7550-75ff-7c1679dba8a7' \
  -d '{
  "mobile": "9823394322",
  "email": "sachit@homecapital.in",
  "pan": "DYYPK7129D"
}'
```

```javascript
var data = JSON.stringify({
  "mobile": "9823394322",
  "email": "sachit@homecapital.in",
  "pan": "DYYPK7129D"
});

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "http:///%7B%7BReq_URL%7D%7D/api/v1/dedupe");
xhr.setRequestHeader("content-type", "application/json");
xhr.setRequestHeader("cache-control", "no-cache");
xhr.setRequestHeader("postman-token", "335413ee-d571-4230-9fec-7706c7f08502");

xhr.send(data);
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint checks against the details provided if the person is already a customer of Singularity or not. If the person is not a customer of Singularity, then the dedupe API will indicate as much. If this happens, then you want to call the Register Applicant API.

### HTTP Request

`GET {{Req_URL}}/api/v1/dedupe`

### Query Parameters

Parameter | Format | Description
--------- | ------- | -----------
mobile | 9999999999 | 10 digit mobile number, without spaces and ISD code
email | email.address@domain.com | Email address of the person who wants the personal loan
pan | AAAAA9999A | PAN of the person who wants the personal loan

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Register Applicant

```ruby
require 'uri'
require 'net/http'

url = URI("http:///%7B%7BReq_URL%7D%7D/api/v1/dedupe")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request["cache-control"] = 'no-cache'
request["postman-token"] = '0ae2699a-c937-1b1e-2fbf-84dd7134acff'
request.body = "{\n  \"mobile\": \"9823394322\",\n  \"email\": \"sachit@homecapital.in\",\n  \"pan\": \"DYYPK7129D\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPConnection("")

payload = "{\n  \"mobile\": \"9823394322\",\n  \"email\": \"sachit@homecapital.in\",\n  \"pan\": \"DYYPK7129D\"\n}"

headers = {
    'content-type': "application/json",
    'cache-control': "no-cache",
    'postman-token': "c43a8082-2abe-84ff-d1cc-5a10a63080fa"
    }

conn.request("POST", "%7B%7BReq_URL%7D%7D/api/v1/dedupe", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```shell
curl -X POST \
  http:///%7B%7BReq_URL%7D%7D/api/v1/dedupe \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 53a1b458-824f-7550-75ff-7c1679dba8a7' \
  -d '{
  "mobile": "9823394322",
  "email": "sachit@homecapital.in",
  "pan": "DYYPK7129D"
}'
```

```javascript
var data = JSON.stringify({
  "mobile": "9823394322",
  "email": "sachit@homecapital.in",
  "pan": "DYYPK7129D"
});

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "http:///%7B%7BReq_URL%7D%7D/api/v1/dedupe");
xhr.setRequestHeader("content-type", "application/json");
xhr.setRequestHeader("cache-control", "no-cache");
xhr.setRequestHeader("postman-token", "335413ee-d571-4230-9fec-7706c7f08502");

xhr.send(data);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


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

Parameter | Required | Description
--------- | ------- | -----------
mobile | Yes | 10 digit mobile number, without spaces and ISD code
email | Yes | Email address of the person who wants the personal loan
pan | Yes | PAN of the person who wants the personal loan

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Register Applicant

```ruby
require 'uri'
require 'net/http'

url = URI("http:///%7B%7BReq_URL%7D%7D/api/v1/applicant")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request["cache-control"] = 'no-cache'
request["postman-token"] = '81336b1f-98b3-87f5-a530-4b29cecc9f05'
request.body = " {\n            \"first_name\" : \"URMILA\",\n            \"middle_name\" : \"HARSHAD\",\n            \"last_name\" : \"ODHEKAR\",\n            \"mobile\": \"9619927914\",\n            \"email\" : \"urmial.odhekar@gmail.com\",\n            \"pan\" : \"AROPB9302K\",\n            \"aadhar_number\" : \"XXXXXXXX6070\",\n            \"dob\" : \"02/25/1984\",\n            \"gender\" : \"female\",\n            \"marital_status\" : \"married\",\n            \"qualification\" : 200,\n            \"citizenship\" : \"indian\",\n            \"ca_line1\" : \"D/401, mandakini chsl, shiv vallabh cross road\",\n            \"ca_line2\" : \"Last bus stop of 298,Rawal pada\",\n            \"ca_city\" : 20005,\n            \"ca_state\" : 19771,\n            \"ca_pincode\" : 400068,\n            \"ca_residence_duration\" : 300,\n            \"ca_residence_type\" : \"with parents\",\n            \"pa_line1\" : \"D/401, mandakini chsl, shiv vallabh cross road\",\n            \"pa_line2\" : \"Last bus stop of 298,Rawal pada\",\n            \"pa_city\" : 20005,\n            \"pa_state\" : 19771,\n            \"pa_pincode\" : 400068,\n            \"pa_residence_duration\" : 300,\n            \"pa_residence_type\" : \"with parents\",\n            \"different_address\" : 0,\n            \"pp_current_job_months\" : 0,\n            \"pp_current_job_years\" : 1,\n            \"pp_total_experience_months\" : 0,\n            \"pp_total_experience_years\" : 1,\n            \"pp_industry\" : 86,\n            \"pp_employment_type\" : \"salaried\",\n            \"pp_company_name\" : \"MUNICIPAL CORPORATION OF GREATER MUMBAI\",\n            \"pp_net_income\" :  59410,\n            \"pp_current_emis\" : 0,\n            \"pp_other_income\":0,\n            \"pp_office_email\" : \"urmial.odhekar@gmail.com\",\n            \"pp_designation\" : \"N/A\",\n            \"pp_constitution\" : \"gov\",\n            \"pp_org_address_line1\" : \"5, Mahapalika Marg, Dhobi Talao\",\n            \"pp_org_address_line2\" : \"Chhatrapati Shivaji Terminus Area,Fort\",\n            \"pp_city\" : 20005,\n            \"pp_state\" : 19771,\n            \"pp_pincode\" : 400001\n        }"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPConnection("")

payload = " {\n            \"first_name\" : \"URMILA\",\n            \"middle_name\" : \"HARSHAD\",\n            \"last_name\" : \"ODHEKAR\",\n            \"mobile\": \"9619927914\",\n            \"email\" : \"urmial.odhekar@gmail.com\",\n            \"pan\" : \"AROPB9302K\",\n            \"aadhar_number\" : \"XXXXXXXX6070\",\n            \"dob\" : \"02/25/1984\",\n            \"gender\" : \"female\",\n            \"marital_status\" : \"married\",\n            \"qualification\" : 200,\n            \"citizenship\" : \"indian\",\n            \"ca_line1\" : \"D/401, mandakini chsl, shiv vallabh cross road\",\n            \"ca_line2\" : \"Last bus stop of 298,Rawal pada\",\n            \"ca_city\" : 20005,\n            \"ca_state\" : 19771,\n            \"ca_pincode\" : 400068,\n            \"ca_residence_duration\" : 300,\n            \"ca_residence_type\" : \"with parents\",\n            \"pa_line1\" : \"D/401, mandakini chsl, shiv vallabh cross road\",\n            \"pa_line2\" : \"Last bus stop of 298,Rawal pada\",\n            \"pa_city\" : 20005,\n            \"pa_state\" : 19771,\n            \"pa_pincode\" : 400068,\n            \"pa_residence_duration\" : 300,\n            \"pa_residence_type\" : \"with parents\",\n            \"different_address\" : 0,\n            \"pp_current_job_months\" : 0,\n            \"pp_current_job_years\" : 1,\n            \"pp_total_experience_months\" : 0,\n            \"pp_total_experience_years\" : 1,\n            \"pp_industry\" : 86,\n            \"pp_employment_type\" : \"salaried\",\n            \"pp_company_name\" : \"MUNICIPAL CORPORATION OF GREATER MUMBAI\",\n            \"pp_net_income\" :  59410,\n            \"pp_current_emis\" : 0,\n            \"pp_other_income\":0,\n            \"pp_office_email\" : \"urmial.odhekar@gmail.com\",\n            \"pp_designation\" : \"N/A\",\n            \"pp_constitution\" : \"gov\",\n            \"pp_org_address_line1\" : \"5, Mahapalika Marg, Dhobi Talao\",\n            \"pp_org_address_line2\" : \"Chhatrapati Shivaji Terminus Area,Fort\",\n            \"pp_city\" : 20005,\n            \"pp_state\" : 19771,\n            \"pp_pincode\" : 400001\n        }"

headers = {
    'content-type': "application/json",
    'cache-control': "no-cache",
    'postman-token': "3244bc00-527a-cb60-0a41-5fd674847456"
    }

conn.request("POST", "%7B%7BReq_URL%7D%7D/api/v1/applicant", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```shell
curl -X POST \
  http:///%7B%7BReq_URL%7D%7D/api/v1/applicant \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 98cefc9d-f6a5-5431-7a12-29e1ad94a9ac' \
  -d ' {
            "first_name" : "URMILA",
            "middle_name" : "HARSHAD",
            "last_name" : "ODHEKAR",
            "mobile": "9619927914",
            "email" : "urmial.odhekar@gmail.com",
            "pan" : "AROPB9302K",
            "aadhar_number" : "XXXXXXXX6070",
            "dob" : "02/25/1984",
            "gender" : "female",
            "marital_status" : "married",
            "qualification" : 200,
            "citizenship" : "indian",
            "ca_line1" : "D/401, mandakini chsl, shiv vallabh cross road",
            "ca_line2" : "Last bus stop of 298,Rawal pada",
            "ca_city" : 20005,
            "ca_state" : 19771,
            "ca_pincode" : 400068,
            "ca_residence_duration" : 300,
            "ca_residence_type" : "with parents",
            "pa_line1" : "D/401, mandakini chsl, shiv vallabh cross road",
            "pa_line2" : "Last bus stop of 298,Rawal pada",
            "pa_city" : 20005,
            "pa_state" : 19771,
            "pa_pincode" : 400068,
            "pa_residence_duration" : 300,
            "pa_residence_type" : "with parents",
            "different_address" : 0,
            "pp_current_job_months" : 0,
            "pp_current_job_years" : 1,
            "pp_total_experience_months" : 0,
            "pp_total_experience_years" : 1,
            "pp_industry" : 86,
            "pp_employment_type" : "salaried",
            "pp_company_name" : "MUNICIPAL CORPORATION OF GREATER MUMBAI",
            "pp_net_income" :  59410,
            "pp_current_emis" : 0,
            "pp_other_income":0,
            "pp_office_email" : "urmial.odhekar@gmail.com",
            "pp_designation" : "N/A",
            "pp_constitution" : "gov",
            "pp_org_address_line1" : "5, Mahapalika Marg, Dhobi Talao",
            "pp_org_address_line2" : "Chhatrapati Shivaji Terminus Area,Fort",
            "pp_city" : 20005,
            "pp_state" : 19771,
            "pp_pincode" : 400001
        }'
```

```javascript
var data = JSON.stringify({
  "first_name": "URMILA",
  "middle_name": "HARSHAD",
  "last_name": "ODHEKAR",
  "mobile": "9619927914",
  "email": "urmial.odhekar@gmail.com",
  "pan": "AROPB9302K",
  "aadhar_number": "XXXXXXXX6070",
  "dob": "02/25/1984",
  "gender": "female",
  "marital_status": "married",
  "qualification": 200,
  "citizenship": "indian",
  "ca_line1": "D/401, mandakini chsl, shiv vallabh cross road",
  "ca_line2": "Last bus stop of 298,Rawal pada",
  "ca_city": 20005,
  "ca_state": 19771,
  "ca_pincode": 400068,
  "ca_residence_duration": 300,
  "ca_residence_type": "with parents",
  "pa_line1": "D/401, mandakini chsl, shiv vallabh cross road",
  "pa_line2": "Last bus stop of 298,Rawal pada",
  "pa_city": 20005,
  "pa_state": 19771,
  "pa_pincode": 400068,
  "pa_residence_duration": 300,
  "pa_residence_type": "with parents",
  "different_address": 0,
  "pp_current_job_months": 0,
  "pp_current_job_years": 1,
  "pp_total_experience_months": 0,
  "pp_total_experience_years": 1,
  "pp_industry": 86,
  "pp_employment_type": "salaried",
  "pp_company_name": "MUNICIPAL CORPORATION OF GREATER MUMBAI",
  "pp_net_income": 59410,
  "pp_current_emis": 0,
  "pp_other_income": 0,
  "pp_office_email": "urmial.odhekar@gmail.com",
  "pp_designation": "N/A",
  "pp_constitution": "gov",
  "pp_org_address_line1": "5, Mahapalika Marg, Dhobi Talao",
  "pp_org_address_line2": "Chhatrapati Shivaji Terminus Area,Fort",
  "pp_city": 20005,
  "pp_state": 19771,
  "pp_pincode": 400001
});

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "http:///%7B%7BReq_URL%7D%7D/api/v1/applicant");
xhr.setRequestHeader("content-type", "application/json");
xhr.setRequestHeader("cache-control", "no-cache");
xhr.setRequestHeader("postman-token", "ce46fbf8-6566-99b7-5ddb-f1a6ca9c5c8a");

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

This API call create an applicant profile on the Singularity systems. 

<aside class="warning">Before you call this API, please remember to call the Dedupe API call first.</aside>

### HTTP Request

`POST {{Req_URL}}/api/v1/applicant`

### URL Parameters

Parameter | Required | Description
--------- | ------- | -----------
first_name | Yes | First name of applicant
middle_name | Yes | Middle name of applicant
last_name | Yes | Last name of applicant
mobile | Yes | 10 digit mobile number, without spaces and ISD code
email | Yes | Email address of the person who wants the personal loan
pan | Yes | PAN of the person who wants the personal loan
aadhar_number | Yes | Aadhaar number of applicant
dob | Yes | Date of Birth
gender | Yes | Gender of the applicant (female/male) 
marital_status | Yes | Marital status of the applicant (single/married/divorced) 
qualification | Yes | Qualification of the applicant (see Master collection for the mapping) 
citizenship | Yes | Citizenship of the applicant (indian/nri) 
ca_line1 | Yes | Address Line 1 of current address
ca_line2 | No | Address Line 2  of current address
ca_city | Yes | City id of the applicant (see Master collection for the mapping) 
ca_state | Yes | State id of the applicant (see Master collection for the mapping) 
ca_pincode | Yes | Pincode of the applicant 
ca_residence_duration | Yes | Residence in months of the applicant at the current address 
ca_residence_type | Yes | Residence type of the applicant at the current address (rented/paying guest/with parents/self owned/company provided)
pa_line1 | Yes | Address Line 1 of permanent address
pa_line2 | No | Address Line 2  of permanent address
pa_city | Yes | City id of the applicant (see Master collection for the mapping) 
pa_state | Yes | State id of the applicant (see Master collection for the mapping) 
pa_pincode | Yes | Pincode of the applicant 
pa_residence_duration | Yes | Residence in months of the applicant at the permanent address 
pa_residence_type | Yes | Residence type of the applicant at the permanent address (rented,paying guest,with parents,self owned,company provided)
pp_current_job_months | Yes | Current job work experience months. This is not total months, but just the remainder of months. e.g If the applicant has been working in a company for 15 months, this value would be 3.
pp_current_job_years | Yes | Current job work experience years. This is not total years, but just the number of years. e.g If the applicant has been working in a company for 15 months, this value would be 1.
pp_total_experience_months | Yes | Total job work experience months. This is not total work experience in months, but just the number of months remainder. e.g If the applicant has been working for 45 months, this value would be 9.
pp_total_experience_years | Yes | Total job work experience years. This is total work experience in years as an integer. e.g If the applicant has been working for 45 months, this value would be 3.
pp_industry | Yes | Industry id of the applicant's professional industry (see Master collection for the mapping) 
pp_employment_type | Yes | Salaried or Self-employed individual (salaried/self-employed/senp/sep)
pp_company_name | Yes | Name of the company where the applicant is working
pp_net_income | Yes | Net income of the applicant is working
pp_current_emis | No | Current EMIs of the applicant (if any)
pp_other_income | No | Other income of the applicant (if any)
pp_office_email | No | Professional email address of the applicant (this will be verified)
pp_designation | No | Designation of the applicant
pp_constitution | Yes | Designation of the applicant
pp_org_address_line1 | Yes | Address Line 1 of Company office
pa_line2 | No | Address Line 2  of Company office
pa_city | Yes | City id of the applicant (see Master collection for the mapping) 
pa_state | Yes | State id of the applicant (see Master collection for the mapping) 
pa_pincode | Yes | Pincode of the applicant's Company office

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


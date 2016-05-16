---
title: API Reference

language_tabs:
  - shell

includes:
  - errors

search: true
---

# Introduction

This API documentation quickly lays out the process of sending across Survey results through our RESTful API. Sending over 
results is a 2 step process, first the lead must be sent across then the survey responses.


# Leads

## Post a Lead

> This request will return JSON structured as follows:

```json
{
  "success": true,
  "data": {
    "lead_id": 55406
  }
}
```

This endpoint posts lead details into our system

### HTTP Request

`POST https://teleoutsourcing.mysecureportal.net/api/leads/`

### Query Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
first_name | true | string | The first name of the lead
last_name | true | string | The last name of the lead
address1 | true | string | First line of the lead's address
address2 | false | string | Second line of the lead's address
address3 | false | string | Third line of the lead's address
town | true | string | The town the lead lives in
county | false | string | The county the lead lives in
postal_code | true | string | The postal code of the lead
home_number | true (if no mobile number) | integer | The home telephone number of the lead (no 44 prefix, e.g. 1253817220)
mobile_number | true (if no home number) | integer | The mobile telephone number of the lead (no 44 prefix, e.g. 7958991982)
email | false | string | The e-mail address of the lead

# Surveys

## Post Survey Results

> This request will return JSON structured as follows:

```json
{
  "success": true,
  "data": {
    "survey_log_id": 86170
  }
}
```

> An example of the json encoded string that should include questions and responses is as follows:

```json
[
  {
    "question_id": 121,
    "response": 1993
  },
  {
    "question_id": 132,
    "response": 1982
  },
  {
    "question_id": 135,
    "response": "£300"
  },
  {
    "question_id": 142,
    "response": 2089
  },
]
```

This endpoint posts results of a survey and associates them with a lead

### HTTP Request

`POST https://teleoutsourcing.mysecureportal.net/api/leads/<lead_id>/surveys/<survey_id>`

### Query Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
completed | true | boolean | The the survey was fully completed then true, if only partially completed then false
responses | true | string | A Json encoded array featuring an array of all questions and responses (see right for example)

### Responses

A full list of question ID's and response ID's will be provided on any update to the script and the responses posted will 
require to be changed to match the given update. The appropriate Survey ID will also be given in this same document.

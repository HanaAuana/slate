---
title: Wufoo API

language_tabs:
  - shell: cURL
  - php: PHP
  - python
  - node
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Wufoo API! You can use our API to access Wufoo API endpoints, which can get information on forms, fields, entries, and more. You can also submit new entries,
and even add or remove Webhooks.

There are wrapper libraries for Ruby, PHP, jQuery, Python, and Node, but you can make requests using any HTTP service. You can view basic code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right. All examples use the 'fishbowl' example subdomain. When making your own requests, be sure to use your own account name/subdomain, and your own API Key

# Authentication

> To authenticate, Wufoo uses HTTP Basic Auth:

```shell
# With cURL, you can just pass the "username" and "password" with each request
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms.json"
```

```php
<? php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms.json');      //1
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);                          //2
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');   //3
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);                     //4
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');             //5

$response = curl_exec($curl);                                           //6
$resultStatus = curl_getinfo($curl);                                    //7

if($resultStatus['http_code'] == 200) {                     //8
    echo htmlentities($response);
} else {
    echo 'Call Failed '.print_r($resultStatus);                         //9
}
?>
```

```python
import requests
from requests.auth import HTTPBasicAuth

url = 'https://fishbowl.wufoo.com/api/v3/forms.json'
auth = HTTPBasicAuth('M8X9-0MP5-63FD-EUG8', 'footastic')
requests.get(url, auth=auth)
```

> Make sure to replace `AOI6-LFKL-VM1Q-IEX9` with your API key. The second value `footastic` is required, but can be anything

Wufoo uses [Basic Auth](http://www.ietf.org/rfc/rfc2617.txt) with API Keys to allow access to the API. 

Wufoo expects for the API key to be included as the 'username' and any value as the 'password' portion of Basic Auth. If the service you're using doesn't have a built in way to authenticate using Basic Auth, you can set the Authorization header to a base64 string, like so:

`Authorization: Basic base64('username:password')`

After encoding, it might look something like this:

`Authorization: Basic QU9JNi1MRktMLVZNMVEtSUVYOTpmb290YXN0aWM=`

<aside class="notice">
You'll need to replace 'username' with your API key, and password with any value (our examples use 'footastic')
</aside>

# Forms

## Get All Forms

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import requests
from requests.auth import HTTPBasicAuth

url = 'https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true'
auth = HTTPBasicAuth('M8X9-0MP5-63FD-EUG8', 'footastic')
requests.get(url, auth=auth)
r.json()
```

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true"
```

> The above request returns JSON structured like this:

```json
{
  "Forms" : [
    {
      "Name" : "Api Submit Example",
      "Description" : "This is my form. Please fill it out. It's awesome!",
      "RedirectMessage" : "Success! Thanks for filling out my form!",
      "Url" : "api-submit-example",
      "Email" : "",
      "IsPublic" : "1",
      "Language" : "english",
      "StartDate" : "2000-01-01 12:00:00",
      "EndDate" : "2030-01-01 12:00:00",
      "EntryLimit" : "0",
      "DateCreated" : "2010-07-07 14:51:14",
      "DateUpdated" : "2010-07-07 14:51:14",
      "Hash" : "psy5irt0bq4brj",
      "LinkFields" : "https://fishbowl.wufoo.com/api/v3/forms/psy5irt0bq4brj/fields.json?pretty=true",
      "LinkEntries" : "https://fishbowl.wufoo.com/api/v3/forms/psy5irt0bq4brj/entries.json?pretty=true",
      "LinkEntriesCount" : "https://fishbowl.wufoo.com/api/v3/forms/psy5irt0bq4brj/entries/count.json?pretty=true"
    },
    {
      "Name" : "Tiny Form",
      "Description" : "This is my form. Please fill it out. It's awesome!",
      "RedirectMessage" : "Great! Thanks for filling out my form!",
      "Url" : "tiny-form",
      "Email" : "",
      "IsPublic" : "1",
      "Language" : "english",
      "StartDate" : "2000-01-01 12:00:00",
      "EndDate" : "2030-01-01 12:00:00",
      "EntryLimit" : "0",
      "DateCreated" : "2012-02-22 15:35:33",
      "DateUpdated" : "2012-02-22 15:35:33",
      "Hash" : "kvikd1a1n54u3f",
      "LinkFields" : "https://fishbowl.wufoo.com/api/v3/forms/kvikd1a1n54u3f/fields.json?pretty=true",
      "LinkEntries" : "https://fishbowl.wufoo.com/api/v3/forms/kvikd1a1n54u3f/entries.json?pretty=true",
      "LinkEntriesCount" : "https://fishbowl.wufoo.com/api/v3/forms/kvikd1a1n54u3f/entries/count.json?pretty=true"
    },
    {
      "Name" : "Wufoo API Example",
      "Description" : "This is my form. Please fill it out. It's awesome!",
      "RedirectMessage" : "Success! Thanks for filling out my form!",
      "Url" : "wufoo-api-example",
      "Email" : "",
      "IsPublic" : "1",
      "Language" : "english",
      "StartDate" : "2000-01-01 12:00:00",
      "EndDate" : "2030-01-01 12:00:00",
      "EntryLimit" : "0",
      "DateCreated" : "0000-00-00 00:00:00",
      "DateUpdated" : "0000-00-00 00:00:00",
      "Hash" : "s1afea8b1vk0jf7",
      "LinkFields" : "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/fields.json?pretty=true",
      "LinkEntries" : "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries.json?pretty=true",
      "LinkEntriesCount" : "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries/count.json?pretty=true"
    }
  ]
}
```

This endpoint retrieves all forms.

### HTTP Request

`GET https://{subdomain}.wufoo.com/api/v3/forms.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format

<aside class="notice">Our examples will all assume 'fishbowl' as the subdomain and 'json' as the format </aside>

### Query Parameters

Parameter          | Default | Description
------------------ | ------- | -----------
includeTodaysCount | false   | If set to true, includes the number of entries received today
pretty             | false   | If set to true, returns the result in a "pretty print" format

<aside class="success">
Remember you'll need to authenticate to access this or any other resource
</aside>

## Get a Specific Form

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7.json?pretty=true"
```

> The above command returns JSON structured like this:

```json
{
  "Fields": [
    {
      "Title": "Entry Id",
      "Type": "text",
      "ID": "EntryId"
    },
    {
      "Title": "Single Line Text",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "text",
      "ID": "Field105"
    },
    {
      "Title": "Number",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "number",
      "ID": "Field106"
    },
    {
      "Title": "Paragraph",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "textarea",
      "ID": "Field107"
    },
    {
      "Title": "Checkbox",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "0",
      "Page": "1",
      "SubFields": [
        {
        "DefaultVal": "0",
        "ID": "Field108",
        "Label": "Check One"
        },
        {
        "DefaultVal": "0",
        "ID": "Field109",
        "Label": "Check Two"
        },
        {
        "DefaultVal": "0",
        "ID": "Field110",
        "Label": "Check Three"
        }
      ],
      "Type": "checkbox",
      "ID": "Field108"
    },
    {
      "Title": "Multiple Choice",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Choices": [
        {
        "Label": "MC One"
        },
        {
        "Label": "MC Two"
        },
        {
        "Label": "MC Three"
        }
      ],
      "Type": "radio",
      "ID": "Field208",
      "HasOtherField": false
    },
    {
      "Title": "Dropdown",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Choices": [
        {
        "Label": ""
        },
        {
        "Label": "Dropdown One"
        },
        {
        "Label": "Dropdown Two"
        },
        {
        "Label": "Dropdown Three"
        }
      ],
      "Type": "select",
      "ID": "Field209",
      "HasOtherField": false
    },
    {
      "Title": "Name",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "SubFields": [
        {
        "DefaultVal": "",
        "ID": "Field1",
        "Label": "First"
        },
        {
        "DefaultVal": "",
        "ID": "Field2",
        "Label": "Last"
        }
      ],
      "Type": "shortname",
      "ID": "Field1"
    },
    {
      "Title": "File Upload",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "file",
      "ID": "Field210"
    },
    {
      "Title": "Address",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "SubFields": [
        {
        "DefaultVal": "",
        "ID": "Field211",
        "Label": "Street Address"
        },
        {
        "DefaultVal": "",
        "ID": "Field212",
        "Label": "Address Line 2"
        },
        {
        "DefaultVal": "",
        "ID": "Field213",
        "Label": "City"
        },
        {
        "DefaultVal": "",
        "ID": "Field214",
        "Label": "State / Province / Region"
        },
        {
        "DefaultVal": "",
        "ID": "Field215",
        "Label": "Postal / Zip Code"
        },
        {
        "DefaultVal": "",
        "ID": "Field216",
        "Label": "Country"
        }
      ],
      "Type": "address",
      "ID": "Field211"
    },
    {
      "Title": "Date",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "date",
      "ID": "Field217"
    },
    {
      "Title": "Email",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "email",
      "ID": "Field218"
    },
    {
      "Title": "Time",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "time",
      "ID": "Field219"
    },
    {
      "Title": "Phone Number",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "phone",
      "ID": "Field220"
    },
    {
      "Title": "Website",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "url",
      "ID": "Field221"
    },
    {
      "Title": "Price",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "money",
      "ID": "Field222"
    },
    {
      "Title": "Likert",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "0",
      "Page": "1",
      "SubFields": [
        {
        "DefaultVal": "0",
        "ID": "Field4",
        "Label": "Wufoo is Fun"
        },
        {
        "DefaultVal": "0",
        "ID": "Field5",
        "Label": "Wufoo Is Pretty"
        },
        {
        "DefaultVal": "0",
        "ID": "Field6",
        "Label": "Wufoo is Your Friend"
        }
      ],
      "Choices": [
        {
        "Score": 1,
        "Label": "Strongly Disagree"
        },
        {
        "Score": 2,
        "Label": "Disagree"
        },
        {
        "Score": 3,
        "Label": "Agree"
        },
        {
        "Score": 4,
        "Label": "Strongly Agree"
        }
      ],
      "Type": "likert",
      "ID": "Field4",
      "HasOtherField": false
    },
    {
      "Title": "Rating",
      "Instructions": "",
      "IsRequired": "0",
      "ClassNames": "",
      "DefaultVal": "",
      "Page": "1",
      "Type": "rating",
      "ID": "Field223"
    },
    {
      "Title": "Date Created",
      "Type": "date",
      "ID": "DateCreated"
    },
    {
      "Title": "Created By",
      "Type": "text",
      "ID": "CreatedBy"
    },
    {
      "Title": "Last Updated",
      "Type": "date",
      "ID": "LastUpdated"
    },
    {
      "Title": "Updated By",
      "Type": "text",
      "ID": "UpdatedBy"
    }
  ]
}

```

This endpoint retrieves a specific form. To identify the desired form, you can either use the form hash or the form title. 

<aside class="notice">You can find the form identifier in either the Easy to Remember or the Permanent form URLs</aside>

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/forms/{identifier}.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the form to retrieve

### Query Parameters

Parameter          | Default | Description
------------------ | ------- | -----------
includeTodaysCount | false   | If set to true, includes the number of entries received today
pretty             | false   | If set to true, returns the result in a "pretty print" format

## Get Form Fields

> The above command returns JSON structured like this:

```json
{
  "Forms": [
    {
      "Name": "Wufoo API Example",
      "Description": "This is my form. Please fill it out. It's awesome!",
      "RedirectMessage": "Success! Thanks for filling out my form!",
      "Url": "wufoo-api-example",
      "Email": "",
      "IsPublic": "1",
      "Language": "english",
      "StartDate": "2000-01-01 12:00:00",
      "EndDate": "2030-01-01 12:00:00",
      "EntryLimit": "0",
      "DateCreated": "0000-00-00 00:00:00",
      "DateUpdated": "0000-00-00 00:00:00",
      "Hash": "s1afea8b1vk0jf7",
      "LinkFields": "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/fields.json",
      "LinkEntries": "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries.json",
      "LinkEntriesCount": "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries/count.json"
    }
  ]
}

```

This endpoint retrieves the field structure for a specific form.

<aside class="notice">You'll use the same form identifier as you would for our Form request</aside>

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/fields.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the form to retrieve

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
system    | false   | If set to true, includes additional metadata fields
pretty    | false   | If set to true, returns the result in a "pretty print" format

# Entries

## Get Form Entries

## Get Form Entry Count

## Get Form Comments

## Get Form Comments Count

## Submit Entry

# Reports

## Get All Reports

## Get Specific Report

## Get Report Entries

## Get Report Fields

## Get Widgets

# Users

## Get Users

# Webhooks

## Add Webhook

## Delete Webhook

# Login

## Retrieve API Key


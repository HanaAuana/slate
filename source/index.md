---
title: Wufoo API

language_tabs:
  - shell: cURL
  - php: PHP
  - python: Python
  - node: Node
  - ruby: Ruby

toc_footers:
  - <a href='http://www.wufoo.com'>Wufoo</a>
  - <a href='http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Wufoo-REST-API-V3'>See our old docs</a>
  - <a href='http://github.com/tripit/slate'>Powered by Slate</a>

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
auth = HTTPBasicAuth('AOI6-LFKL-VM1Q-IEX9', 'footastic')
response  =requests.get(url, auth=auth)
response.json()
```

> Make sure to replace `AOI6-LFKL-VM1Q-IEX9` with your API key and `fishbowl` with your own subdomain. The second value `footastic` is required, but can be anything

Wufoo uses [Basic Auth](http://www.ietf.org/rfc/rfc2617.txt) with API Keys to allow access to the API. 

Wufoo expects for the API key to be included as the 'username' and any value as the 'password' portion of Basic Auth. If the service you're using doesn't have a built in way to authenticate using Basic Auth, you can set the Authorization header to a base64 encoded string:

`base64('username:password')`

After encoding, you can set the header like this:

`Authorization: Basic QU9JNi1MRktMLVZNMVEtSUVYOTpmb290YXN0aWM=`

<aside class="notice">
You'll need to replace 'username' with your API key, and password with any value (our examples use 'footastic')
</aside>

# Forms

## Get All Forms

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true"
```

```python
import requests
from requests.auth import HTTPBasicAuth

url = 'https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true'
auth = HTTPBasicAuth('AOI6-LFKL-VM1Q-IEX9', 'footastic')
response = requests.get(url, auth=auth)
response.json()
```

> The above request produces output in this format:

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

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7.json?pretty=true"
```

```python
import requests
from requests.auth import HTTPBasicAuth

url = 'https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7.json?pretty=true'
auth = HTTPBasicAuth('AOI6-LFKL-VM1Q-IEX9', 'footastic')
response = requests.get(url, auth=auth)
response.json()
```

> The above request produces output in this format:

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

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/fields.json?pretty=true"
```

```python
import requests
from requests.auth import HTTPBasicAuth

url = 'https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/fields.json?pretty=true'
auth = HTTPBasicAuth('AOI6-LFKL-VM1Q-IEX9', 'footastic')
response = requests.get(url, auth=auth)
response.json()
```

> The above request produces output in this format:

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

<b>Most of the properties for a Field object match the options set in your Field Settings. Here a few:</b>

Title - The Field Label.

Instructions - The Instructions for User (if any).

ClassNames - Any values that were added to the CSS Keywords option in the Form Builder.

ID - The API ID for that field. This is what you'll use for submitting new entries, or using URL Modification and Templating


<h4 id='checkbox'>Checkbox fields will have SubFields property that is an array of all the field options</h4>

```json
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
```
Notice how each SubField element also has it's own ID. This is what allows you to "check" more than one option

<h4 id='mc'>Multiple Choice fields have a Choices property that is an array of all options</h4>

```json
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
```

<h4 id='dd'>Dropdown fields also have a Choices property: an array of all options</h4>
```json
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
```
<h4 id='address'>Address fields have a SubFields property with one element for each part of the address</h4>
```json
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
```
<h4 id='likert'>Likert fields have a SubFields propertyfor the "rows" and a Choices property for the "columns"</h4>
```json
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
```
<h4 id='meta'>These are the default metadata fields</h4>
```json
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
<h4 id='system'>Here are the System Fields</h4>

```json
    {
      "Title":"Payment Status",
      "IsSystem":true,
      "Type":"text",
      "ID":"Status"
    },
    {
      "Title":"Payment Total",
      "IsSystem":true,
      "Type":"text",
      "ID":"PurchaseTotal"
    },
    {
      "Title":"Payment Currency",
      "IsSystem":true,
      "Type":"text",
      "ID":"Currency"
    },
    {
      "Title":"Payment Confirmation",
      "IsSystem":true,
      "Type":"text",
      "ID":"TransactionId"
    },
    {
      "Title":"Payment Merchant",
      "IsSystem":true,
      "Type":"text",
      "ID":"MerchantType"
    },
    {
      "Title":"IP Address",
      "IsSystem":true,
      "Type":"text",
      "ID":"IP"
    },
    {
      "Title":"Last Page Accessed",
      "IsSystem":true,
      "Type":"text",
      "ID":"LastPage"
    },
    {
      "Title":"Completion Status",
      "IsSystem":true,
      "Type":"text",
      "ID":"CompleteSubmission"
    }
```
These are only included if you set the `system=true` query parameter
If you set `system` to any value, the fields will be included, so if you don't want the System Fields, leave the `system` paramter out (Don't just set it to `false`). Also available in the Entries API for more details on the [System Fields](/#entries-system)

<b>The System Fields are:</b>

IP - The IP Address of the user submitting the form.

Last Page Accessed - If a user did not complete the form, this number represents the last page the user did submit.

Completion Status - Is a one or zero, representing either completed (1) or incomplete.

Status - Indicates what state your payment is in. An example is ‘Paid’. To see more payment types, check out the payment status documentation

PurchaseTotal - The total purchase, after discounts, etc.

Currency - The type of currency. An example is USD.

TransactionId - The confirmation number sent back from the merchant gateway.

MerchantType - The merchant name. An example is authnet


# Entries

## Get Form Entries

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/wufoo-api-example/entries.json?pretty=true&sort=EntryId&sortDirection=DESC"
```

> The above request produces output in this format:

```json
{
  "Entries" : [
    {
      "EntryId" : "9",
      "Field105" : "Some Text",
      "Field106" : "123",
      "Field107" : "Here is a Paragraph field. It can hold more text than a regular Single Line Text field. \r\nThis is a second line of text in the same field.",
      "Field108" : "Check One",
      "Field109" : "Check Two",
      "Field110" : "Check Three",
      "Field208" : "MC Two",
      "Field209" : "Dropdown Three",
      "Field1" : "Wufoo",
      "Field2" : "Test",
      "Field210" : "test.txt (https://fishbowl.wufoo.com/cabinet/s1afea8b1vk0jf7/gTVeAerMQyk%3D/test.txt)",
      "Field211" : "123 Street",
      "Field212" : "",
      "Field213" : "City",
      "Field214" : "CA",
      "Field215" : "12445",
      "Field216" : "United States",
      "Field217" : "2015-04-20",
      "Field218" : "test@wufoo.com",
      "Field219" : "00:34:56",
      "Field220" : "1231231234",
      "Field221" : "http://www.wufoo.com",
      "Field222" : "100.99",
      "Field4" : "Strongly Agree",
      "Field5" : "Agree",
      "Field6" : "Strongly Agree",
      "Field223" : "5",
      "DateCreated" : "2015-04-20 15:50:34",
      "CreatedBy" : "public",
      "DateUpdated" : "",
      "UpdatedBy" : null
    },
...
    {
      "EntryId" : "2",
      "Field105" : "",
      "Field106" : "",
      "Field107" : "",
      "Field108" : "",
      "Field109" : "",
      "Field110" : "",
      "Field208" : "",
      "Field209" : "",
      "Field1" : "Amber",
      "Field2" : "Des",
      "Field210" : "",
      "Field211" : "",
      "Field212" : "",
      "Field213" : "",
      "Field214" : "",
      "Field215" : "",
      "Field216" : "",
      "Field217" : "",
      "Field218" : "",
      "Field219" : "",
      "Field220" : "",
      "Field221" : "",
      "Field222" : null,
      "Field4" : "Agree",
      "Field5" : "Agree",
      "Field6" : "Disagree",
      "Field223" : "",
      "DateCreated" : "2008-11-24 09:46:04",
      "CreatedBy" : "public",
      "DateUpdated" : "",
      "UpdatedBy" : null
    },
    {
      "EntryId" : "1",
      "Field105" : "",
      "Field106" : "",
      "Field107" : "",
      "Field108" : "",
      "Field109" : "",
      "Field110" : "",
      "Field208" : "",
      "Field209" : "",
      "Field1" : "Tim",
      "Field2" : "Sabat",
      "Field210" : "",
      "Field211" : "",
      "Field212" : "",
      "Field213" : "",
      "Field214" : "",
      "Field215" : "",
      "Field216" : "",
      "Field217" : "",
      "Field218" : "",
      "Field219" : "",
      "Field220" : "",
      "Field221" : "",
      "Field222" : null,
      "Field4" : "Strongly Agree",
      "Field5" : "Strongly Agree",
      "Field6" : "Agree",
      "Field223" : "",
      "DateCreated" : "2008-11-24 09:45:28",
      "CreatedBy" : "public",
      "DateUpdated" : "",
      "UpdatedBy" : null
    }
  ]
}
```

This endpoint retrieves the entries from a specific form. 

<aside class="notice">To identify the desired form, use the form hash or the form title, just like the Form request. </aside>

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/forms/entries/{identifier}.{format}`


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
pageStart | 0       | The entry that the request will start from
pageSize  | 25      | The number of entries returned in the request (Maximum of 100)

<b>Every Entries API call returns five fields with every request. The Default Fields are:</b>

EntryId - This value is the unique identifier for your entry.

DateCreated - The date that this entry was submitted.

Created By - The person who created the entry. If submitted through a form, the value here will be public. If the submission originated in the Entry Manager this value will be the user name of the submitting user.

DateUpdated - The date that this entry was edited through the Entry Manager. If the submission has never been updated, this value will be blank.

UpdatedBy - The user name of the person who updated the entry in the Entry Manager will appear in this element.

<b id='entries-system'>The System Fields are:</b>

IP - The IP Address of the user submitting the form.

Last Page Accessed - If a user did not complete the form, this number represents the last page the user did submit.

Completion Status - Is a one or zero, representing either completed (1) or incomplete.

Status - Indicates what state your payment is in. An example is ‘Paid’. To see more payment types, check out the payment status documentation

PurchaseTotal - The total purchase, after discounts, etc.

Currency - The type of currency. An example is USD.

TransactionId - The confirmation number sent back from the merchant gateway.

MerchantType - The merchant name. An example is authnet

### Filtering

You can filter an Entries API request, similar to how the Wufoo [Entry Manager](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Entry-Manager#filter) works. Here's the format:

`Filter{##}={ID}+{Operator}+{Value}&match={Grouping}`

Parameter   | Description
----------- | -----------
Filter{##}  | {##} should just be a unique number to identify each filter (1, 2, 3, etc.)
{ID}        | The API Field ID for the field you want to use. These values are the same as the "ID" property in a [Fields](/#get-form-fields) request
{Operator}  | The comparison that will be used with the filter. See full list below.
{Value}     | The value to match with your filter
{Grouping}  | Allows you group your filters as 'AND' (all must match) or 'OR' (at least one must match)

<aside class="notice">We do not adjust your input fiter date/time, so all dates/times are interpreted as Eastern Standard Time (UTC - 5)</aside>

Here's an example:

`https://fishbowl.wufoo.com/api/v3/entries/s1afea8b1vk0jf7.json?Filter1=EntryId+Is_after+1&Filter2=EntryId+Is_before+200&match=AND`

<b>Valid Operators</b>

- Contains
- Does_not_contain
- Begins_with
- Ends_with
- Is_less_than
- Is_greater_than
- Is_on
- Is_before
- Is_after
- Is_not_equal_to
- Is_equal_to
- Is_not_NULL

### Sorting

Sorting can also be applied using additional query parameters in this format:

`sort={ID}&sortDirection={DESC|ASC}`

Parameter    | Default | Description
------------ | ------- | -----------
{ID}         | N/A     | The API Field ID for the field you want to use. These values are the same as the "ID" property in a [Fields](http://localhost:4567/#get-form-fields) request
sortDirection | ASC     | The order to sort returned entries: ASC (lowest to highest) or DESC (highest to lowest)

Example: 

`https://fishbowl.wufoo.com/api/v3/entries/s1afea8b1vk0jf7.json?sort=EntryId&sortDirection=DESC`

## Get Form Entries Count

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/entries/count.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the form to retrieve

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
pretty    | false   | If set to true, returns the result in a "pretty print" format

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries/count.json?pretty=true"
```
> The above request produces output in this format:

```json
{
  "EntryCount" : "8"
}
```

## Get Form Comments

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/comments.json?pretty=true"
```

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/comments.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the form to retrieve

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
pretty    | false   | If set to true, returns the result in a "pretty print" format
entryId   | N/A     | If set to a number, will only return comments for the specific entry
pageStart | 0       | The entry that the request will start from
pageSize  | @todo   | @todo

> The above request produces output in this format:

```json
{
  "Comments" : [
    {
      "CommentId" : "4",
      "EntryId" : "6",
      "Text" : "Here's another comment",
      "CommentedBy" : "fishbowl",
      "DateCreated" : "2015-04-20 15:37:56"
    },
    {
      "CommentId" : "2",
      "EntryId" : "8",
      "Text" : "Test Comment",
      "CommentedBy" : "fishbowl",
      "DateCreated" : "2015-04-20 15:37:42"
    },
    {
      "CommentId" : "3",
      "EntryId" : "8",
      "Text" : "Another Comment",
      "CommentedBy" : "fishbowl",
      "DateCreated" : "2015-04-20 15:37:47"
    }
  ]
}
```

<b>Here are the properties of each Comment:</b>

CommentId - A unique ID for this comment.

CommentedBy - The name of the person who commented on this entry.

DateCreated - The date on which the comment was made.

EntryId - Is the unique ID of the entry to which this comment is associated.

Text - The comment itself.

## Get Form Comments Count

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/comments/count.json?pretty=true"
```

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/comments/count.{format}`



### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the form to retrieve

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
pretty    | false   | If set to true, returns the result in a "pretty print" format


> The above request produces output in this format:

```json
{
  "Count" : 3
}
```

## Submit Entry

# Reports

## Get All Reports

## Get Specific Report

## Get Report Entries

## Get Report Entries Count

## Get Report Fields

## Get Widgets

# Users

## Get Users

# Webhooks

## Add Webhook

## Delete Webhook

# Login

## Retrieve API Key


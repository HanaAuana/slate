# Forms

## All Forms

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true"
```

```python
import urllib2
import json

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()
password_manager.add_password(None, base_url, username, password)
handler = urllib2.HTTPBasicAuthHandler(password_manager)
opener = urllib2.build_opener(handler)

urllib2.install_opener(opener)

response = urllib2.urlopen(base_url+'forms.json')
data = json.load(response)
print json.dumps(data, indent=4, sort_keys=True)
```

```ruby
require "net/http"
require "uri"
require "json"

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

uri = URI.parse(base_url+"forms.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

$response = curl_exec($curl);
$resultStatus = curl_getinfo($curl);

if($resultStatus['http_code'] == 200) {
    $json = json_decode($response);
    echo json_encode($json, JSON_PRETTY_PRINT);
} else {
    echo 'Call Failed '.print_r($resultStatus);
}
?>
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
    ...
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

This request returns details on all the forms you have permission to access. 

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
includeTodayCount  | false   | If set to true, includes the number of entries received today
pretty             | false   | If set to true, returns the result in a "pretty print" format

<aside class="success">
Remember you'll need to authenticate with your API Key to access this or any other resource
</aside>

Each Form will be displayed as a separate object made up of these properties:

Name - The title of the form specified in the Form Settings

Description - The description of the form as specified in the Form Settings

Redirect Message - The Confirmation message shown to users after they submit an entry

Url - This is the "easy to remember" URL used for the form. Since it changes when the form title is changed, we recommend using the "hashed" URL instead when you need a permanent link. Can be used as a form identifier in other requests

Email - A list of the email addresses that are set to receive Notification emails in the Notification Settings

IsPublic - Indicates whether or not the "Public" option is enabled, allowing anyone with the link to access the form Possible values are: 1 = true, 0 = false

Language - Indicates the language set for this account in the Form Settings

StartDate - The date/time the form will be accessible through the public URL

EndDate - The date/time the form will no longer be accessible through the public URL

EntryLimit - The maximum number of entries this form will accept before it is no longer accessible through the public URL

DateCreated - A timestamp of when the form was created. For a duplicated form, this will be the DateCreated for the original form

DateUpdated - A timestamp of when the form was lasted edited in the Wufoo Form Builder

Hash - A permanent, "hashed" value unique to this form on this user’s account. Can be used as a form identifier in other requests

LinkFields - Link to the Fields API for a list of this form's fields

LinkEntries - Link to the Entries API for a list of entries stored by this form

LinkEntriesCount - Link to the Entries API for a count of the entries stored by this form

## Form

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7.json?pretty=true"
```

```python
import urllib2
import json

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()
password_manager.add_password(None, base_url, username, password)
handler = urllib2.HTTPBasicAuthHandler(password_manager)
opener = urllib2.build_opener(handler)

urllib2.install_opener(opener)

response = urllib2.urlopen(base_url+'forms/s1afea8b1vk0jf7.json')
data = json.load(response)
print json.dumps(data, indent=4, sort_keys=True)
```

```ruby
require "net/http"
require "uri"
require "json"

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

uri = URI.parse(base_url+"forms/s1afea8b1vk0jf7.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

$response = curl_exec($curl);
$resultStatus = curl_getinfo($curl);

if($resultStatus['http_code'] == 200) {
    $json = json_decode($response);
    echo json_encode($json, JSON_PRETTY_PRINT);
} else {
    echo 'Call Failed '.print_r($resultStatus);
}
?>
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

This request returns a specific form. To identify the desired form, you can either use the form hash or the form title. 

<aside class="notice">You can find the form identifier in either the Easy to Remember or the Permanent form URLs. Making a request for all Forms will also allow you to locate the form identifiers</aside>

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
includeTodayCount  | false   | If set to true, includes the number of entries received today
pretty             | false   | If set to true, returns the result in a "pretty print" format

The Form properties are the same as in the All Forms request. The only difference is that this request will only return the identified form.

## Form Fields

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/fields.json?pretty=true"
```

```python
import urllib2
import json

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()
password_manager.add_password(None, base_url, username, password)
handler = urllib2.HTTPBasicAuthHandler(password_manager)
opener = urllib2.build_opener(handler)

urllib2.install_opener(opener)

response = urllib2.urlopen(base_url+'forms/s1afea8b1vk0jf7/fields.json')
data = json.load(response)
print json.dumps(data, indent=4, sort_keys=True)
```

```ruby
require "net/http"
require "uri"
require "json"

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

uri = URI.parse(base_url+"forms/s1afea8b1vk0jf7/fields.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/fields.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

$response = curl_exec($curl);
$resultStatus = curl_getinfo($curl);

if($resultStatus['http_code'] == 200) {
    $json = json_decode($response);
    echo json_encode($json, JSON_PRETTY_PRINT);
} else {
    echo 'Call Failed '.print_r($resultStatus);
}
?>
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
      "IsRequired": "1",
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



This request returns the field structure for a specific form.

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

IsRequired - Whether or not the field has been marked as Required in the Field Settings. This value can be 1 = true or 0 = false

ClassNames - Any values that were added to the CSS Keywords option in the Form Builder.

ID - The API ID for that field. This is what you'll use for [submitting new entries](/#submit-entry), or using URL Modification and Templating

Label - If a field has a SubFields or Choices property (meaning there are multiple fields or options), each sub-field or choice will have its own label. This is the value stored for Dropdown, Multiple Choice, or Checkbox fields. For fields like Name and Address, these are the values of the different sub-fields 

DefaultVal - If the field has a Predefined Value set in the Field Settings, it will be displayed here. Otherwise, the value will be "0"

Page - Indicates which page of the form the field is added to. On a single page form (no Page Breaks) all fields will be on Page 1


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
Multiple Choice fields have a `HasOtherField` property:

HasOtherField - This value is either true or false and is only set if the "Allow Other" option was enabled in the Field Settings. When the HasOtherField is true, the last choice is the "other" field.

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
Dropdown fields have the `HasOtherField` property as well, but they can't actually use the "Allow Other" option like Multiple Choice fields.


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
```
Each choice also has a Score property, representing that choice's "value" relative to the other choices. If the Not Applicable option is enabled in the Field Settings, there will be an additional Choice with a score of 0

```json 
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
These are only included if you set the `system` query parameter.
If you set `system` to any value (`system=true`, `system=false`, etc), the fields will be included, so if you don't want the System Fields, leave the `system` paramter out (Don't just set it to `false`). This parameter is also available in the [Entries API](/#entries-system)

<b>The System Fields are:</b>

IP - The IP Address of the user submitting the form.

LastPage - This represents the last page the user submitted.

CompleteSubmission - Represents either a completed (`1`) or incomplete/partial (`0`) entry.

Status - Indicatesthe payment status. An example is ‘Paid’. More info [here](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Entry-Manager#payment)

PurchaseTotal - The total amount charged for the transaction. This is the final total we send to the payment processor

Currency - The currency used. This is the currency value we send to the payment processor

TransactionId - The confirmation number sent back from the payment processor.

MerchantType - The name of the payment processor used. This is determined by which pyament integration is set up. There is a full list [here](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Payment-Settings)

## Form Comments

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/comments.json?pretty=true"
```

```python
import urllib2
import json

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()
password_manager.add_password(None, base_url, username, password)
handler = urllib2.HTTPBasicAuthHandler(password_manager)
opener = urllib2.build_opener(handler)

urllib2.install_opener(opener)

response = urllib2.urlopen(base_url+'forms/s1afea8b1vk0jf7/comments.json')
data = json.load(response)
print json.dumps(data, indent=4, sort_keys=True)
```

```ruby
require "net/http"
require "uri"
require "json"

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

uri = URI.parse(base_url+"forms/s1afea8b1vk0jf7/comments.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/comments.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

$response = curl_exec($curl);
$resultStatus = curl_getinfo($curl);

if($resultStatus['http_code'] == 200) {
    $json = json_decode($response);
    echo json_encode($json, JSON_PRETTY_PRINT);
} else {
    echo 'Call Failed '.print_r($resultStatus);
}
?>
```

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

This request returns any comments made on this form's entries in the [Entry Manager](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Entry-Manager)

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
pageSize  | 25      | The number of entries returned in the request (Maximum of 100)

<b>Here are the properties of each Comment:</b>

CommentId - A unique ID for this comment.

CommentedBy - The name of the person who commented on this entry.

DateCreated - The date on which the comment was made.

EntryId - Is the unique ID of the entry to which this comment is associated.

Text - The comment itself.

## Comments Count

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/comments/count.json?pretty=true"
```

```python
import urllib2
import json

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()
password_manager.add_password(None, base_url, username, password)
handler = urllib2.HTTPBasicAuthHandler(password_manager)
opener = urllib2.build_opener(handler)

urllib2.install_opener(opener)

response = urllib2.urlopen(base_url+'forms/s1afea8b1vk0jf7/comments/count.json')
data = json.load(response)
print json.dumps(data, indent=4, sort_keys=True)
```

```ruby
require "net/http"
require "uri"
require "json"

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

uri = URI.parse(base_url+"forms/s1afea8b1vk0jf7/comments/count.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/comments/count.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

$response = curl_exec($curl);
$resultStatus = curl_getinfo($curl);

if($resultStatus['http_code'] == 200) {
    $json = json_decode($response);
    echo json_encode($json, JSON_PRETTY_PRINT);
} else {
    echo 'Call Failed '.print_r($resultStatus);
}
?>
```

> The above request produces output in this format:

```json
{
  "Count" : 3
}
```

This request returns a count of all comments made on this form's entries 

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

# Reports

## All Reports

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports.json?pretty=true"
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

response = urllib2.urlopen(base_url+'reports.json')
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

uri = URI.parse(base_url+"reports.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/reports.json');
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
  "Reports" : [
    {
      "Name" : "Colors",
      "IsPublic" : "0",
      "Url" : "colors",
      "Description" : null,
      "DateCreated" : "0000-00-00 00:00:00",
      "DateUpdated" : "0000-00-00 00:00:00",
      "Hash" : "mbrtcpw036ecgn",
      "LinkFields" : "https://fishbowl.wufoo.com/api/v3/reports/mbrtcpw036ecgn/fields.json?pretty=true",
      "LinkEntries" : "https://fishbowl.wufoo.com/api/v3/reports/mbrtcpw036ecgn/entries.json?pretty=true",
      "LinkEntriesCount" : "https://fishbowl.wufoo.com/api/v3/reports/mbrtcpw036ecgn/entries/count.json?pretty=true",
      "LinkWidgets" : "https://fishbowl.wufoo.com/api/v3/reports/mbrtcpw036ecgn/widgets.json?pretty=true"
    },
    {
      "Name" : "Example Report",
      "IsPublic" : "0",
      "Url" : "example-report",
      "Description" : "This is my report. View it in all its glory!",
      "DateCreated" : "2015-04-21 11:02:04",
      "DateUpdated" : "2015-04-21 11:02:04",
      "Hash" : "qa4d98l1ib9or7",
      "LinkFields" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/fields.json?pretty=true",
      "LinkEntries" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries.json?pretty=true",
      "LinkEntriesCount" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries/count.json?pretty=true",
      "LinkWidgets" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/widgets.json?pretty=true"
    },
    {
      "Name" : "Names",
      "IsPublic" : "1",
      "Url" : "names",
      "Description" : null,
      "DateCreated" : "0000-00-00 00:00:00",
      "DateUpdated" : "0000-00-00 00:00:00",
      "Hash" : "z1qlusp218ylc12",
      "LinkFields" : "https://fishbowl.wufoo.com/api/v3/reports/z1qlusp218ylc12/fields.json?pretty=true",
      "LinkEntries" : "https://fishbowl.wufoo.com/api/v3/reports/z1qlusp218ylc12/entries.json?pretty=true",
      "LinkEntriesCount" : "https://fishbowl.wufoo.com/api/v3/reports/z1qlusp218ylc12/entries/count.json?pretty=true",
      "LinkWidgets" : "https://fishbowl.wufoo.com/api/v3/reports/z1qlusp218ylc12/widgets.json?pretty=true"
    }
  ]
}
```

This request returns details on all the reports you have permission to access. 

### HTTP Request

`GET https://{subdomain}.wufoo.com/api/v3/reports.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format

### Query Parameters

Parameter          | Default | Description
------------------ | ------- | -----------
pretty             | false   | If set to true, returns the result in a "pretty print" format

Each Report will be displayed as a separate object made up of these properties:

Name - The title of the report specified in the Report Builder

Description - The description of the report as specified in the Report Builder

Url - This is the "easy to remember" URL used for the report. Since it changes when the report title is changed, we recommend using the "hashed" URL instead when you need a permanent link. Can be used as a report identifier in other requests

IsPublic - Indicates whether or not the "Public" option is enabled, allowing anyone with the link to access the report. Possible values are: 1 = true, 0 = false

DateCreated - A timestamp of when the report was created. For a duplicated report, this will be the DateCreated for the original report @todo

DateUpdated - A timestamp of when the report was lasted edited in the Wufoo Report Builder

Hash - A permanent, "hashed" value unique to this report on this user’s account. Can be used as a report identifier in other requests

LinkFields - Link to the Report Fields API for a list of this report's fields

LinkEntries - Link to the Report Entries API for a list of entries stored by this report

LinkEntriesCount - Link to the Report Entries API for a count of the entries stored by this report

LinkWidgets - Link to the Widgets API for the widgets that make up this report

## Report

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7.json?pretty=true"
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

response = urllib2.urlopen(base_url+'reports/qa4d98l1ib9or7.json')
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

uri = URI.parse(base_url+"reports/qa4d98l1ib9or7.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7.json');
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
  "Reports" : [
    {
      "Name" : "Example Report",
      "IsPublic" : "0",
      "Url" : "example-report",
      "Description" : "This is my report. View it in all its glory!",
      "DateCreated" : "2015-04-21 11:02:04",
      "DateUpdated" : "2015-04-21 11:02:04",
      "Hash" : "qa4d98l1ib9or7",
      "LinkFields" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/fields.json?pretty=true",
      "LinkEntries" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries.json?pretty=true",
      "LinkEntriesCount" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries/count.json?pretty=true",
      "LinkWidgets" : "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/widgets.json?pretty=true"
    }
  ]
}
```

This request returns a specific report. To identify the desired report, you can either use the report hash or the report title. 

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/reports/{identifier}.{format}`

<aside class="notice">You can find the report identifier in the report URL, or through a <a href='/#reports'>Reports</a> request</aside>

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the report to retrieve

### Query Parameters

Parameter          | Default | Description
------------------ | ------- | -----------
pretty             | false   | If set to true, returns the result in a "pretty print" format

The Report properties are the same as in the All Reporst request. The only difference is that this request will only return the identified report.

## Report Entries

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries.json?pretty=true"
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

response = urllib2.urlopen(base_url+'reports/qa4d98l1ib9or7/entries.json')
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

uri = URI.parse(base_url+"reports/qa4d98l1ib9or7/entries.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries.json');
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
  "Entries" : [
    {
      "EntryId" : "1",
      "Field105" : "",
      "Field106" : "",
      "Field107" : "",
      "Field108" : "",
      "Field208" : "",
      "Field209" : "",
      "Field1" : "Tim",
      "Field210" : "",
      "Field211" : "",
      "Field217" : "",
      "DateCreated" : "2008-11-24 09:45:28"
    },
    {
      "EntryId" : "2",
      "Field105" : "",
      "Field106" : "",
      "Field107" : "",
      "Field108" : "",
      "Field208" : "",
      "Field209" : "",
      "Field1" : "Amber",
      "Field210" : "",
      "Field211" : "",
      "Field217" : "",
      "DateCreated" : "2008-11-24 09:46:04"
    },
...
    {
      "EntryId" : "9",
      "Field105" : "Some Text",
      "Field106" : "123",
      "Field107" : "Here is a Paragraph field. It can hold more text than a regular Single Line Text field. \r\nThis is a second line of text in the same field.",
      "Field108" : "Check One",
      "Field208" : "MC Two",
      "Field209" : "Dropdown Three",
      "Field1" : "Wufoo",
      "Field210" : "test.txt (https://fishbowl.wufoo.com/cabinet/s1afea8b1vk0jf7/gTVeAerMQyk%3D/test.txt)",
      "Field211" : "123 Street",
      "Field217" : "2015-04-20",
      "DateCreated" : "2015-04-20 15:50:34"
    }
  ]
}
```

This request returns the entries that make up a specific report. 

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

This is essentially an equivalent of the data that would show up in a datagrid widget on the report, or in an exported copy of the report entry data

<aside class="notice">For more details on entry objects, see <a href='/#form-entries'>Form Entries</a></aside>

## Report Entries Count

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries/count.json?pretty=true"
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

response = urllib2.urlopen(base_url+'reports/qa4d98l1ib9or7/entries/count.json')
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

uri = URI.parse(base_url+"reports/qa4d98l1ib9or7/entries/count.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries/count.json');
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
  "EntryCount" : "9"
}
```

This request returns a count of the entries stored for a specific report. This can help with determining the number of elements you have to display. 

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/reports/{identifier}/entries/count.{format}`

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

## Report Fields

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/fields.json?pretty=true"
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

response = urllib2.urlopen(base_url+'reports/qa4d98l1ib9or7/fields.json')
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

uri = URI.parse(base_url+"reports/qa4d98l1ib9or7/fields.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/fields.json');
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
  "Fields" : [
    {
      "Title" : "Single Line Text",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "text",
      "ID" : "Field105"
    },
    {
      "Title" : "Number",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "number",
      "ID" : "Field106"
    },
    {
      "Title" : "Paragraph",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "textarea",
      "ID" : "Field107"
    },
    {
      "Title" : "Checkbox",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "0",
      "Page" : "1",
      "SubFields" : [
        {
          "DefaultVal" : "0",
          "ID" : "Field108",
          "Label" : "Check One"
        },
        {
          "DefaultVal" : "0",
          "ID" : "Field109",
          "Label" : "Check Two"
        },
        {
          "DefaultVal" : "0",
          "ID" : "Field110",
          "Label" : "Check Three"
        }
      ],
      "Type" : "checkbox",
      "ID" : "Field108"
    },
    {
      "Title" : "Multiple Choice",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Choices" : [
        {
          "Label" : "MC One"
        },
        {
          "Label" : "MC Two"
        },
        {
          "Label" : "MC Three"
        }
      ],
      "Type" : "radio",
      "ID" : "Field208",
      "HasOtherField" : false
    },
    {
      "Title" : "Dropdown",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Choices" : [
        {
          "Label" : ""
        },
        {
          "Label" : "Dropdown One"
        },
        {
          "Label" : "Dropdown Two"
        },
        {
          "Label" : "Dropdown Three"
        }
      ],
      "Type" : "select",
      "ID" : "Field209",
      "HasOtherField" : false
    },
    {
      "Title" : "Name",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "SubFields" : [
        {
          "DefaultVal" : "",
          "ID" : "Field1",
          "Label" : "First"
        },
        {
          "DefaultVal" : "",
          "ID" : "Field2",
          "Label" : "Last"
        }
      ],
      "Type" : "shortname",
      "ID" : "Field1"
    },
    {
      "Title" : "File Upload",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "file",
      "ID" : "Field210"
    },
    {
      "Title" : "Address",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "SubFields" : [
        {
          "DefaultVal" : "",
          "ID" : "Field211",
          "Label" : "Street Address"
        },
        {
          "DefaultVal" : "",
          "ID" : "Field212",
          "Label" : "Address Line 2"
        },
        {
          "DefaultVal" : "",
          "ID" : "Field213",
          "Label" : "City"
        },
        {
          "DefaultVal" : "",
          "ID" : "Field214",
          "Label" : "State / Province / Region"
        },
        {
          "DefaultVal" : "",
          "ID" : "Field215",
          "Label" : "Postal / Zip Code"
        },
        {
          "DefaultVal" : "",
          "ID" : "Field216",
          "Label" : "Country"
        }
      ],
      "Type" : "address",
      "ID" : "Field211"
    },
    {
      "Title" : "Date",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "date",
      "ID" : "Field217"
    },
    {
      "Title" : "Email",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "email",
      "ID" : "Field218"
    },
    {
      "Title" : "Time",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "time",
      "ID" : "Field219"
    },
    {
      "Title" : "Phone Number",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "phone",
      "ID" : "Field220"
    },
    {
      "Title" : "Website",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "url",
      "ID" : "Field221"
    },
    {
      "Title" : "Amount",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "money",
      "ID" : "Field222"
    },
    {
      "Title" : "Rating",
      "Instructions" : "",
      "IsRequired" : "0",
      "ClassNames" : "",
      "DefaultVal" : "",
      "Page" : "1",
      "Type" : "rating",
      "ID" : "Field223"
    },
    {
      "Title" : "Date Created",
      "Type" : "date",
      "ID" : "DateCreated"
    },
    {
      "Title" : "Last Updated",
      "Type" : "date",
      "ID" : "LastUpdated"
    }
  ]
}
```

This request returns the field structure for the report's corresponding form.

`GET http://{subdomain}.wufoo.com/api/v3/reports/{identifier}/fields.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the report to retrieve

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
system    | false   | If set to true, includes additional metadata fields
pretty    | false   | If set to true, returns the result in a "pretty print" format

<aside class="notice">Report fields are the field for the form the report is based on. For more, see <a href='/#form-fields'>Form Fields</a></aside>

## Widgets

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/widgets.json?pretty=true"
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

response = urllib2.urlopen(base_url+'reports/qa4d98l1ib9or7/widgets.json')
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

uri = URI.parse(base_url+"reports/qa4d98l1ib9or7/widgets.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/widgets.json');
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
  "Widgets" : [
    {
      "Name" : "Graph Widget",
      "Size" : "small",
      "Hash" : "jKyonpg4od1IeSBnJxqqc8n0N6kyD38YOofKjPwuslash5MI8=",
      "Type" : "pie",
      "TypeDesc" : "Pie Graph"
    },
    {
      "Name" : "Chart Widget",
      "Size" : "fill",
      "Hash" : "Dv0H6fRnzFwuBeWzVLhJailsckhmKzVQVjFxPMGI7S4olI=",
      "Type" : "fieldChart",
      "TypeDesc" : "Chart"
    },
    {
      "Name" : "Number Widget",
      "Size" : "fill",
      "Hash" : "krr7b7sEMLwuslashlfS8PVwuBe7wTk46plu7IwuBeUAZVWrR7qYhgA=",
      "Type" : "bigNumber",
      "TypeDesc" : "Number"
    }
  ]
}
```

This request returns details of the widgets that make up a specific report.

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/reports/{identifier}/widgets.{format}`

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

Only Chart, Graph, and Number widgets will be included in the request. Any Text or Datagrid widgets will not be shown. Each widget element will have the following properties:

Name - This is the name you chose when creating this widget in the Report Builder.

Size - Graphs (pie, bar, line) can be `small`, `medium` or `large`. Charts (fieldChart) will have a size of `fill` because they always fill the container they are placed in. Big Numbers (bigNumber) will also have a size of `fill` because they are all one size.

Type - The identifier for the widget type. Valid `type` values are `fieldChart`, `bigNumber`, `bar`, `line`, and `pie`.

TypeDesc - A user-friendly version of the Widget type.

Hash - An unchanging value representing this specific widget on this specific form.

<h4 id='embed-widget'>The hash code for a widget can be used to embed the widget using Javascript</h4>

> Example widget embed code:

```html
<script type="text/javascript">
  var host = (("https:" == document.location.protocol) ? "https://" : "http://");
  document.write(unescape("%3Cscript src='" + host + "{subdomain}.wufoo.com/scripts/widget/embed.js?w={Hash}' type='text/javascript'%3E%3C/script%3E"));
</script>
```

>Where {subdomain} is your account subdomain and {Hash} is your widget's hash code
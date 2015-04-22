# Reports

## All Reports

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports.json?pretty=true"
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

This endpoint retrieves all reports.

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

## Report

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7.json?pretty=true"
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

This endpoint retrieves a specific report. To identify the desired report, you can either use the report hash or the report title. 

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

## Report Entries

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries.json?pretty=true"
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

This endpoint retrieves the entries from a specific report. 

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

<aside class="notice">For more details on entry objects, see <a href='/#form-entries'>Form Entries</a></aside>

## Report Entries Count

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/reports/qa4d98l1ib9or7/entries/count.json?pretty=true"
```
> The above request produces output in this format:

```json
{
  "EntryCount" : "9"
}
```

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

Name - Is the widget name. This is the friendly name you chose when creating this widget.

Size - Graphs (pie, bar, line) have the sizes small, medium and large. Field Charts (fieldChart) have a size of ‘fill’ because they always fill the container they are placed in. Big Numbers (bigNumber) have a size of ‘fixed’ because they are all one size.

Type - The identifier for the widget type. Valid Typeof values are fieldChart, bigNumber, bar, line, and pie.

TypeDesc - A user-friendly version of Typeof.

Hash - An unchanging value representing this widget.


<h4 id='embed-widget'>The hash code for a widget can be used to embed the widget using Javascript</h4>

> Example widget embed code:

```html
<script type="text/javascript">
  var host = (("https:" == document.location.protocol) ? "https://" : "http://");
  document.write(unescape("%3Cscript src='" + host + "{subdomain}.wufoo.com/scripts/widget/embed.js?w={Hash}' type='text/javascript'%3E%3C/script%3E"));
</script>
```

>Where {subdomain} is your account subdomain and {Hash} is your widget's hash code
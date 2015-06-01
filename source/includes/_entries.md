# Entries

## Form Entries

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
{ID}        | The API Field ID for the field you want to use. These values are the same as the "ID" property in a [Fields](/#form-fields) request
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
{ID}         | N/A     | The API Field ID for the field you want to use. These values are the same as the "ID" property in a [Fields](/#form-fields) request
sortDirection | ASC     | The order to sort returned entries: ASC (lowest to highest) or DESC (highest to lowest)

Example: 

`https://fishbowl.wufoo.com/api/v3/entries/s1afea8b1vk0jf7.json?sort=EntryId&sortDirection=DESC`

## Form Entries Count

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries/count.json?pretty=true"
```
> The above request produces output in this format:

```json
{
  "EntryCount" : "8"
}
```

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

## Form Comments

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/comments.json?pretty=true"
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

> The above request produces output in this format:

```json
{
  "Count" : 3
}
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

## Submit Entry 

```shell
curl -X POST -d "Field1=Wufoo" -d "Field2=Test" -d "Field105=API-Test" -d "Field106=42" -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries.json"
```
> The above request will recieve a response in this format:

```json
{
  "Success": 1,
  "EntryId": 10,
  "EntryLink": "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries.json?Filter1=EntryId+Is_equal_to+10",
  "RedirectUrl":"http://wufoo.com"
}
```

This endpoint allows you to submit a new entry to a specific form. 

### HTTP Request

`POST http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/entries.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the form to retrieve

### POST Parameters

To submit an entry to a form, you'll need to match the API ID values for each field in the form. You can find these values through a [Form Fields](/#form-fields) request, or through your form's [API Information](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Templating#api) page.

The POST request should contain the data for the new entry submission in key/value pairs. The key will be the API ID in the format of `Field##`, where `##` is the API ID for the given field. The value will be your desired entry data, which will be recorded as if a user had submitted that value on the form manually.

Here's an example of what the key/value pairs might look like:

`{
    "Field1":   "Wufoo", 
    "Field2":   "Test", 
    "Field105": "API-Test",
    "Field106": "42"
 }`

### Response
When you make the Entries POST, you'll receive a PostResponse object containing the following:

Property    | Description
---------   | -----------
Success     | Will be '1' if the submission was a success. If the submission [failed](/#failed-submissions), it will be '0'
EntryId     | If the submission was a success, this value will be the EntryId assigned to this submission
EntryLink   | If the submission was a success, this value will be the URL for an [Entries](/#form-entries) request, filtered for this entry
RedirectUrl | If the form has a [Redirect](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Form-Settings#confirmation) set up, that URL will be included in the response

>Note this POST request is missing a value for Field105 (a required Text field) and has a text value submitted for Field106 (a Number field)

```shell
curl -X POST -d "Field1=Wufoo" -d "Field2=Test" -d "Field106=test" -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/entries.json"
```

>Here is the corresponding "failed" PostResponse

```json
{
    "RedirectUrl":"http://wufoo.com",
    "Success":0,
    "ErrorText":"Errors have been <b>highlighted<\/b> below.",
    "FieldErrors":[
        {
          "ID":"Field105",
          "ErrorText":"This field is required. Please enter a value."
        },
        {
          "ID":"Field106",
          "ErrorText":"Please enter a numeric value."
        }
    ]
}
```

### Failed Submissions

An Entries POST can fail for a few different reasons. A submission through the API must still adhere to any [field validation](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Field-Settings) or [form activity limits](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Form-Settings#limit). If these are not respected, the PostResponse will return with a 'Success' value of '0'. In this case, the PostResponse will contain some alternate properties:

Property    | Description
---------   | -----------
Success     | Will be '0' if the submission failed.
ErrorText   | This is some general text related to the error. Equivalent to what would be shown to the user on the actual form
FieldErrors | This will be an array of ID and ErrorText pairs for each affected field. These would be any error displayed on the field itself
RedirectUrl | If the form has a [Redirect](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Form-Settings#confirmation) set up, that URL will be included in the response

### Restrictions

Additionally, it is not possible to make an Entry POST request to a private form, even if the user making the request (the API Key used) has permissions to view/edit that form, or is an Administrator. If you need a "protected" form which can accept submissions via the API, you can use this alternate setup:

1. Set the form to Public in the [Form Manager](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Form-Manager#public).
2. Add a password to prevent unauthorized access.
3. Access the form via the API using a key with permissions to view/edit that form.
# Users

## Users

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/users.json?pretty=true"
```
> The above request produces output in this format:

```json
{
  "Users" : [
    {
      "User" : "fishbowl",
      "Email" : "fishbowl@wufoo.com",
      "TimeZone" : "",
      "Company" : "",
      "IsAccountOwner" : "1",
      "CreateForms" : "1",
      "CreateReports" : "1",
      "CreateThemes" : "1",
      "AdminAccess" : "0",
      "Image" : "boy_1",
      "ApiKey" : "AOI6-LFKL-VM1Q-IEX9",
      "LinkForms" : "https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true",
      "LinkReports" : "https://fishbowl.wufoo.com/api/v3/reports.json?pretty=true",
      "Hash" : "b1fe5l920lqsh58",
      "ImageUrlBig" : "https://wufoo.com/images/avatars/big/boy_1.png",
      "ImageUrlSmall" : "https://wufoo.com/images/avatars/small/boy_1.png",
      "HttpsEnabled" : "1"
    },
    {
      "User" : "User With No Permissions",
      "Email" : "fishy@wufoo.com",
      "TimeZone" : "-12.00",
      "Company" : "",
      "IsAccountOwner" : "0",
      "CreateForms" : "0",
      "CreateReports" : "0",
      "CreateThemes" : "0",
      "AdminAccess" : "0",
      "Image" : "animal_10",
      "ApiKey" : "EL2P-RPCO-HD1W-SX96",
      "LinkForms" : "https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true",
      "LinkReports" : "https://fishbowl.wufoo.com/api/v3/reports.json?pretty=true",
      "Hash" : "k78jvgk0l2lbz7",
      "ImageUrlBig" : "https://wufoo.com/images/avatars/big/animal_10.png",
      "ImageUrlSmall" : "https://wufoo.com/images/avatars/small/animal_10.png",
      "HttpsEnabled" : "1"
    },
    {
      "User" : "Administrator",
      "Email" : "test@wufoo.com",
      "TimeZone" : "",
      "Company" : "",
      "IsAccountOwner" : "0",
      "CreateForms" : "1",
      "CreateReports" : "1",
      "CreateThemes" : "1",
      "AdminAccess" : "1",
      "Image" : "doll_10",
      "ApiKey" : "D71P-FARY-REB1-GN4W",
      "LinkForms" : "https://fishbowl.wufoo.com/api/v3/forms.json?pretty=true",
      "LinkReports" : "https://fishbowl.wufoo.com/api/v3/reports.json?pretty=true",
      "Hash" : "n1ojkirv01rmc7h",
      "ImageUrlBig" : "https://wufoo.com/images/avatars/big/doll_10.png",
      "ImageUrlSmall" : "https://wufoo.com/images/avatars/small/doll_10.png",
      "HttpsEnabled" : "1"
    }
  ]
}
```

### HTTP Request

`GET http://{subdomain}.wufoo.com/api/v3/users.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
pretty    | false   | If set to true, returns the result in a "pretty print" format

User properties are as follows:

User: Is the user name. This is the friendly name you chose when creating this user.

Email: The email address on file for this user.

Timezone: an offset from UTC.

Company: The company defined when this user was created.

IsAccountOwner: Binary value indicating a yes (1) or (0). If the user is an account owner the Create(Forms/Reports/Themes) and AdminAccess values are ignored, as an AccountOwner has full rights to the account.

CreateForms: Binary value indicating whether or not this user may create forms.

CreateReports: Binary value indicating whether or not this user may create reports.

CreateThemes: Binary value indicating whether or not this user may create themes.

AdminAccess: This is an all-inclusive access right. In other words, if a user has this permission, they may create forms/reports/themes and administer users.

ApiKey: The authentication token permitting the user to make requests against the system.

Hash: An unchanging value representing the user.

ImageUrl: Links to the images used for the user's avatar in Wufoo

HttpsEnabled: No longer needed, since all Wufoo forms now use HTTPS unless you decide to [manually disable](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/URL-Modifications#ssl) it through the link or embed code
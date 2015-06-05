# Users

## Users

```shell
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/users.json?pretty=true"
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

response = urllib2.urlopen(base_url+'users.json')
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

uri = URI.parse(base_url+"users.json")

request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/users.json');
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

This request returns details of your account's sub-users, including the API Key for each user.

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

Each user will have the following properties:

User: This is the name chosen when creating this user.

Email: The email address on file for this user.

Timezone: The offset from UTC used for certain account timestamps.

Company: The company defined when this user was created.

IsAccountOwner: Indicates whether the user is the Account Creator. If the user is AccountCreator, the Create(Forms/Reports/Themes) and AdminAccess values are ignored, as an AccountOwner has full rights to the account. Values can be `1` (yes) or `0` (no)

CreateForms: Indicates whether or not this user may create forms. Values can be `1` (yes) or `0` (no)

CreateReports: Binary value indicating whether or not this user may create reports. Values can be `1` (yes) or `0` (no)

CreateThemes: Binary value indicating whether or not this user may create themes. Values can be `1` (yes) or `0` (no)

AdminAccess: This indicates if the user has been designated as an Administrator. If a user has this permission, they may create forms/reports/themes and administer users. Values can be `1` (yes) or `0` (no)

ApiKey: The authentication value used to make API requests for this account. Each API Key is restricted by that user's permissions as set in the account's [Users tab](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/User-Management)

Hash: An unchanging value representing the user on this account.

ImageUrl: Links to the images used for the user's avatar in Wufoo

HttpsEnabled: No longer used, since all accounts can use HTTPS. All Wufoo forms now use HTTPS automatically, unless you decide to [manually disable](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/URL-Modifications#ssl) it through the link or embed code
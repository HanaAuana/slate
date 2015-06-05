# Login

## Retrieve API Key

> The integrationKey and password values have been redacted. In an actual request, substitute your own key and the user's password

```shell
curl -X POST -d "integrationKey=XXX" -d "email=fishbowl@wufoo.com" -d "password=XXX" -d "subdomain=fishbowl" -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://wufoo.com/api/v3/login.json"
```

```python
import urllib
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

values = {
        'integrationKey' : 'XXX', 
        'email' : 'fishbowl@wufoo.com',
        'password' : 'XXX',
        'subdomain': 'fishbowl'
}

data = urllib.urlencode(values)

response = urllib2.urlopen(base_url+'login.json', data)
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

uri = URI.parse(base_url+"forms/s1afea8b1vk0jf7/entries.json")

request = Net::HTTP::Post.new(uri.request_uri)
request.basic_auth(username, password)

request.set_form_data('integrationKey' => 'XXX',
                      'email' => 'fishbowl@wufoo.com',
                      'password' => 'XXX',
                      'subdomain' => 'fishbowl'
                      )

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

```php
<?php
$curl = curl_init('https://wufoo.com/api/v3/login.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

curl_setopt($curl, CURLOPT_POST, 1);
curl_setopt($curl, CURLOPT_POSTFIELDS, 'integrationKey=XXX&mail=fishbowl@wufoo.com&password=XXX&subdomain=fishbowl');

$response = curl_exec($curl);
$resultStatus = curl_getinfo($curl);

if($resultStatus['http_code'] == 200 || $resultStatus['http_code'] == 201) {
    $json = json_decode($response);
    echo json_encode($json, JSON_PRETTY_PRINT);
} else {
    echo 'Call Failed '.print_r($resultStatus);
}
?>
```

> The above request will recieve a response in this format:

```json
{
  "ApiKey":"AOI6-LFKL-VM1Q-IEX9",
  "UserLink":"https://fishbowl.wufoo.com/api/v3/users/b1fe5l920lqsh58.json",
  "Subdomain":"fishbowl"
}
```
This request allows [approved partners](https://master.wufoo.com/forms/integration-key-application/) to access users API Keys. This is useful for custom integrations that need to make API requests on behalf of Wufoo users. For example, [Zapier](https://zapier.com/zapbook/wufoo/) uses this method to set up new integrations, without requiring users to use or even know their own API Key.

### HTTP Request

`POST http://wufoo.com/api/v3/login.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
format    | Either 'json' or 'xml' is required. This will determine response format

### POST Parameters

Parameter      | Description
-------------- | -----------
integrationKey | Required. This is your Login integration key. You can apply for one [here](https://master.wufoo.com/forms/integration-key-application/)
email          | Required. The user’s email, which acts as the identifier for their account.
password       | Required. The user's password
subdomain      | Optional. The user's subdomain. Is required if the email belongs to a sub-user or the email address is used on multiple accounts.
<aside class="warning">If you submit a request without the subdomain, but there's a conflict, the request will return a 409 error</aside>

A successful response will contain:

ApiKey - This is the user's API Key. You can then use this to make API requests on their behalf.

UserLink - This is a link for the corresponding Users request for this specific user.

Subdomain - The subdomain for the user. You’ll need this to make proper API requests to the user's account.

### Sub-users and Multiple subdomains

If the user you're trying to access is either:
- A subuser of the account
- An Account Creator and/or sub-user on multiple accounts
the subdomain parameter is required. 

If you leave out the subdomain, but one of the above criteria applies, you'll receive a 409 error. To avoid this, we recommend making all requests with the relevant subdomain parameter, even if it's not technically "required."
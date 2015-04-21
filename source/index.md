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
  - forms
  - entries
  - reports
  - users
  - webhooks
  - login
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

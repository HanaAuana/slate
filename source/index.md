---
title: Wufoo API

language_tabs:
  - shell: cURL
  - php: PHP
  - python: Python
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

Welcome to the Wufoo API! You can use our API to access your forms, entries, reports, and more. You can also submit new entries, and even add or remove Webhooks. 

Our v3 API is RESTful, which means you can make requests using any HTTP service. To help you get started with building your own integrations, there are some basic code examples in the area to the right, and you can switch the programming language of the examples with the tabs in the top right. All examples use the 'fishbowl' example subdomain. When making your own requests, be sure to use your own account name/subdomain, and your own API Key.

## Structure

Each resource page will go into more detail, but here's a quick overview of how the Wufoo API is structured

When making a request, you'll use your specific account subdomain. For example: `https://fishbowl.wufoo.com`

All of our API resources then start with: `/api/v3` 

To help keep things organized, we've broken up our API into logical sections based on the different aspects of Wufoo. These are:  

Name     | Endpoint    | HTTP Methods
-------- | ----------- | -----------
Forms    | `/forms`    | GET
Entries  | `/entries`  | GET or POST
Reports  | `/reports`  | GET
Users    | `/users`    | GET
Webhooks | `/webhooks` | PUT or DELETE
Login    | `/login`    | POST

Some requests require you to identify the specific resource you're trying to access. The most commonly used example would be a form identifier. To uniquely identify a specific form, you can use either 
the "hashed" URL: `/forms/s1afea8b1vk0jf7/`
or the form title: `/forms/wufoo-api-example/`

Forms and Reports resources have a  "hashed" and a "title" identifier. Widgets, Users, and WebHooks resources only have hash identifiers.

Finally, each request will end with a format extension. Our API can return responses in either `.json` or `.xml` format.

A complete request will look like this: `https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7.json`

## Restrictions

We currently restrict API usage to 5000 requests per key, per day. This means that each sub-user on an account can make 5000 requests.

## API Key

To use any of the API functions, you'll need to use your Wufoo API Key. If you haven't already, you can follow these steps to locate your key:

- Log in to your Wufoo account
- Click the Share button beneath any of your forms 
- In the Share menu, click the API Information button to access your API credentials. 
- On that page there is a 16 digit code, which is your unique API key.

<aside class="notice">
Each sub-user on your account has their own API Key. This allows you to still enforce <a href='http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/User-Management'>User Permissions</a>, even with the API
</aside>


> Here is a sample request, showing the process for authenticating using your API Key:

# Authentication

```shell
# With cURL, you can just pass the "username" and "password" with each request
curl -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms.json"
```

```php
<? php
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
    echo htmlentities($response);
} else {
    echo 'Call Failed '.print_r($resultStatus);
}
?>
```

```python
# Using urllib2 we'll need an HTTPPasswordMgr and HTTPBasicAuthHandler
import urllib2

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

# Create a password manager
password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()

# Add the username and password (API key and nonsense value)
password_manager.add_password(None, base_url, username, password)

# Create the AuthHandler
handler = urllib2.HTTPBasicAuthHandler(password_manager)

# Create and install an opener using the AuthHandler
opener = urllib2.build_opener(handler)
urllib2.install_opener(opener)

# Now each request we make will be authenticated
response = urllib2.urlopen(base_url+'forms.json')
```

```ruby
require "net/http"
require "uri"
require "json"

base_url = 'https://fishbowl.wufoo.com/api/v3/'
username = 'AOI6-LFKL-VM1Q-IEX9'
password = 'footastic'

uri = URI.parse(base_url+"forms.json")

# Set up our request using the desired endpoint, and configure the basic auth
request = Net::HTTP::Get.new(uri.request_uri)
request.basic_auth(username, password)

# Make our request using https
response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

# Print the output in a "pretty" json format
puts JSON.pretty_generate(JSON[response.body])
```

> Make sure to replace `AOI6-LFKL-VM1Q-IEX9` with your API key and `fishbowl` with your own subdomain. The second value `footastic` is required, but can be anything

Wufoo uses [Basic Auth](http://www.ietf.org/rfc/rfc2617.txt) with API Keys to allow access to the API. 

Wufoo expects the API key to be included as the 'username' and any value as the 'password' portion of Basic Auth. If the service you're using doesn't have a built in way to authenticate using Basic Auth, you can set the Authorization header to a base64 encoded string:

`base64('username:password')`

After encoding, you can set the header like this:

`Authorization: Basic QU9JNi1MRktMLVZNMVEtSUVYOTpmb290YXN0aWM=`

<aside class="notice">
You'll need to replace 'username' with your API key, and password with any value (our examples use 'footastic')
</aside>

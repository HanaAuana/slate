# Webhooks

## Add Webhook

```shell
curl -X PUT -d "url=https://www.wufoo.com" -d "handshakeKey=secret123" -d "metadata=true" -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/webhooks.json"
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
    'url' : 'https://www.wufoo.com', 
    'handshakeKey' : 'secret123',
    'metadata' : 'true'
}

put_data = urllib.urlencode(values)

request = urllib2.Request(url=base_url+'forms/s1afea8b1vk0jf7/webhooks.json', data=put_data)
request.get_method = lambda: 'PUT'

response = urllib2.urlopen(request)
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

uri = URI.parse(base_url+"forms/s1afea8b1vk0jf7/webhooks.json")

request = Net::HTTP::Put.new(uri.request_uri)
request.basic_auth(username, password)

request.set_form_data('url' => 'https://wufoo.com',
                      'handshakeKey' => 'secret123',
                      'metadata' => 'true'
                      )

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

> The above request will recieve a response in this format:

```json
{
  "WebHookPutResult": {
    "Hash": "h1elg2i41wauer1"
  }
}
```

### HTTP Request

`PUT http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/webhooks.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
subdomain | Your account subdomain/username.
format    | Either 'json' or 'xml' is required. This will determine response format
identifier| The title or hash of the form to retrieve

### PUT Parameters

Parameter    | Default | Description
------------ | ------- | -----------
url          | N/A     | Required. This represents the URL that the Webhook will POST to when an entry is submitted. URL must be valid.
handshakeKey | None    | Optional. Sets the handshakeKey property, to allow you to reject random POSTs
metadata     | false   | Optional. If set to true, the Webhook will include form/field structure data in each POST (required for some integrations)

## Delete Webhook

```shell
curl -X DELETE -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/webhooks/h1elg2i41wauer1.json"
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

request = urllib2.Request(url=base_url+'forms/s1afea8b1vk0jf7/webhooks/hap0e1c1x5rapc.json')
request.get_method = lambda: 'DELETE'

response = urllib2.urlopen(request)
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

uri = URI.parse(base_url+"forms/s1afea8b1vk0jf7/webhooks/hw271p50lanp7l.json")

request = Net::HTTP::Delete.new(uri.request_uri)
request.basic_auth(username, password)

response = Net::HTTP.start(uri.hostname, uri.port, :use_ssl => uri.scheme == 'https') {|http|
  http.request(request)
}

puts JSON.pretty_generate(JSON[response.body])
```

> The above request produces output in this format:

```json
{
  "WebHookDeleteResult":{
    "Hash":"h1elg2i41wauer1"
  }
}
```

### HTTP Request

`DELETE http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/webhooks/{webhookHash}.{format}`

### URL Parameters

Parameter   | Description
----------- | -----------
subdomain   | Your account subdomain/username.
format      | Either 'json' or 'xml' is required. This will determine response format
identifier  | The title or hash of the form to retrieve
webhookHash | The hash for the webhook you want to delete (Is returned in the initial PUT request response)
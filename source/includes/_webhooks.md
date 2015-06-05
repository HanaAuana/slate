# Webhooks

The Webhooks API allows you to add/delete Webhooks on your form, without requiring any manual setup. For example, Zapier uses this to [set up a "Zap"](https://zapier.com/help/wufoo/#using-the-quotnew-entry-webhookquot-trigger) in your forms, without you needing to make any changes.

Reducing the number of steps your user takes to connect your integration to Wufoo can help to increase conversion and decreases user frustration.

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

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/webhooks.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

curl_setopt($curl, CURLOPT_POST, 1);
curl_setopt($curl, CURLOPT_POSTFIELDS, 'url=https://www.wufoo.com&handshakeKey=secret123&metadata=true');
curl_setopt($curl, CURLOPT_CUSTOMREQUEST, 'PUT');

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
  "WebHookPutResult": {
    "Hash": "h1elg2i41wauer1"
  }
}
```

This request updates the Webhooks for a specific form. We only allow one Webhook per URL, so if there's a request made for an existing URL, it will simply update, rather than duplicate the Webhook.

### HTTP Request

`PUT http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/webhooks.{format}`

A PUT request is [idempotent](http://stackoverflow.com/questions/46585/when-do-you-use-post-and-when-do-you-use-get/46639#46639), which means that you may safely make this call multiple times with the same data. This prevents you from accidentally adding 10 of the same Webhook URLs to one form. For example: 
- You make one PUT call to the Webhook API with the `url`, `metadata`, and `handshakeKey` parameters
- Your user decides they want to use a new handshake key. 
- You make a second API call with the same `url`, but a new `handshakeKey`, and the API will update the handshake key of the Webhook with that URL to the new `handshakeKey` parameter.

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
handshakeKey | N/A     | Optional. Sets the [handshakeKey property](http://help.wufoo.com/articles/en_US/SurveyMonkeyArticleType/Webhooks#getstarted). This can be used to help the receipient of the Webhooks ignore unwanted POSTs 
metadata     | false   | Optional. If set to true, the Webhook will include form/field structure data in each POST (required for some integrations)

The Webhook PUT request will return a WebHookPutResult object, with a `Hash` property: the newly created/updated Webhook's "hash." This is an unchanging value representing the Webhook on your form. It's a good idea to save this value, because it acts as the Webhook identifier for a Webhook DELETE request, and you can’t retrieve it without making another request.

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

```php
<?php
$curl = curl_init('https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/webhooks/hjnuh251sepi2x.json');
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($curl, CURLOPT_USERPWD, 'AOI6-LFKL-VM1Q-IEX9:footastic');
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_ANY);
curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);                          
curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);                           
curl_setopt($curl, CURLOPT_USERAGENT, 'Wufoo Sample Code');

curl_setopt($curl, CURLOPT_CUSTOMREQUEST, 'DELETE');

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

> The above request produces output in this format:

```json
{
  "WebHookDeleteResult":{
    "Hash":"h1elg2i41wauer1"
  }
}
```

This request allows you to remove a specific Webhook from a specific form.

### HTTP Request

`DELETE http://{subdomain}.wufoo.com/api/v3/forms/{identifier}/webhooks/{webhookHash}.{format}`

### URL Parameters

Parameter   | Description
----------- | -----------
subdomain   | Your account subdomain/username.
format      | Either 'json' or 'xml' is required. This will determine response format
identifier  | The title or hash of the form to retrieve
webhookHash | The hash for the webhook you want to delete (Is returned in the initial PUT request response)

The webhookHash identifier is the value that was returned from the Webhook PUT request that created the Webhook. If you don't have this recorded, you'll need to manually delete the Webhook, or make another PUT request with the same values. Upon a successful deletion, the WebHookDeleteResult object will be returned, with the same `Hash` property as a PUT request.
# Webhooks

## Add Webhook

```shell
curl -X PUT -d "url=https://www.wufoo.com" -d "handshakeKey=secret123" -d "metadata=true" -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://fishbowl.wufoo.com/api/v3/forms/s1afea8b1vk0jf7/webhooks.json"
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
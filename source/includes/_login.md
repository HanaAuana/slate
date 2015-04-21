# Login

## Retrieve API Key

> integrationKey and password values have been redacted. In an actual request, substitute your own key and the user's password

```shell
curl -X POST -d "integrationKey=XXX" -d "email=fishbowl@wufoo.com" -d "password=XXX" -d "subdomain=fishbowl" -u "AOI6-LFKL-VM1Q-IEX9":"footastic" "https://wufoo.com/api/v3/login.json"
```
> The above request will recieve a response in this format:

```json
{
  "ApiKey":"AOI6-LFKL-VM1Q-IEX9",
  "UserLink":"https://fishbowl.wufoo.com/api/v3/users/b1fe5l920lqsh58.json",
  "Subdomain":"fishbowl"
}
```

### HTTP Request

`POST http://wufoo.com/api/v3/login.{format}`

### URL Parameters

Parameter | Description
--------- | -----------
format    | Either 'json' or 'xml' is required. This will determine response format

### POST Parameters

Parameter      | Description
-------------- | -----------
integrationKey | Required. This is your Login integration key. You can apply [here](https://master.wufoo.com/forms/integration-key-application/)
email          | Required. The user’s email, which acts as the identifier for their account.
password       | Required. The user's password
subdomain      | Optional. The user's subdomain. Is required if the email belongs to a sub-user or the email address is used on multiple accounts.
<aside class="warning">If you submit a request without the subdomain, but there's a conflict, the request will return a 409 error</aside>
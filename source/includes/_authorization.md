
# Authorization

The Payments API relies on [SKY API's implementation of OAuth2](https://developer.blackbaud.com/skyapi/docs/authorization/auth-code-flow) for authorizing requests. 

See the SKY API authorization code flow [code samples](https://developer.blackbaud.com/skyapi/docs/authorization/auth-code-flow/code-samples) for complete examples of how to implement this, but the following captures key steps.


## Request access

> Request access

```csharp
var yourApplicationId = "";
var yourApplicationCallbackUri = "";
using (var client = new HttpClient())
{
    var skyApiTokenUrl = $"https://oauth2.sky.blackbaud.com/authorization?" 
      + $"client_id={yourApplicationId}&response_type=code"
      + &redirect_uri={yourApplicationCallbackUri}";

    return await client.GetAsync(skyApiTokenUrl);
}
```

<aside class="notice">Don't forget to provide the values specific to your application and account on each step!</aside>

The first step is getting approval from a user at the organization for your application to access their data.

## Retrieve tokens

> Exchange auth code for tokens

```csharp
var code = ""; // This is the authorization code from the previous step
var yourApplicationCallbackUri = "";
var yourApplicationId = "";
var yourApplicationSecret = "";

using (var client = new HttpClient())
{
    var skyApiTokenUrl = $"https://oauth2.sky.blackbaud.com/token";

    var requestBody = new Dictionary<string, string>()
    {
        { "grant_type", "authorization_code" },
        { "code", code },
        { "redirect_uri", yourApplicationCallbackUri }
    };

    var password = Utility.EncodeBase64($"{yourApplicationId}:{yourApplicationSecret}");
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", password);

    client.DefaultRequestHeaders.Accept.Add(
      new MediaTypeWithQualityHeaderValue(
        "application/x-www-form-urlencoded"));

    var response = await client.PostAsync(skyApiTokenUrl, new FormUrlEncodedContent(requestBody));

    if (response.IsSuccessStatusCode)
    {
        var tokens = JsonConvert.DeserializeObject<Dictionary<string, string>>(
          await response.Content.ReadAsStringAsync());
        
        // You can use this to issue authorized requests.
        var accessToken = tokens["access_token"];

        // You can use this in the next step.
        var refreshToken = tokens["refresh_token"];
    }
}
```

The second step is exchanging the authorization code for the access and refresh token.

## Refresh tokens

> Refresh tokens

```csharp
var refreshToken = ""; // This is the refresh token from the previous step
var yourApplicationCallbackUri = "";
var yourApplicationId = "";
var yourApplicationSecret = "";
using (var client = new HttpClient())
{
    var skyApiTokenUrl = $"https://oauth2.sky.blackbaud.com/token";

    var requestBody = new Dictionary<string, string>()
    {
        { "grant_type", "refresh_token" },
        { "refresh_token", RefreshToken }
    };

    var password = Utility.EncodeBase64($"{yourApplicationId}:{yourApplicationSecret}");
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", password);

    client.DefaultRequestHeaders.Accept.Add(
      new MediaTypeWithQualityHeaderValue(
        "application/x-www-form-urlencoded"));

    var response = await client.PostAsync(skyApiTokenUrl, new FormUrlEncodedContent(requestBody));

    if (response.IsSuccessStatusCode)
    {
        var tokens = JsonConvert.DeserializeObject<Dictionary<string, string>>(
          await response.Content.ReadAsStringAsync());

        // You can use this to issue authorized requests.
        var accessToken = tokens["access_token"];

        // Rinse and repeat.
        var refreshToken = tokens["refresh_token"];
    }
}
```

The third step is once your access token expires, to exchange your refresh token for a new pair of access and refresh token.

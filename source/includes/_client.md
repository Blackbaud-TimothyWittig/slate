# Payments API Client

> Add your access token and subscription key as headers to the http client

```csharp
var yourAccessToken = "";
var yourSubscriptionKey = "";
using (var httpClient = new HttpClient())
{
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", yourAccessToken);
    httpClient.DefaultRequestHeaders.Add("Bb-Api-Subscription-Key", yourSubscriptionKey);

    var paymentsApiClient = new Blackbaud.PaymentsApi.Client(httpClient);
}
```

> The client library let's you manage the lifecycle of the the `HttpClient` that it uses.

<aside class="warning">TODO: provide links to client repos.</aside>

Once you have your access token and subscription key on hand, you can create an instance of the Payments API Client.


# Payment configurations
## GET single

`https://api.sky.blackbaud.com/payments/v1/paymentconfigurations/{payment_configuration_id}`

```csharp
var yourAccessToken = "";
var yourPaymentConfigurationId = "";
using (var client = new HttpClient())
{
    var url = $"https://api.sky.blackbaud.com/payments/v1/paymentconfigurations/{yourPaymentConfigurationId}";

    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", yourAccessToken);
    client.DefaultRequestHeaders.Add("Bb-Api-Subscription-Key", Configuration.SubscriptionKey);

    return await client.GetAsync(url);
}
```

### Description:

Returns information about a payment configuration.

### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| payment_configuration_id | path | The identifier for the payment configuration. | Yes | string (uuid) |

### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returned when the operation is successful. The response body contains payment configuration details. | [PaymentConfigurationRead](#paymentconfigurationread) |
| 400 | Returned when the request body is not in the appropriate format. | [ [ServiceError](#serviceerror) ] |
| 404 | Returned when the specified payment configuration is not found. | [ [ServiceError](#serviceerror) ] |

## GET all

`https://api.sky.blackbaud.com/payments/v1/paymentconfigurations`

```csharp
var yourAccessToken = "";
using (var client = new HttpClient())
{
    var url = "https://api.sky.blackbaud.com/payments/v1/paymentconfigurations";

    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", yourAccessToken);
    client.DefaultRequestHeaders.Add("Bb-Api-Subscription-Key", Configuration.SubscriptionKey);

    return await client.GetAsync(url);
}
```

### Summary:

Payment configuration list

### Description:

Returns a set of payment configurations.

### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| include_inactive | query | True to include payment configurations whose status is inactive. | No | boolean |

### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returned when the operation is successful. The response body contains a set of payment configurations. | [PaymentConfigurationListRead](#paymentconfigurationlistread) |
| 400 | Returned when the request body is not in the appropriate format. | [ [ServiceError](#serviceerror) ] |


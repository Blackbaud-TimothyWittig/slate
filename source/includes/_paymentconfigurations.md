
# Payment configurations

## GET List

`https://api.sky.blackbaud.com/payments/v1/paymentconfigurations`

```csharp
var paymentConfigurations = await paymentsApiClient.ListPaymentConfigurationAsync();
foreach (var paymentConfiguration in paymentConfigurations.Value)
{
    if (paymentConfiguration.Name == "some name")
    {
        // Do something.
    } 
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


## GET

`https://api.sky.blackbaud.com/payments/v1/paymentconfigurations/{payment_configuration_id}`

```csharp
var paymentConfiguration = await paymentsApiClient.GetPaymentConfigurationAsync("<payment configuration id>");
if (paymentConfiguration.Process_mode == "Test")
{
    // Do something.
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

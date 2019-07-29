# Transactions

## GET

`https://api.sky.blackbaud.com/payments/v1/transactions/{transaction_id}`

```csharp
var yourAccessToken = "";
var yourTransactionId = "";
using (var client = new HttpClient())
{
    var url = $"https://api.sky.blackbaud.com/payments/v1/transactions/{yourTransactionId}";

    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", yourAccessToken);
    client.DefaultRequestHeaders.Add("Bb-Api-Subscription-Key", Configuration.SubscriptionKey);

    return await client.GetAsync(url);
}
```

### Description:

Returns information about a transaction.

### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| transaction_id | path | The identifier of the transaction for which you would like to retrieve additional information. | Yes | string (uuid) |

### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returned when the operation is successful. The response body contains transaction details. | [TransactionRead](#transactionread) |
| 400 | Returned when the request body is not in the appropriate format. | [ [ServiceError](#serviceerror) ] |
| 404 | Returned when the specified transaction was not found. | [ [ServiceError](#serviceerror) ] |

## POST

`https://api.sky.blackbaud.com/payments/v1/transactions`

### Description:

Create a transaction.

### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| transactionAdd | body | An object that represents the transaction to process. | Yes | [TransactionAdd](#transactionadd) |

### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returned when the operation is successful. The response body contains transaction details. | [TransactionRead](#transactionread) |
| 400 | Returned when the request body is not in the appropriate format. | [ [ServiceError](#serviceerror) ] |


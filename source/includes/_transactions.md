# Transactions

## GET


```csharp
var transactionId = "<a valid transaction id>";
var transaction = await paymentsApiClient.GetTransactionAsync(transactionId);
if (transaction.State == Blackbaud.PaymentsApi.TransactionReadState.Pending)
{
    // Do something.
}
```

`https://api.sky.blackbaud.com/payments/v1/transactions/{transaction_id}`

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

```csharp
var transactionAdd = new Blackbaud.PaymentsApi.TransactionAdd {
    Amount = 1000,
    Billing_contact = new Blackbaud.PaymentsApi.BillingInfoAdd
    {
        Address = "2000 Daniel Island Drive",
        City = "Charleston",
        Country = "US",
        First_name = "Blackbaud",
        Post_code = "29442",
        State = "SC"
    },
    Credit_card = new Blackbaud.PaymentsApi.CreditCardAdd
    {
        Exp_month = 2,
        Exp_year = 1985,
        Name = "Donna Donor",
        Number = "4111111111111111"
    },
    Csc = "123",
    Comment = "Recurring donation",
    Donor_ip = "192.168.0.1",
    Payment_configuration_id = new Guid("<a valid payment configuration id>")
};
var transaction = await paymentsApiClient.CreateTransactionAsync(transactionAdd);
if (transaction.State == Blackbaud.PaymentsApi.TransactionReadState.Processed)
{
    // Do something.
}
```

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


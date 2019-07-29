
# Models

## CardRead

Represents a stored credit card.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| bank_identification_number | string | The first six of the account number for the stored credit card. | No |
| brand | string | The brand name of the stored credit card. | No |
| last_four | string | The last four of the account number for the stored credit card. | No |
| expiry_year | integer | The expiration year for the stored credit card. | No |
| expiry_month | integer | The expiration month for the stored credit card. | No |
| cardholder_name | string | The name of the account holder for the stored credit card. | No |

## ServiceError

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| message | string |  | No |
| error_name | string |  | No |
| error_code | integer |  | No |
| raw_message | string |  | No |
| error_args | [ string ] |  | No |

## PublicKeyRead

Defines the data model for the Public Key endpoint response.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| public_key | string (uuid) | Gets the public key | No |

## CheckoutTransactionAdd

Defines the data model for post checkout transaction request.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | integer | The amount to charge, used to validate that the authorized amount is the same as the amount being charged.  Measured in cents: 1000 = $10.00. | Yes |
| authorization_token | string (uuid) | The authorization token of the transaction to charge. | Yes |

## TransactionRead

Represents a created transaction.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| token | string (uuid) | The stored token. Available only on creation of Transaction record. | No |
| id | string (uuid) | The unique identifier of this transaction. | No |
| amount | integer | The gross amount of this transaction. Measured in cents: 1000 = $10.00. | No |
| transaction_type | string | The transaction type of this transaction.  Possible values are CardNotPresent, CardPresent, TransactionBatch, OfflineBatch, Refund, RefundBatch, ChargeBack, ReverseChargeback, or FraudManagement. | No |
| credit_card | [CreditCardRead](#creditcardread) | The information of the credit card for this transaction. | No |
| additional_fee | integer | The additional fee amount for this transaction.  Measured in cents: 1000 = $10.00. | No |
| currency | string | The 3 char ISO4217 currency code used for this transaction. | No |
| application | string | The calling Application of this transaction. | No |
| comment | string | The comment on this transaction. | No |
| transaction_date | string | The date and time of this transaction. | No |
| donor_ip_address | string | The IP address where this transaction originated. | No |
| email_address | string | The account holder’s email address. | No |
| phone_number | string | The account holder’s phone number. | No |
| is_live | boolean | True if this is not a test or demo transaction. | No |
| disbursement_status | string | The disbursement status of this transaction.  Possible values are Disbursable, DoNotDisburse, and Disbursed. | No |
| terminal_type | string | Used for card present transactions to indicate the type of terminal used.  Possible values are Unknown, AutomatedDispensingMachine, SelfServiceTerminal, LimitedAmountTerminal, MobilePayDevice, or ChipAndPIN | No |
| routing_number | string | The Routing Number for the transaction. | No |
| pending_date | string | The date by which decision could be made for the transaction. It will be approved or declined. | No |
| check_number | string | The Check Number for the transaction to be processed. | No |
| account_type | string | The type of account of this transaction. Used for Direct Debit transactions.  Possible values are Checking, Savings, Corporate checkings, or Corporate savings. | No |
| billing_info | [BillingInfoRead](#billinginforead) | The billing info for this transaction. | No |
| fraud_result | [FraudResultRead](#fraudresultread) | The fraud result information for this transaction. | No |
| state | string | The current processing state of the transaction. | No |

## CreditCardRead

Defines the data model for credit card read.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| card_type | string | The IIN value of the card. | No |
| exp_month | integer | The expiration month for the card. | No |
| exp_year | integer | The expiration year for the card. | No |
| last_four | string | The last 4 digits of primary account number for this card. | No |
| name | string | The name of the card holder. | No |

## BillingInfoRead

Defines the data model for billing information.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| city | string | The account holder’s billing city. | No |
| country | string | The account holder’s billing country - ISO standard. | No |
| post_code | string | The account holder’s billing postal code. | No |
| state | string | The account holder’s billing state - ISO standard. | No |
| street | string | The account holder’s billing address. | No |

## FraudResultRead

Defines the data model for fraud result information.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| anonymous_proxy_result | string | Used for clients who have opted in to Premium Fraud Service, this is the result of the anonymous proxy validation.  The possible values are NotProcessed, Pass, or Failed. | No |
| bin_and_ip_country_result | string | Used for clients who have opted in to Premium Fraud Service, this is the result of the bin origination country compared to the origination country of the ip.  The possible values are NotProcessed, Pass, or Failed. | No |
| high_risk_country_result | string | Used for clients who have opted in to Premium Fraud Service, this is the result of the high risk country validation.  The possible values are NotProcessed, Pass, or Failed. | No |
| result_code | string | Used for clients who have opted in to Premium Fraud Service, this is the result of the overall result of the premium fraud validation.  The possible values are NotProcessed, Passed, FailedProcessingError, FailedProfileSettings, MissingRequiredLicensekey, MissingRequiredField, or NonRoutableIP | No |
| risk_score | integer | Used for clients who have opted in to Premium Fraud Service, this is the score that was determined for this transaction. | No |
| risk_threshold | integer | Used for clients who have opted in to Premium Fraud Service, this is the threshold that was set by the client at the time of this transaction. | No |
| velocity_result | string | Used for clients who have opted in to Premium Fraud Service, this is the result of the velocity validation.  The possible values are NotProcessed, Pass, or Failed. | No |

## PaymentConfigurationRead

Defines a payment configuration.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| active | boolean | True if the payment configuration is active. | No |
| avs_level | string | The AVS level for this payment configuration.  Possible values are None, Full, Medium, or Light. | No |
| csc_level | string | The CSC level for this payment configuration.  Possible values are None, Full, or Light. | No |
| currency | string | The currency used for this payment configuration. | No |
| id | string (uuid) | The unique identifier for this payment configuration. | No |
| name | string | The name of the payment configuration. | No |
| process_mode | string | The processing mode for this payment configuration.  Possible values are Live, Test, or Demo. | No |
| supported_cards | [ string ] | The list of supported card type IINs | No |
| use3ds | boolean | True if the payment configuration is set to use 3DS processing. | No |

## PaymentConfigurationListRead

Defines a set of payment configurations.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| count | integer | Total count of PaymentConfigurationRead records | No |
| value | [ [PaymentConfigurationRead](#paymentconfigurationread) ] | An array of PaymentConfigurationRead records | No |

## RefundAdd

Defines the data model for the refund request.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | integer | The amount to be refund. If empty, will refund the entire amount of the transaction.  Measured in cents: 1000 = $10.00. | No |
| reference_transaction_id | string (uuid) | The unique identifier of the transaction to refund. | Yes |
| transaction_id | string (uuid) | Optional unique identifier for this transaction. If empty, will be auto-generated. | No |

## DirectDebitAccountTokenAdd

Defines the available values for adding a direct debit account token.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| direct_debit_account_info | [DirectDebitAccountInfo](#directdebitaccountinfo) | The direct debit account information to tokenize. | Yes |
| id | string | The token identifier. | No |

## DirectDebitAccountInfo

Defines a direct debit account to use for transaction processing.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| account_holder | string | The name of the account holder of the direct debit transaction. | No |
| account_number | string | The account used to make the transaction. | No |
| account_type | string | The account type. Possible values are Checking, Savings, Corporate checking, or Corporate savings. | No |
| check_number | string | The check number of the transaction. | No |
| routing_number | string | The routing number of the direct debit transaction. | No |

## DirectDebitAccountTokenRead

Defines the output values when adding a direct debit account token.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| direct_debit_account_token | string | The direct debit account token identifier. | No |

## CardTokenAdd

Defines the data model for the card token request.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| exp_month | integer | The expiration month for the card. | Yes |
| exp_year | integer | The expiration year for the card. | Yes |
| id | string | Gets or sets the ID. | No |
| issue_number | string | Optional issue number for the card. | No |
| name | string | The name of the card holder. | Yes |
| number | string | The primary account number for this card. | Yes |
| valid_from_month | integer | Optional issue month for the card. | No |
| valid_from_year | integer | Optional issue year for the card. | No |

## CardTokenRead

Defines the data model for the card token endpoint response.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| card_token | string | Gets the card token. | No |

## TransactionAdd

Represents options to create a transaction.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| tokenize | boolean | Optionally tokenize payment information if CreditCardAdd, CardPresentData, or DirectDebitAccountInfo parameters are available. | No |
| transaction_id | string (uuid) | Optional unique identifier for this transaction. If empty, will be auto-generated. | No |
| amount | integer | The monetary amount of the transaction. Measured in cents: 1000 = $10.00. | Yes |
| payment_configuration_id | string (uuid) | The unique identifier for the payment configuration to be used when processing this request.                Payment configurations can be retrieved using the <a href="https://developer.sky.blackbaud.com/docs/services/payments/operations/ListPaymentConfiguration">GET Payment Configuration list endpoint</a>. | Yes |
| donor_ip | string | The IPv4 address of the person whose credit card we are attempting to process. This parameter should be treated as required for all Web applications.  If not provided Premium Fraud Management Services will not be executed. | No |
| email | string | The email address of the donor. | No |
| phone | string | The phone number of the donor. | No |
| comment | string | A free form comment for this transaction. | No |
| card_token | string (uuid) | The <a href="https://en.wikipedia.org/wiki/Universally_unique_identifier">unique identifier</a> for the stored credit card whose PAN you wish to use for this transaction.                This parameter is optional, but either the CreditCard, CardToken, CardPresent, DirectDebitAccountInfo, or DirectDebitAccountToken parameter must be specified. | No |
| credit_card | [CreditCardAdd](#creditcardadd) | The credit card information to be used for this transaction.                This parameter is optional, but either the CreditCard, CardToken, CardPresent, DirectDebitAccountInfo, or DirectDebitAccountToken parameter must be specified. | No |
| card_present | [CardPresentData](#cardpresentdata) | Card Present information swipe data to be used for the transaction.                This parameter is optional, but either the CreditCard, CardToken, CardPresent, DirectDebitAccountInfo, or DirectDebitAccountToken parameter must be specified. | No |
| csc | string | The Card Security Code (CVV2) for the card whose PAN was specified in the CreditCard parameter.  This parameter should be omitted when using a payment configuration that does not perform CSC check. | No |
| billing_contact | [BillingInfoAdd](#billinginfoadd) | The billing information for this transaction. | No |
| direct_debit_account_info | [DirectDebitAccountInfo](#directdebitaccountinfo) | This parameter is optional, but either the CreditCard, CardToken, CardPresent, DirectDebitAccountInfo, or DirectDebitAccountToken parameter must be specified. | No |
| direct_debit_account_token | string (uuid) | The <a href="https://en.wikipedia.org/wiki/Universally_unique_identifier">unique identifier</a> for the stored debit account info that can be used for the transaction.                This parameter is optional, but either the CreditCard, CardToken, CardPresent, DirectDebitAccountInfo, or DirectDebitAccountToken parameter must be specified. | No |

## CreditCardAdd

Defines the data model for the credit card add.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| exp_month | integer | The expiration month for the card. | No |
| exp_year | integer | The expiration year for the card. | No |
| issue_number | string | Optional issue number for the card. | No |
| name | string | The name of the card holder. | No |
| number | string | The primary account number for this card. | No |
| valid_from_month | integer | Optional issue month for the card. | No |
| valid_from_year | integer | Optional issue year for the card. | No |

## CardPresentData

Defines the data model for the card Present request.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| swipe_data | string | Swipe data information obtained from card reader. The content should adhere to <a href="https://en.wikipedia.org/wiki/ISO/IEC_7813">the ISO/IEC 7813 standard</a>. | No |

## BillingInfoAdd

Defines the data model for billing information request.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| address | string | The account holder’s billing address. | No |
| city | string | The account holder’s billing city. | No |
| country | string | The account holder’s billing country - ISO standard. | No |
| first_name | string | The given name of the account holder for the card whose PAN you wish to use for this transaction. | No |
| last_name | string | The surname of the account holder for the card whose PAN you wish to use for this transaction. | No |
| post_code | string | The account holder’s billing postal code. | No |
| state | string | The account holder’s billing state - ISO standard. | No |
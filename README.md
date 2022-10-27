# Cashfree-SDK

[![Downloads](https://pepy.tech/badge/cashfree-sdk/month)](https://pepy.tech/project/cashfree-sdk)

Cashfree SDK's are released in Beta. This is work in progress and we are continuously working on improving various aspects of it. It is released as learning aid and example kit for the API integrators. This is not recommended by Cashfree for direct use in production code. Please report any bugs to Cashfree at techsupport@cashfree.com.
# cashfree-sdk-python

The official Cashfree SDK for Python3,

Get started quickly using Cashfree with the Cashfree SDK for python. The SDK helps take the complexity out of coding by providing Python objects for Cashfree services including Payouts, Payment Gateway, Marketplace and Autocollect. The single, downloadable package includes the Cashfree Python Library and documentation.

Please refer to the [Cashfree Docs](https://docs.cashfree.com/docs/)  for the complete API reference.

## Installing
### In Django or Flask Application for Python 3.5+

The preferred way to install the Cashfree SDK for Python is to use the [pip](https://pypi.org/project/pip/) package manager for pip. Simply type the following into a terminal window:
```sh
pip3 install cashfree-sdk
```

## Getting Started
### Pre-requisites
  - A [Cashfree Merchant Account](https://merchant.cashfree.com/merchant/sign-up)
  - API keys for different products. You can generate them from your Dashboard
### IP Whitelisting and dynamic IPs
Your IP has to be whitelisted to hit Cashfree's server. Or if you have a dynamic IP please pass in the public key parameter during the init method as shown below. For more information please go [here](https://dev.cashfree.com/development/quickstart#ip-whitelisting).
## Usage
### Payouts
The package needs to be configured with your account's secret key which is available in your Cashfree Dashboard.
Init the package with your credentials and add the below code in your config.py of your package.
##### In case of static IP (Your IP is whitelisted)
```python

from cashfree_sdk.payouts import Payouts

//Initialize Cashfree Payout
Payouts.init("<client_id>", "<client_secret>", "PROD")
```
##### In case of dynamic IP you will need a public key to generate a signature(which will be done by sdk itself)

```python

from cashfree_sdk.payouts import Payouts

//Initialize Cashfree Payout
Payouts.init("<client_id>", "<client_secret>", "PROD", public_key_path='/User/Cashfree/file_path.pem')
// OR
Payouts.init("<client_id>", "<client_secret>", "PROD", public_key= b'public key')
```


| Option              | Default                       | Description                                                                           |
| ------------------- | ----------------------------- | ------------------------------------------------------------------------------------- |
| `env`        | `TEST`                        | Environment to be initialized. Can be set to `TEST` or `PROD` |
| `client_id` | ``                             | `client_id` which can be generated on cashfree dashboard.                  |
| `client_secret`         | ``                        | `client_secret` which can be found alongside generated `client_id`. |
| `public_key_path`         | ``                        | `public_key_path` specify the path to your .pem public key file `. |
| `public_key`         | ``                        | `public_key` Pass your Public Key to this parameter as an alternative to `public_key_path` . |                     

#### [Payout Library Docs](cashfree_sdk/payouts/README.md)

### WebHook Verification

To verify the webhook received from Cashfree for different events and accept the webhook only when it returns `True`.

#### Usage
Pass the webhook received along with the payload type.

| Option              | Options                       |
| ------------------- | ----------------------------- |
| `payload_type`        | `JSON` for `application/json` , `FORM` for `application/x-www-form-urlencoded`                      |


```python
from cashfree_sdk import verification
webhook_data = '{"cashgramId": "5b8283182e0711eaa4c531df6a4f439b-28", "event": "CASHGRAM_EXPIRED", "eventTime": "2020-01-03 15:01:06", "reason": "OTP_ATTEMPTS_EXCEEDED", "signature": "TBpM+4nr1DsWsov7QiHSTfRJP4Z9BD8XrDgEhBlf9ss="}'
verification.verify_webhook(webhook_data, 'JSON')
```

### Using Python requests
Every method returns a python request object which can be used:
```python
from cashfree_sdk.payouts.beneficiary import Beneficiary
bene_add = Beneficiary.add("kit_test6", "ankur", "ankur@cashfree.com", "9999999999", "aakjakjakja")
```
```diff
- All Optional Arguments Should Be Passed As An Keyword (Named) Arguments
```
[Readme](cashfree_sdk/exceptions) for the exception thrown for invalid operation and how to handle the exceptions.

- For more information about the APIs go to [Payouts](https://github.com/cashfree/cashfree-sdk-python/tree/master/cashfree_sdk/payouts).
- Complete list of [APIs](https://docs.cashfree.com/docs/payout/guide/#fetch-beneficiary-id).
### TODO
- [ ] PG
- [ ] Market Place
- [ ] Autocollect

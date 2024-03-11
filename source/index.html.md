---
title: ScriptDrop Delivery API

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - elixir

includes:
  - errors
  - changelog

search: true

code_clipboard: true

---

# Introduction

Welcome to the ScriptDrop Delivery API.

# Authentication
Authentication is performed using an API key and secret and sent using the
`Authorization` header with the `Basic` realm.

> To authorize, use this code:

```elixir
api_key = "pk_myapikey1234"
api_secret = "tesk_myapisecret1234"

encoded_authorization = Base.url_encode64("#{api_key}:#{api_secret}")

authorization_header = "Basic #{encoded_authorization}"
```

ScriptDrop uses API keys to allow access to the API. Please contact our support
team for API keys.

ScriptDrop expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Basic encoded_authorization`

<aside class="notice">
You must replace <code>encoded_authorization</code> with your encoded API key
and secret.
</aside>

# V1 Orders

## Create an Order

```elixir
url = "https://delivery.scriptdrop.co/api/v1/orders"

headers = [
  {"Authorization", "Basic encoded_authorization"},
  {"Content-type", "application/json"}
]

sameday_order_params = %{
  "delivery_fee" => 5.00,
  "rx_amount_due" => 2.00,
  "other_items_amount_due" => 3.50,
  "delivery_notes" => "Deliver at front desk",
  "external_reference_number" => "238947",
  "pharmacy" => %{
    "npi" => "1234567890",
    "ncpdp" => "1234567"
  },
  "recipient" => %{
    "description" => "JOHN WAYNE DOE",
    "mobile_phone_number" => "1115550000",
    "home_phone_number" => "2225550000",
    "is_patient" => true,
    "address" => %{
      "street" => "1230 Street",
      "street2" => "Unit 1",
      "city" => "Columbus",
      "state" => "OH",
      "zipcode" => "43210"
    }
  },
  "patient" => %{
    "first_name" => "JOHN",
    "last_name" => "DOE",
    "gender" => "male",
    "date_of_birth" => "2000-02-01",
    "mobile_phone_number" => "3335550000",
    "home_phone_number" => "4445550000"
  },
  "prescriptions" => [
    %{
      "number" => "897234",
      "ndc" => "69618001436",
      "refrigeration" => "none",
      "days_supply" => 30,
      "fill_quantity" => 30.0,
      "fill_number" => 1,
      "patient_pay" => 50.0,
      "date_of_service" => "2019-02-03",
      "prescriber" => %{
        "first_name" => "Prescriber First",
        "last_name" => "Prescriber Last",
        "npi" => "1234567890",
        "address" => %{
          "street" => "1231 Street",
          "city" => "Columbus",
          "state" => "OH",
          "zipcode" => "43210"
        }
      },
      "payers" => [
        %{
          "bin" => "1112",
          "pcn" => "2222",
          "rx_group" => "123456",
          "coverage_type" => "primary",
          "government_plan_indicator" => false
        },
        %{
          "bin" => "1113",
          "pcn" => "2223",
          "rx_group" => "123456",
          "coverage_type" => "secondary",
          "government_plan_indicator" => true
        }
      ]
    }
  ],
  "other_items" => [
    %{
      "sku" => "2318901234234",
      "upc" => "1203492394823",
      "description" => "Snickers 6oz",
      "quantity" => 2
    }
  ]
}

HTTPoison.start()
HTTPoison.post(url, Json.encode!(sameday_order_params), headers)

ondemand_order_params = %{
  "service_level" => "ondemand",
  "ready_at" => "2019-01-02T13:00:00-05:00",
  "delivery_fee" => 5.00,
  "rx_amount_due" => 2.00,
  "other_items_amount_due" => 3.50,
  "delivery_notes" => "Deliver at front desk",
  "pharmacy" => %{
    "npi" => "1234567890",
    "ncpdp" => "1234567"
  },
  "recipient" => %{
    "description" => "JOHN WAYNE DOE",
    "mobile_phone_number" => "1115550000",
    "home_phone_number" => "2225550000",
    "is_patient" => true,
    "address" => %{
      "street" => "1230 Street",
      "street2" => "Unit 1",
      "city" => "Columbus",
      "state" => "OH",
      "zipcode" => "43210"
    }
  },
  "patient" => %{
    "first_name" => "JOHN",
    "last_name" => "DOE",
    "gender" => "male",
    "date_of_birth" => "2000-02-01",
    "mobile_phone_number" => "3335550000",
    "home_phone_number" => "4445550000"
  },
  "prescriptions" => [
    %{
      "number" => "897234",
      "ndc" => "69618001436",
      "refrigeration" => "none",
      "days_supply" => 30,
      "fill_quantity" => 30.0,
      "fill_number" => 1,
      "patient_pay" => 50.0,
      "date_of_service" => "2019-02-03",
      "prescriber" => %{
        "first_name" => "Prescriber First",
        "last_name" => "Prescriber Last",
        "npi" => "1234567890",
        "address" => %{
          "street" => "1231 Street",
          "city" => "Columbus",
          "state" => "OH",
          "zipcode" => "43210"
        }
      },
      "payers" => [
        %{
          "bin" => "1112",
          "pcn" => "2222",
          "rx_group" => "123456",
          "coverage_type" => "primary",
          "government_plan_indicator" => false
        },
        %{
          "bin" => "1113",
          "pcn" => "2223",
          "rx_group" => "123456",
          "coverage_type" => "secondary",
          "government_plan_indicator" => true
        }
      ]
    }
  ],
  "other_items" => [
    %{
      "sku" => "2318901234234",
      "upc" => "1203492394823",
      "description" => "Snickers 6oz",
      "quantity" => 2
    }
  ]
}

HTTPoison.start()
HTTPoison.post(url, Json.encode!(ondemand_order_params), headers)

shipping_order_params = %{
  "service_level" => "shipping",
  "service_date" => "2022-12-10",
  "delivery_fee" => 0.00,
  "rx_amount_due" => 0.00,
  "other_items_amount_due" => 0.00,
  "delivery_notes" => nil,
  "shipping" => %{
    "carrier" => "USPS",
    "carrier_service" => "USPS Priority Mail",
    "signature" => "none",
    "weight" => %{
      "unit" => "pound",
      "value" => 1.0
    },
    "package_code" => "usps_small_flat_rate_box",
    "dimensions" => %{
      "_comment" =>  "The dimensions key is not required if a package_code is sent
        but is being shown in this example as a demonstration of the structure",
      "unit" => "inch",
      "length" => 2.0,
      "width" => 1.0,
      "height" => 3.0
    }
  },
  "pharmacy" => %{
    "npi" => "1234567890",
    "ncpdp" => "1234567"
  },
  "recipient" => %{
    "description" => "JOHN WAYNE DOE",
    "mobile_phone_number" => "1115550000",
    "home_phone_number" => "2225550000",
    "is_patient" => true,
    "address" => %{
      "street" => "1230 Street",
      "street2" => "Unit 1",
      "city" => "Columbus",
      "state" => "OH",
      "zipcode" => "43210"
    }
  },
  "patient" => %{
    "first_name" => "JOHN",
    "last_name" => "DOE",
    "gender" => "male",
    "date_of_birth" => "2000-02-01",
    "mobile_phone_number" => "3335550000",
    "home_phone_number" => "4445550000"
  },
  "prescriptions" => [
    %{
      "number" => "897234",
      "ndc" => "69618001436",
      "refrigeration" => "none",
      "days_supply" => 30,
      "fill_quantity" => 30.0,
      "fill_number" => 1,
      "patient_pay" => 50.0,
      "date_of_service" => "2019-02-03",
      "prescriber" => %{
        "first_name" => "Prescriber First",
        "last_name" => "Prescriber Last",
        "npi" => "1234567890",
        "address" => %{
          "street" => "1231 Street",
          "city" => "Columbus",
          "state" => "OH",
          "zipcode" => "43210"
        }
      },
      "payers" => [
        %{
          "bin" => "1112",
          "pcn" => "2222",
          "rx_group" => "123456",
          "coverage_type" => "primary",
          "government_plan_indicator" => false
        },
        %{
          "bin" => "1113",
          "pcn" => "2223",
          "rx_group" => "123456",
          "coverage_type" => "secondary",
          "government_plan_indicator" => true
        }
      ]
    }
  ],
  "other_items" => [
    %{
      "sku" => "2318901234234",
      "upc" => "1203492394823",
      "description" => "Snickers 6oz",
      "quantity" => 2
    }
  ]
}

HTTPoison.start()
HTTPoison.post(url, Json.encode!(shipping_order_params), headers)
```

> The above command returns JSON structured like this:

```json
{
  "order": {
    "id": "1234",
    "status": "new",
    "pickup": null,
    "delivery": null,
    "return": null,
    "cancellation": null,
    "eta": null
  }
}
```

This endpoint creates an order.

### HTTP Request

`POST https://delivery.scriptdrop.co/api/v1/orders`

### Body Parameters

| Name                      | Type                                       | Required                           | Length   | Description                                                                                                                   |
| ------------------------- | ------------------------------------------ | ---------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| initiator                 | String                                     | false                              |          | Indicates the source of the request. Must be one of: pharmacy.                                                              |
| delivery_fee              | Decimal                                    | Only for sameday                   |          | Delivery fee to be collected.                                                                                          |
| rx_amount_due             | Decimal                                    | Only for sameday                   |          | Copay to be collected for the order.                                                                                          |
| other_items_amount_due    | Decimal                                    | false. Only supported for sameday. |          | Fees related to other items to be collected.                                                                              |
| delivery_notes            | String                                     | false                              | max: 280 | Instructions visible to courier during delivery to assist with the delivery.                                                |
| external_reference_number | String                                     | false                              | max: 255 | Reference number used to identify the order from an external system.                                                          |
| photo_id_required         | Boolean                                    | false. Only supported for sameday. |          | Indicates whether a photo ID is required for delivery.                                                                        |
| pharmacy                  | [Pharmacy](#pharmacy-parameters)           | true                               |          | Pharmacy details.                                                                                                             |
| recipient                 | [Recipient](#recipient-parameters)         | true                               |          | Recipient details.                                                                                                            |
| patient                   | [Patient](#patient-parameters)             | true                               |          | Patient details.                                                                                                              |
| shipping                  | [Shipping](#shipping-parameters)           | Only for shipping                  |          | Additional information required for shipping.                                                                                 |
| prescriptions             | [Prescription[]](#prescription-parameters) | true                               |          | Prescriptions to be delivered.                                                                                                |
| other_items               | [OtherItem[]](#other-item-parameters)      | false                              |          | Other items to be delivered, typically OTC items.                                                                             |

### Pharmacy Parameters

| Name  | Type   | Required | Length | Description              |
| ----- | ------ | -------- | ------ | ------------------------ |
| npi   | String | true     | is: 10 | Pharmacy NPI for order   |
| ncpdp | String | true     | is: 7  | Pharmacy NCPDP for order |

### Recipient Parameters

| Name                | Type                           | Required | Length  | Description                                                                                                                  |
| ------------------- | ------------------------------ | -------- | ------- | ---------------------------------------------------------------------------------------------------------------------------- |
| description         | String                         | true     | max: 71 | Describes the recipient. In cases where the patient is the recipient, this should be the first and last name of the patient. |
| mobile_phone_number | String                         | false    | is: 10  | Mobile phone number for the order recipient.                                                                                 |
| home_phone_number   | String                         | false    | is: 10  | Home phone number for the order recipient                                                                                    |
| address             | [Address](#address-parameters) | true     |         | Recipient's location (i.e. dropoff location).                                                                                |

### Address Parameters

| Name    | Type   | Required | Length         | Description                   |
| ------- | ------ | -------- | -------------- | ----------------------------- |
| street  | String | true     | max: 255       | Street                        |
| street2 | String | false    | max: 255       | Street Line 2 (ex. Unit 1)    |
| city    | String | true     | max: 255       | City                          |
| state   | String | true     | max: 2         | Two-letter state abbreviation |
| zipcode | String | true     | is: 5 or is: 9 | Zipcode                       |

### Patient Parameters

| Name                | Type                 | Required     | Length  | Description                                                                             |
| ------------------- | -------------------- | ------------ | ------- | --------------------------------------------------------------------------------------- |
| first_name          | String               | true         | max: 30 | Patient's first name.                                                                   |
| last_name           | String               | true         | max: 40 | Patient's. last name                                                                    |
| gender              | String               | true         |         | Patient's gender. Can be one of: `male`, `female`, `unspecified`.                       |
| date_of_birth       | ISO 8601 date string | true         |         | Patient's date of birth.                                                                |
| mobile_phone_number | String               | for shipping | is: 10  | Patient's mobile phone number. Required for shipping if home_phone_number not provided. |
| home_phone_number   | String               | for shipping | is: 10  | Patient's home phone number. Required for shipping if mobile_phone_number not provided. |

### Prescription Parameters

| Name            | Type                                 | Required | Length   | Description                                                                                               |
| --------------- | ------------------------------------ | -------- | -------- | --------------------------------------------------------------------------------------------------------- |
| number          | String                               | true     | max: 255 | Rx number.                                                                                                |
| ndc             | String                               | true     | is: 11   | National Drug Code.                                                                                       |
| refrigeration   | String                               | true     |          | Indicates whether the prescription needs to be refrigerated. Can be one of `none`, `fridge`, or `frozen`. |
| days_supply     | Integer                              | true     |          | Days supply.                                                                                              |
| fill_quantity   | Decimal                              | true     |          | Fill quantity.                                                                                            |
| fill_number     | Integer                              | true     |          | Fill number.                                                                                              |
| patient_pay     | Decimal                              | true     |          | Patient responsibility.                                                                                   |
| prescriber      | [Prescriber](#prescriber-parameters) | true     |          | Prescriber information.                                                                                   |
| date_of_service | String                               | false    |          | Date of service for the prescription.                                                                     |
| payers          | [Payer[]](#payer-parameters)         | true     |          | Payer information.                                                                                        |

### Other Item Parameters

| Name        | Type    | Required | Length | Description                               |
| ----------- | ------- | -------- | ------ | ----------------------------------------- |
| upc         | String  | true     |        | UPC                                       |
| sku         | String  | true     |        | SKU                                       |
| quantity    | Integer | true     |        | Quantity being delivered                  |
| description | String  | true     |        | Short description of item being delivered |

### Prescriber Parameters

| Name       | Type                           | Required | Length | Description             |
| ---------- | ------------------------------ | -------- | ------ | ----------------------- |
| first_name | String                         | true     |        | Prescriber's first name |
| last_name  | String                         | true     |        | Prescriber's last name  |
| npi        | String                         | true     |        | Prescriber's NPI        |
| address    | [Address](#address-parameters) | true     |        | Prescriber's address    |

### Payer Parameters

| Name                      | Type    | Required | Length   | Description                                                         |
| ------------------------- | ------- | -------- | -------- | ------------------------------------------------------------------- |
| bin                       | String  | true     | max: 255 | BIN                                                                 |
| pcn                       | String  | true     | max: 255 | PCN                                                                 |
| rx_group                  | String  | true     |          | Rx group                                                            |
| coverage_type             | String  | true     |          | Coverage type. Can be one of `primary`, `secondary`, or `tertiary`. |
| government_plan_indicator | Boolean | true     |          | Indicates whether or not payer is a government plan.                |

### Shipping Parameters

| Name              | Type    | Required | Length | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------------- | ------- | -------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| carrier           | String  | true     |        | Ground carrier to be used. Can be one of `USPS`, `UPS`, or `FedEx`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| carrier_service   | String  | true     |        | Shipping service used. Can be one of `UPS Ground`, `UPS 2nd Day Air`, `UPS Next Day Air`, `FedEx 2 Day`, `FedEx Standard Overnight`, `FedEx Priority Overnight`, `FedEx Ground`, `FedEx Home Delivery`, `USPS Priority Mail`, `USPS Priority Mail Express`, and `USPS First Class Mail`.                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| signature         | String  | true     |        | Value indicating which signature method should be used. Can be one of `none`, `required`, `adult_required`, or `patient_signature`. All carriers support `none`. Other supported signature types by carrier:<br/>USPS<br/><small>&nbsp;&bull; POD signature (anyone can sign) = `required`<br/>&nbsp;&bull; Adult (over 21) = `adult_required`<br/>&nbsp;&bull; Patient (over 21) = `patient_signature`</small><br/>UPS<br/><small>&nbsp;&bull; Signature (anyone can sign) = `required`<br/>&nbsp;&bull; Adult (over 21) = `adult_required`<br/></small>FedEx<br/><small>&nbsp;&bull; Indirect (anyone can sign) = `required`<br/>&nbsp;&bull; Direct (Patient) = `patient_signature`<br/>&nbsp;&bull; Adult (over 21) = `adult_required`</small> |
| saturday_delivery | Boolean | false    |        | Value indicating whether Saturday should be included in possible days for delivery. This option is ONLY available for `UPS 2nd Day Air` and `UPS Next Day Air`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| weight.unit       | String  | true     |        | Unit of measure for weight. Can be one of `ounce` or `pound`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| weight.value      | Decimal | true     |        | Package weight. Must be under 1 pound for USPS First Class Mail.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| package_code      | String  | false    |        | Code representing carrier specific package sizes. For USPS can be one of: `usps_small_flat_rate_box`, `usps_medium_flat_rate_box`, `usps_large_flat_rate_box`. For FedEx can be one of: `fedex_envelope_onerate`, `fedex_small_box_onerate`, `fedex_medium_box_onerate`, `fedex_large_box_onerate`, `fedex_extra_large_box_onerate`. If a package_code is selected, all dimension data will be overwritten by the selected default package dimensions.                                                                                                                                                                                                                                                                                             |
| dimensions        | Object  | false    |        | Required if package_code is not set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| dimensions.unit   | String  | false    |        | Unit of measure for dimensions. Must be `inch`. Required if package_code is not set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| dimensions.length | Decimal | false    |        | Length of package. Required if package_code is not set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| dimensions.width  | Decimal | false    |        | Width of package. Required if package_code is not set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| dimensions.height | Decimal | false    |        | Height of package. Required if package_code is not set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### 200 Response Schema

See the [200 Response Schema under Get an Order](#200-response-schema-2).

### Error Response

> JSON example of a 400 response payload when shipping order is not eligible for Saturday delivery:

```json
{
  "error": {
    "message": "Carrier service level does not offer saturday delivery."
  }
}
```

## Cancel an Order

```elixir
url = "https://delivery.scriptdrop.co/api/v1/orders/1234"

headers = [
  {"Authorization", "Basic encoded_authorization"},
]

HTTPoison.start()
HTTPoison.delete(url, headers)
```

> On success the above command returns no response body

This endpoint cancels a specific order only if the order is new or submitted to courier.

### HTTP Request

`DELETE https://delivery.scriptdrop.co/api/v1/orders/:id`

### URL Parameters

| Parameter | Description                   |
| --------- | ----------------------------- |
| :id       | The ID of the order to delete |

### Success Response

HTTP status code 204

### Error Response

> JSON example of a 400 response payload when the order is in any status but new or submitted to courier:

```json
{
  "error": {
    "message": "Order is not in a cancellable status"
  }
}
```

See also [Errors](#errors)

## Get an Order

```elixir
url = "https://delivery.scriptdrop.co/api/v1/orders/1234"

headers = [
  {"Authorization", "Basic encoded_authorization"},
  {"Content-type", "application/json"}
]

HTTPoison.start()
HTTPoison.get(url, headers)
```

> JSON returned when a sameday or ondemand order is new:

```json
{
  "order": {
    "id": "1234",
    "external_reference_number": null,
    "status": "new",
    "pickup": null,
    "delivery": null,
    "return": null,
    "shipping": null,
    "cancellation": null
    "eta": null
  }
}
```

> JSON returned when a shipping order is new:

```json
{
  "order": {
    "id": "1234",
    "external_reference_number": null,
    "status": "new",
    "pickup": null,
    "delivery": null,
    "return": null,
    "cancellation": null,
    "eta": null,
    "shipping": {
      "tracking_number": "128397192837",
      "tracking_url": "https://tools.usps.com/go/TrackConfirmAction?tLabels=128397192837",
      "carrier": "USPS",
      "carrier_service": "USPS Priority Mail",
      "label_pdf": "https://example.com/123123/13123123?param=value",
      "saturday_delivery": false,
      "cost": 2.95
    }
  }
}
```

> JSON returned when a sameday or ondemand order is submitted to courier:

```json
{
  "order": {
    "id": "1234",
    "external_reference_number": null,
    "status": "submitted to courier",
    "pickup": null,
    "delivery": null,
    "return": null,
    "shipping": null,
    "eta": {
      "arrival_at": "2023-10-11T15:40:40.765721Z",
      "type": "pickup"
    },
    "cancellation": null
  }
}
```

> JSON returned when a sameday or ondemand order is picked up:

```json
{
  "order": {
    "id": "1234",
    "external_reference_number": null,
    "status": "picked_up",
    "pickup": {
      "_comment": "Pickup information is not available for shipping orders",
      "occurred_at": "2019-01-01T01:00:00Z"
    },
    "delivery": null,
    "return": null,
    "shipping": null,
    "cancellation": null,
    "eta": {
      "arrival_at": "2023-10-11T15:40:40.765721Z",
      "type": "delivery"
    }
  }
}
```

> JSON returned when a sameday or ondemand order is cancelled:

```json
{
  "order": {
    "id": "1234",
    "external_reference_number": null,
    "status": "cancelled",
    "pickup": null,
    "delivery": null,
    "return": null,
    "shipping": null,
    "cancellation": {
            "occurred_at": "2023-10-17T10:15:08.773523Z",
            "reason": "Courier Company Reassignment"
        }
    "eta": null
  }
}
```

> JSON returned when a sameday or ondemand order is successfully delivered:

```json
{
  "order": {
    "id": "1234",
    "external_reference_number": null,
    "status": "delivered",
    "pickup": {
      "occurred_at": "2019-01-01T01:00:00Z"
    },
    "delivery": {
      "_comment": "Delivery information is not available for shipping orders",
      "occurred_at": "2019-01-01T02:00:00Z",
      "signature_url": "https://example.com/238947",
      "signed_by": "John Doe",
      "relationship": "Other",
      "other_relationship_description": "Sibling",
      "recipient_identification": null,
      "failure_reason": null
    },
    "return": null,
    "shipping": null,
    "cancellation": null,
    "eta": {
      "arrival_at": "2023-10-11T15:19:23.085272Z",
      "type": "delivery"
    }
  }
}
```

> JSON returned when a sameday or ondemand order is successfully delivered and identification was collected from recipient:

```json
{
  "order": {
    "id": "1234",
    "external_reference_number": null,
    "status": "delivered",
    "pickup": {
      "occurred_at": "2019-01-01T01:00:00Z"
    },
    "delivery": {
      "occurred_at": "2019-01-01T02:00:00Z",
      "signature_url": "https://example.com/238947",
      "signed_by": "John Doe",
      "relationship": "Other",
      "other_relationship_description": "Sibling",
      "recipient_identification": {
        "number": "TT123456789",
        "jurisdiction_code": "OH",
        "qualifier": "06",
        "type": "Driver License ID"
      },
      "failure_reason": null
    },
    "return": null,
    "shipping": null,
    "cancellation": null,
    "eta": {
      "arrival_at": "2023-10-11T15:19:23.085272Z",
      "type": "delivery"
    }
  }
}
```

> JSON returned when a sameday or ondemand order is unsuccessfully delivered and being returned to the
> pharmacy:

```json
{
  "order": {
    "id": "1234",
    "status": "delivery_attempted",
    "pickup": {
      "occurred_at": "2019-01-01T01:00:00Z"
    },
    "delivery": {
      "occurred_at": "2019-01-01T02:00:00Z",
      "signature_url": null,
      "signed_by": null,
      "relationship": null,
      "other_relationship_description": null,
      "recipient_identification": null,
      "failure_reason": "Patient Not Home"
    },
    "return": null,
    "shipping": null,
    "cancellation": null,
    "eta": {
      "arrival_at": "2023-10-11T15:19:23.085272Z",
      "type": "delivery"
    }
  }
}
```

> JSON returned when a sameday or ondemand order is returned to the pharmacy:

```json
{
  "order": {
    "id": "1234",
    "status": "returned_to_pharmacy",
    "pickup": {
      "occurred_at": "2019-06-06T15:57:03.672507Z"
    },
    "delivery": {
      "failure_reason": "Patient Not Home",
      "occurred_at": "2019-06-06T15:58:11.246000Z",
      "other_relationship_description": null,
      "signature_url": null,
      "recipient_identification": null,
      "signed_by": null
    },
    "return": {
      "occurred_at": "2019-06-06T15:59:11.246000Z"
    },
    "shipping": null,
    "cancellation": null,
    "eta": {
      "arrival_at": "2023-10-11T15:19:23.085272Z",
      "type": "delivery"
    }
  }
}
```

> JSON returned when a shipping order is successfully delivered:

```json
{
  "order": {
    "delivery": null,
    "external_reference_number": null,
    "id": "455",
    "pickup": null,
    "return": null,
    "shipping": {
      "carrier": "USPS",
      "carrier_service": "USPS Priority Mail",
      "cost": 7.49,
      "delivery": {
        "occurred_at": "2022-02-16T20:44:56.913400Z"
      },
      "saturday_delivery": false,
      "label_pdf": "/images/example_shipping_label.png",
      "tracking_number": "9205590258667011612249",
      "tracking_url": "https://tools.usps.com/go/TrackConfirmAction?tLabels=9205590258667011612249"
    },
    "status": "delivered",
    "cancellation": null,
    "eta": null
  }
}
```

This endpoint retrieves a specific order.

### HTTP Request

`GET https://delivery.scriptdrop.co/api/v1/orders/:id`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| :id       | The ID of the order to retrieve |

### 200 Response Schema

| Name                            | Type                  | Description                                      |
| ------------------------------- | --------------------- | ------------------------------------------------ |
| order.id                        | String                | ID of the order                                  |
| order.status                    | String                | Current status of the order                      |
| order.external_reference_number | String                | External reference number for the order          |
| order.pickup                    | [Pickup](#pickup)     | Details about when the orders was picked up      |
| order.delivery                  | [Delivery](#delivery) | Details about when the order was delivered       |
| order.return                    | [Return](#return)     | Details about the order's return to the pharmacy |
| order.shipping                  | [Shipping](#shipping) | Shipping details for the order                   |
| order.cancellation              | [Cancellation](#cancellation) | Details about an order's cancellation    |
| order.eta                       | [ETA](#eta)           | ETA details for the order                        |

### Pickup

Note: This section is not returned for shipping orders. The status field should be referenced for the current status of the order.

| Name        | Type               | Description                               |
| ----------- | ------------------ | ----------------------------------------- |
| occurred_at | ISO 8601 timestamp | Timestamp indicating when pickup occurred |

### Delivery

Note: This section is not returned for shipping orders. The status field should be referenced for the current status of the order.

| Name                           | Type                                                 | Description                                                                                                                                                                                            |
| ------------------------------ | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| occurred_at                    | ISO 8601 timestamp                                   | Timestamp indicating when delivery occurred.                                                                                                                                                           |
| signature_url                  | String                                               | URL that can be used to download the signature image. The URL is only authenticated for a brief period of time. A new URL will be provided on each request. Only present when delivery was successful. |
| signed_by                      | String                                               | Name of recipient who signed for the delivery. Only present when the delivery was successful.                                                                                                          |
| relationship                   | String                                               | Description of the relationship between the patient and recipient. Only present when the delivery was successful for sameday orders.                                                                   |
| other_relationship_description | String                                               | Description of the relationship between the patient and recipient. Only present when `order.delivery.relationship` is `Other` for sameday orders.                                                      |
| failure_reason                 | String                                               | Reason why the delivery failed. Only present when the delivery was unsuccessful.                                                                                                                       |
| recipient_identification       | [RecipientIdentification](#recipient-identification) | Information regarding identification of the recipient at the point of delivery.                                                                                                                        |

### Recipient Identification

| Name              | Type   | Description                                                                                                                                                                              |
| ----------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| number            | String | Identifier captured. Example: driver license number.                                                                                                                                     |
| type              | String | Human readable description of the type of identification collected at point of delivery.                                                                                                 |
| qualifier         | String | Qualifier corresponding to type. See the [Recipient Identification Qualifiers table](#recipient-identification-qualifiers) below for the mapping.                                        |
| jurisdiction_code | String | Code representing the jurisdiction which issued the form of identification collected. Only used if identification type is a driver license or state issued ID. Example: "OH" for "Ohio". |

### Shipping

| Name              | Type                                   | Description                                                         |
| ----------------- | -------------------------------------- | ------------------------------------------------------------------- |
| tracking_number   | String                                 | Carrier tracking number                                             |
| tracking_url      | String                                 | Carrier tracking url                                                |
| carrier           | String                                 | Carrier used for the shipping service. Example: USPS                |
| carrier_service   | String                                 | Carrier service used. Example: USPS Priority Mail                   |
| label_pdf         | String                                 | URL to PDF of the label to be placed on the package                 |
| cost              | Decimal                                | Cost of shipping for the order                                      |
| saturday_delivery | Boolean                                | Whether Saturday delivery was requested                             |
| delivery          | [ShippingDelivery](#shipping-delivery) | Shipping delivery details (null if shipment has not been delivered) |

### Shipping Delivery

| Name        | type               | Description                                 |
| ----------- | ------------------ | ------------------------------------------- |
| occurred_at | ISO 8601 timestamp | Timestamp indicating when delivery occurred |

### Recipient Identification Qualifiers

| Value | Description                          |
| ----- | ------------------------------------ |
| 01    | Military ID                          |
| 02    | State Issued ID                      |
| 03    | Unique System ID                     |
| 04    | Permanent Resident Card (Green Card) |
| 05    | Passport ID                          |
| 06    | Driver’s License ID                  |
| 07    | Social Security Number               |
| 08    | Tribal ID                            |

### Return

| Name        | type               | Description                               |
| ----------- | ------------------ | ----------------------------------------- |
| occurred_at | ISO 8601 timestamp | Timestamp indicating when return occurred |

### Cancellation

| Name        | type               | Description                               |
| ----------- | ------------------ | ----------------------------------------- |
| occurred_at | ISO 8601 timestamp | Timestamp indicating when cancellation occurred |
| cancellation_reason | string | Short phrase describing reason for cancellation |

Possible Cancellation Reasons (Can Change)

| Value |
| ----------- |
| Patient no longer wants |
| Patient came to pickup |
| Medication not ready for delivery |
| No Coverage at this time |
| Copay Unpaid |
| Courier Company Reassignment |
| Pharmacy Closed |
| Pharmacy Closed for Lunch |
| Pharmacy too busy |
| Pharmacy Unwilling to Participate |
| Pharmacy Willing to Participate |
| Out of Stock |
| Unwilling to give to driver |
| Driver unwilling to wait |
| Unknown Reason |
| Pickup Address Inaccessible |
| Pickup Address Incorrect |
| Cold Chain Violation |
| Pickup Contact Unavailable |
| Delivery Job Expired |
| Excessive Courier Delay |
| Courier Initiated Cancellation |
| Duplicate Job Cancellation |
| Delivery Already Completed |
| Delivery Contents Damaged |
| Delivery Contents Incorrect |
| Not Ready for Pickup |
| Order Canceled |
| Incomplete Order Contents |
| Order Not Found |
| Wait Time Exceeded at Pickup |
| Item Not As Described |
| Other |

### ETA

Note: Currently shipping orders don't provide an ETA. If no ETA available or yet available, field will be null.

| Name       | type               | Description                                        |
| ---------- | ------------------ | -------------------------------------------------- |
| arrival_at | ISO 8601 timestamp | Timestamp indicating estimated datetime of arrival. When delivered or returned, arrival given is last ETA from before delivery. |
| type       | String             | Type of ETA. Can be one of `pickup` or `delivery`. |

## Get Multiple Orders

```elixir
url = "https://delivery.scriptdrop.co/api/v1/orders"

headers = [
  {"Authorization", "Basic encoded_authorization"},
  {"Content-type", "application/json"}
]

HTTPoison.start()
HTTPoison.get(url, headers, params: ["ids[]": "1234", "ids[]": "1235"])
```

> Response Containing One New and One Delivered Order

```json
{
  "orders": [
    {
      "id": "1234",
      "external_reference_number": null,
      "status": "new",
      "pickup": null,
      "delivery": null,
      "return": null,
      "cancellation": null,
      "shipping": {
        "tracking_number": "128397192837",
        "tracking_url": "https://tools.usps.com/go/TrackConfirmAction?tLabels=128397192837",
        "carrier": "USPS",
        "carrier_service": "USPS Priority Mail",
        "label_pdf": "https://example.com/123123/13123123?param=value",
        "saturday_delivery": false,
        "cost": 2.95
      },
      "eta": null
    },
    {
      "id": "1235",
      "external_reference_number": null,
      "status": "delivered",
      "pickup": {
        "occurred_at": "2019-01-01T01:00:00Z"
      },
      "delivery": {
        "occurred_at": "2019-01-01T02:00:00Z",
        "signature_url": "https://example.com/238947",
        "signed_by": "John Doe",
        "relationship": "Other",
        "other_relationship_description": "Sibling",
        "recipient_identification": null,
        "failure_reason": null
      },
      "return": null,
      "shipping": null,
      "cancellation": null,
      "eta": {
        "arrival_at": "2023-10-11T15:19:23.085272Z",
        "type": "delivery"
      }
    }
  ]
}
```

This endpoint retrieves information for several orders at once.

### HTTP Request

`GET https://delivery.scriptdrop.co/api/v1/orders?ids=:order_ids`

### URL Parameters

| Parameter  | Description                                                                              |
| ---------- | ---------------------------------------------------------------------------------------- |
| :order_ids | An array of IDs for the orders you wish to retrieve, formatted as `ids[]=1&ids[]=2`, etc |

### 200 Response Schema

| Name    | Type    | Description                                                              |
| ------- | ------- | ------------------------------------------------------------------------ |
| objects | Order[] | Array of Order objects as described under [Get an Order](#get-an-order). |

## Add Prescription to Order

```elixir
url = "https://delivery.scriptdrop.co/api/v1/orders/:id/prescriptions"

headers = [
  {"Authorization", "Basic encoded_authorization"},
  {"Content-type", "application/json"}
]

params = %{
  "number" => "897234",
  "ndc" => "69618001436",
  "refrigeration" => "none",
  "days_supply" => 30,
  "fill_quantity" => 30.0,
  "fill_number" => 1,
  "patient_pay" => 50.0,
  "prescriber" => %{
    "first_name" => "Prescriber First",
    "last_name" => "Prescriber Last",
    "npi" => "1234567890",
    "address" => %{
      "street" => "1231 Street",
      "city" => "Columbus",
      "state" => "OH",
      "zipcode" => "43210"
    }
  },
  "payers" => [
    %{
      "bin" => "1112",
      "pcn" => "2222",
      "rx_group" => "123456",
      "coverage_type" => "primary",
      "government_plan_indicator" => false
    },
    %{
      "bin" => "1113",
      "pcn" => "2223",
      "rx_group" => "123456",
      "coverage_type" => "secondary",
      "government_plan_indicator" => true
    }
  ]
}

HTTPoison.start()
HTTPoison.post(url, Json.encode!(params), headers)
```

> The above command returns JSON structured like this:

```json
{
  "order": {
    "id": "1234",
    "status": "new",
    "pickup": null,
    "delivery": null,
    "return": null
  }
}
```

This endpoint adds a prescription to an already existing order.

### HTTP Request

`POST https://delivery.scriptdrop.co/api/v1/orders/:id/prescriptions`

### Body Parameters

| Name          | Type                                 | Required | Length   | Description                                                                                               |
| ------------- | ------------------------------------ | -------- | -------- | --------------------------------------------------------------------------------------------------------- |
| number        | String                               | true     | max: 255 | Rx number                                                                                                 |
| ndc           | String                               | true     | is: 11   | National Drug Code.                                                                                       |
| refrigeration | String                               | true     |          | Indicates whether the prescription needs to be refrigerated. Can be one of `none`, `fridge`, or `frozen`. |
| days_supply   | Integer                              | true     |          | Days supply                                                                                               |
| fill_quantity | Decimal                              | true     |          | Fill quantity                                                                                             |
| fill_number   | Integer                              | true     |          | Fill number                                                                                               |
| patient_pay   | Decimal                              | true     |          | Patient responsibility                                                                                    |
| prescriber    | [Prescriber](#prescriber-parameters) | true     |          | Prescriber's information                                                                                  |
| payers        | [Payer[]](#payer-parameters)         | true     |          | Payer information                                                                                         |

### 200 Response Schema

See the [200 Response Schema under Get an Order](#200-response-schema-2).

## Remove Prescription from Order

```elixir
url = "https://delvery.scriptdrop.co/api/v1/orders/:id/prescriptions/:rx_number"

headers = [
  {"Authorization", "Basic encoded_authorization"},
  {"Content-type", "application/json"}
]

HTTPoison.start()
HTTPoison.delete(url, headers)
```

> On success the above command returns no response body

This endpoint removes a specific prescription from an order.

### HTTP Request

`DELETE https://delivery.scriptdrop.co/api/v1/orders/:id/prescriptions/:rx_number`

### URL Parameters

| Parameter  | Description                                                      |
| ---------- | ---------------------------------------------------------------- |
| :id        | The ID of the order that the prescription should be removed from |
| :rx_number | The prescription number to delete                                |

### Success Response

HTTP status code 204

### Error Response

See [Errors](#errors)

# V1 Delivery Options

## Get Delivery Information

```elixir
url = "https://delvery.scriptdrop.co/api/v1/pharmacies/1234567"

headers = [
  {"Authorization", "Basic encoded_authorization"},
  {"Content-type", "application/json"}
]

HTTPoison.start()
HTTPoison.get(url, headers)
```
> The above command returns JSON structured like this:

```json
{
  "TBD"
}
```

### HTTP Request

`GET https://delivery.scriptdrop.co/api/v1/pharmacies/:id`

### Parameters

| Name                      | Type    | Required | Length   | Description                                                         |
| ------------------------- | ------- | -------- | -------- | ------------------------------------------------------------------- |
| :id                       | String  |          |          | The NPI or NCPDP of the pharmacy.                                   |
| :delivery.address         | Address | true     |          | Recipient's location (i.e. dropoff location)                        |
| :POD                      |         |          |          | "Null = Defualts to pharmacy configuration POD signature (anyone can sign)"|
| :package                  |         |          |          | Coverage type. Can be one of `primary`, `secondary`, or `tertiary`. |
| :saturday.delivery        | Boolean | false    |          | Value indicating whether Saturday should be in included in the possible days for delivery. This option is ONLY available for UPS 2nd Day Air and UPS Next Day Air                |

### 200 Response Schema

TBD

### Error Response

See [Errors](#errors)

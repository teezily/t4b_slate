# Orders

## Create an order

```shell
curl --location --request POST 'https://plus.teezily.com/api/v2/orders' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9' \
--header 'Content-Type: application/json' \
--data-raw '{
  "external_reference": "C9759",
  "email": "orval_jerde@ko.org",
  "address": {
    "first_name": "Shalon",
    "last_name": "Kihn",
    "company": "Schaefer, Daugherty and Tillman",
    "street1": "Leonardo Garden",
    "street2": "",
    "city": "North Kory",
    "postcode": "80802-1677",
    "state": "NY",
    "country_code": "US",
    "phone": "0102030406"
  },
  "line_items": [
    {
      "external_reference": "I7366",
      "variant_reference": "TSRN_U_IGREEN_L",
      "quantity": 2,
      "designs": [
        {
          "key": "front",
          "url": "http://example.org/front_preview.png"
        }
      ]
    }
  ]
}
'
```

```python
import http.client
import json

conn = http.client.HTTPSConnection("plus.teezily.com", undefined)
payload = json.dumps({
  "email": "orval_jerde@ko.org",
  "external_reference": "C9759",
  "address": {
    "first_name": "Shalon",
    "last_name": "Kihn",
    "company": "Schaefer, Daugherty and Tillman",
    "street1": "Leonardo Garden",
    "street2": "",
    "city": "North Kory",
    "postcode": "80802-1677",
    "state": "NY",
    "country_code": "US",
    "phone": "0102030406"
  },
  "line_items": [
    {
      "external_reference": "I7366",
      "variant_reference": "TSRN_U_IGREEN_L",
      "quantity": 2,
      "designs": [
        {
          "key": "front",
          "url": "http://example.org/front_preview.png"
        }
      ]
    }
  ]
})
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9',
  'Content-Type': 'application/json'
}
conn.request("POST", "/api/v2/orders", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```ruby
require "uri"
require "json"
require "net/http"

url = URI("https://plus.teezily.com/api/v2/orders")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Accept"] = "application/json"
request["Authorization"] = "Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "email": "orval_jerde@ko.org",
  "external_reference": "C9759",
  "address": {
    "first_name": "Shalon",
    "last_name": "Kihn",
    "company": "Schaefer, Daugherty and Tillman",
    "street1": "Leonardo Garden",
    "street2": "",
    "city": "North Kory",
    "postcode": "80802-1677",
    "state": "NY",
    "country_code": "US",
    "phone": "0102030406"
  },
  "line_items": [
    {
      "external_reference": "I7366",
      "variant_reference": "TSRN_U_IGREEN_L",
      "quantity": 2,
      "retail_price": "39.0",
      "designs": [
        {
          "key": "front",
          "url": "http://example.org/front_preview.png"
        }
      ]
    }
  ]
})

response = http.request(request)
puts response.read_body
```

> The above command returns JSON structured like this:

```json
{
  "id": 152,
  "external_reference": "C9759",
  "email": "orval_jerde@ko.org",
  "status": "pending",
  "address": {
    "first_name": "Shalon",
    "last_name": "Kihn",
    "company": "Schaefer, Daugherty and Tillman",
    "street1": "Leonardo Garden",
    "street2": "",
    "city": "North Kory",
    "postcode": "80802-1677",
    "state": "NY",
    "country_code": "US",
    "phone": "0102030406"
  },
  "line_items": [
    {
      "external_reference": "I7366",
      "variant_reference": "TSRN_U_IGREEN_L",
      "quantity": 2
    }
  ]
}
```

### HTTP Request

`POST https://plus.teezily.com/api/v2/orders`

### Order

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
external_reference | No| String | Your Order ID: O-xxx. Usefull to track orders. The API will raise an error if you have any other non-canceled orders with the same `external_reference`
email | Yes | String | Buyer's e-mail
status | No | String | Fulfillment internal status. do not submit this parameter for creation
address | **Yes** | Object | An [Address](./#address) Object. The API will attempt to verify the address before accepting order
line_items | **Yes** | Array | An array of [Line Item](./#line-item) Object

<!-- shipping_method | No | String | Can be `standard` or `tracking` -->
<!-- retail | No | Object | A [Retail](./#retail) object for invoicing -->

### HTTP Response
Returns an [Order](./#order) object

### Address

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
first_name | **Yes** | String |
last_name | **Yes** | String |
company | No | String |
phone | No | String |
street1 | **Yes** | String |
street2 | **Yes** | String | If not present put an empty string
city | **Yes** | String |
postcode | **Yes** | String | Some countries do not require postcodes, in that case put an empty string
state | No | String | Some countries do not require state codes, if it is the case the API will raise an error
country_code | **Yes** | String | Formatted as ISO 3166-1 two-letter
skip_verified_delivery | No | Boolean | Skip address delivery verification

### Line Item

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
external_reference | No| String | Your unique line item ID. Usefull to track line items. The API will raise an error if you have any other non-canceled line items with the same `external_reference`
variant_reference | **Yes** | String | The variant reference, see the [Product](./#product) endpoint
quantity | **Yes** | Integer
designs  | **Yes** | Array | An array of [Design](./#design) object
retail_price | No | String | Value of single item as purchased from the end customer. Used if VAT is provided so we can generate an invoice for you

### Design

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
key | **Yes** | String | Can be `front`, `back`, ... see our [Design specification](./#design-specification) `Side key` column
url | No | String | The url of the production design. Either `url` or `file` must be specified
file | No | File | If you wish to submit your payload in `multipart/form-data` and attach directly the file in it. Either `url` or `file` must be specified
position | No | String | Defaults to `auto` (more positional values coming soon)

<!-- position | No | String | Defaults to `auto`. Used to align the artwork within print area. Valid values are `top_left`, `top`, `top_right`, `center_left`, `center`, `center_right`, `bottom_left`, `bottom`, `bottom_right`, `manual`. Using `auto` will adjust your design the best way possible given the product, it is recommended you use this setting. -->
<!-- x | No | String | When using `manual`. Value ranges from `0` to `100`, origin is the center of the design -->
<!-- y | No | String | When using `manual`. Value ranges from `0` to `100`, origin is the center of the design -->
<!-- scale | No | String | When using `manual`. Value ranges from `0` to `100` -->

<!-- ### Retail -->

<!-- Retail costs that are to be displayed on the packing slip for international shipments. Retail costs are used only if every `line_item` in order contains the `retail_price` attribute. -->
<!--  -->
<!-- Parameter | Required | Type | Description -->
<!-- --------- | -------- | ---- | ----------- -->
<!-- vat_number | **Yes** | String | -->
<!-- vat_currency | **Yes** | String | An [ISO 4217](https://www.wikipedia.org/wiki/ISO_4217) string representing the currency associated with your VAT number if you specify it -->
<!-- currency | **Yes** | String | An [ISO 4217](https://www.wikipedia.org/wiki/ISO_4217) string representing the currency. Used if VAT is provided so we can generate an invoice for you -->
<!-- shipping | **Yes** | String | Shipping price -->
<!-- handling | **Yes** | String | Handling price -->
<!-- discount | **Yes** | String | Discount price -->
<!-- total | **Yes** | String | Total price -->
<!-- tax | **Yes** |  String | Tax price -->

<!-- <aside class="warning"> -->
<!-- `total_price` must equal `line_items.retail_price` + `shipping_price` + `discount_price` + `handling_price` -->
<!-- </aside> -->

## Get a single order

```shell
curl --location --request GET 'https://plus.teezily.com/api/v2/orders/152' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
```

```python
import http.client

conn = http.client.HTTPSConnection("plus.teezily.com", undefined)
payload = ''
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
}
conn.request("GET", "/api/v2/orders/152", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```ruby
require "uri"
require "net/http"

url = URI("https://plus.teezily.com/api/v2/orders/152")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Get.new(url)
request["Accept"] = "application/json"
request["Authorization"] = "Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9"

response = http.request(request)
puts response.read_body
```

> The above command returns JSON structured like this:

```json
{
  "id": 152,
  "external_reference": "C9759",
  "shipping_method": "tracking",
  "email": "orval_jerde@ko.org",
  "status": "pending",
  "address": {
    "first_name": "Shalon",
    "last_name": "Kihn",
    "company": "Schaefer, Daugherty and Tillman",
    "street1": "Leonardo Garden",
    "street2": "",
    "city": "North Kory",
    "postcode": "80802-1677",
    "state": "NY",
    "country_code": "US",
    "phone": "0102030406"
  },
  "line_items": [
    {
      "external_reference": "I7366",
      "variant_reference": "TSRN_U_IGREEN_L",
      "quantity": 2
    }
  ]
}
```

### HTTP Request

`GET https://plus.teezily.com/api/v2/orders/{id}`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | String | **Yes** | The order ID

`GET https://plus.teezily.com/api/v2/orders?external_reference={id}`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | String | **Yes** | The external order reference

### HTTP Response

Returns an [Order](./#order) object

## Get all orders

```shell
curl --location --request GET 'https://plus.teezily.com/api/v2/orders' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
```

```python
import http.client

conn = http.client.HTTPSConnection("plus.teezily.com", undefined)
payload = ''
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
}
conn.request("GET", "/api/v2/orders", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```ruby
require "uri"
require "net/http"

url = URI("https://plus.teezily.com/api/v2/orders")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Get.new(url)
request["Accept"] = "application/json"
request["Authorization"] = "Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9"

response = http.request(request)
puts response.read_body
```

> The above command returns JSON structured like this:

```json
{
  "results": [
    {
      "id": 152,
      "external_reference": "C9759",
      "shipping_method": "tracking",
      "email": "orval_jerde@ko.org",
      "status": "pending",
      "address": {
        "first_name": "Shalon",
        "last_name": "Kihn",
        "company": "Schaefer, Daugherty and Tillman",
        "street1": "Leonardo Garden",
        "street2": "",
        "city": "North Kory",
        "postcode": "80802-1677",
        "state": "NY",
        "country_code": "US",
        "phone": "0102030406"
      },
      "line_items": [
        {
          "external_reference": "I7366",
          "variant_reference": "TSRN_U_IGREEN_L",
          "quantity": 2
        }
      ]
    },
    {
      "id": 1,
      "external_reference": "C9346",
      "status": "pending",
      "shipping_method": "tracking",
      "email": "hobert@zemlakherzog.name",
      "address": {
        "first_name": "Nellie",
        "last_name": "Stoltenberg",
        "company": "Lueilwitz, Beier and Olson",
        "street1": "Elisha Wall",
        "street2": "",
        "city": "Kuhicfort",
        "postcode": "23988-4408",
        "state": "WI",
        "country_code": "US",
        "phone": "0102030406"
      },
      "line_items": [
        {
          "external_reference": "I4360",
          "variant_reference": "TSRN_U_IGREEN_L",
          "quantity": 3
        }
      ],
    },
  ],
  "count": 2
}
```


### HTTP Request

`GET https://plus.teezily.com/api/v2/orders`

Available parameters, in addition to [pagination](./#pagination):

Parameter |  Type | Description
--------- |  ---- | -----------
status | String | Filter by status

### HTTP Response

Returns all [Orders](./#order) objects paginated

Parameter |  Type | Description
--------- |  ---- | -----------
results | Array | [Orders](./#order) objects
count | Integer | Number of results


## Fulfill an order

```shell
curl --location --request PUT 'https://plus.teezily.com/api/v2/orders/152/fulfill' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
```

```python
import http.client

conn = http.client.HTTPSConnection("plus.teezily.com", undefined)
payload = ''
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
}
conn.request("PUT", "/api/v2/orders/152/fulfill", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

require "uri"
require "net/http"
```

```ruby
url = URI("https://plus.teezily.com/api/v2/orders/152/fulfill")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Put.new(url)
request["Accept"] = "application/json"
request["Authorization"] = "Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9"

response = http.request(request)
puts response.read_body
```

> No content response

Once an order is created, in order to send it to production you need to use the fulfill API method.

### HTTP Request

`PUT https://plus.teezily.com/api/v2/orders/{id}/fulfill`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | String | **Yes** | The order ID


### HTTP Response

No content.

## Cancel an order

```shell
curl --location --request PUT 'https://plus.teezily.com/api/v2/orders/152/cancel' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
```

```python
import http.client

conn = http.client.HTTPSConnection("plus.teezily.com", undefined)
payload = ''
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9'
}
conn.request("PUT", "/api/v2/orders/152/fulfill", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

require "uri"
require "net/http"
```

```ruby
url = URI("https://plus.teezily.com/api/v2/orders/152/cancel")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Put.new(url)
request["Accept"] = "application/json"
request["Authorization"] = "Bearer d9119ab7-38df-4b05-ba8f-f374c022fff9"

response = http.request(request)
puts response.read_body
```

> No content response

If an order is not yet produced you might still be able to cancel it using the following endpoint.

### HTTP Request

`PUT https://plus.teezily.com/api/v2/orders/{id}/cancel`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | **Yes** | String | The order ID

### HTTP Response

No content.

<!---
Returns an [Order](./#order) object with the following fields appended to it

Parameter |  Type | Description
--------- |  ---- | -----------
status | String | Current order status `unfulfilled` `fulfilled` `shipped`
--->
<!--
<aside class="warning">Do we have address check ? current order statuses ? total computations see with charles ?, order => state/postcode weirdy ? cancel only http status ? replace PUT by PATCH ? default shipping method ? Retail finishion ? eternal params ordering /id, top left scale 0 to 1 or 0 to 100, talk about printful mockup API => possibility to access printfile / mokcups ?</aside>
-->

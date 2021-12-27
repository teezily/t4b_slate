# Orders

## Create an order

```json
{

}
```

### HTTP Request

`POST http://plus.teezily.com/api/v2/orders`

### Order

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
external_id | No| String | Your Order ID: O-xxx. Usefull to track orders. The API will raise an error if you have any other non-cancelled orders with the same `external_id`
address | **Yes** | Object | An [Address](/#address) Object. The API will attempt to verify the address before accepting order
shipping_method | No | String | Can be `economy` or `express`
line_items | **Yes** | Array | An array of [Line Item](/#line-item) Object
retail | No | Object | A [Retail](/#retail) object for invoicing
status | No | String | Fulfillment internal status. do not submit this parameter for creation

### HTTP Response
Returns an [Order](/#order) object

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
zipcode | **Yes** | String | Some countries do not require zipcodes, in that case put an empty string
state | No | String | Some countries do not require state codes, if it is the case the API will raise an error
country_code | **Yes** | String | Formatted as ISO 3166-1 two-letter
skip_verified_delivery | No | Boolean | Skip address delivery verification

### Line Item

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
external_id | No| String | Your unique line item ID. Usefull to track line items. The API will raise an error if you have any other non-cancelled line items with the same `external_id`
variant_reference | **Yes** | String | The variant reference, see the [Product](/#product) endpoint
quantity | **Yes** | Integer
designs  | **Yes** | Array | An array of [Design](/#design) object
retail_price | No | String | Value of single item as purchased from the end customer. Used if VAT is provided so we can generate an invoice for you

### Design

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
key | **Yes** | String | Can be `front`, `back`, ... see our [Design specification](/#design-specification) `Side key` column
design_url | No | String | The url of the production design. Either `design_url` or `design_file` must be specified
design_file | No | File | If you wish to submit your payload in `multipart/form-data` and attach directly the file in it. Either `design_url` or `design_file` must be specified
position | No | String | Defaults to `auto`. Used to align the artwork within print area. Valid values are `top_left`, `top`, `top_right`, `center_left`, `center`, `center_right`, `bottom_left`, `bottom`, `bottom_right`. Using `auto` will adjust your design the best way possible given the product, it is recommended you use this setting.


### Retail

Retail costs that are to be displayed on the packing slip for international shipments. Retail costs are used only if every `line_item` in order contains the `retail_price` attribute.

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
vat_number | **Yes** | String |  
vat_currency | **Yes** | String | An ISO 4217 string representing the currency associated with your VAT number if you specify it
currency | **Yes** | String | An ISO 4217 string representing the currency. Used if VAT is provided so we can generate an invoice for you
shipping | **Yes** | String | Shipping price
handling | **Yes** | String | Handling price
discount | **Yes** | String | Discount price
total | **Yes** | String | Total price
tax | **Yes** |  String | Tax price

`total_price` should equal `line_items.retail_price` + `shipping_price` + `discount_price` + `handling_price`

## Get a single order

### HTTP Request

`GET http://plus.teezily.com/api/v2/orders/{id}`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | String | **Yes** | The order ID

`GET http://plus.teezily.com/api/v2/orders?external_id={id}`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | String | **Yes** | The external order ID

### HTTP Response

Returns an [Order](/#order) object

## Get all orders

### HTTP Request

`GET http://plus.teezily.com/api/v2/orders`

Parameter |  Type | Description
--------- |  ---- | -----------
page | Integer | A page number within the paginated result set
limit | Integer | Number of results to return per page
status | String | Filter by status


### HTTP Response

Returns all [Orders](/#order) objects paginated

Parameter |  Type | Description
--------- |  ---- | -----------
status | String
message | String
results | Array | [Orders](/#order) objects


## Fulfill an order

### HTTP Request

`PUT http://plus.teezily.com/api/v2/orders/fulfill/{id}`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | String | The order ID

`PUT http://plus.teezily.com/api/v2/orders/fulfill?external_id={external_id}`

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
id | String | The external order ID

### HTTP Response

Returns an [Order](/#order) object


<!---
Returns an [Order](/#order) object with the following fields appended to it

Parameter |  Type | Description
--------- |  ---- | -----------
status | String | Current order status `unfulfilled` `fulfilled` `shipped`
--->

<aside class="warning">Do we have address check ? current order statuses ? total computations see with charles ? response array result + message ?</aside>

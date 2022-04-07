# Catalog Products

## Get all Products and Variants

```shell
curl --location --request GET 'http://plus.teezily.com/api/v2/catalog/products' \
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
conn.request("GET", "/api/v2/catalog/products", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```ruby
require "uri"
require "net/http"

url = URI("http://plus.teezily.com/api/v2/catalog/products")

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
      "id": 156,
      "reference": "TSRN_U",
      "name": "round neck t-shirt unisex",
      "image": "http://example.org/products/1/preview.png",
      "variants": [
        {
          "id": 135,
          "reference": "TSRN_U_DHEATHERGREY_XXL",
          "name": "round neck t-shirt unisex dark heather grey XXL",
          "color": "dark heather grey",
          "size": "XXL"
        },
        {
          "id": 134,
          "reference": "TSRN_U_DHEATHERGREY_XL",
          "name": "round neck t-shirt unisex dark heather grey XL",
          "color": "dark heather grey",
          "size": "XL"
        }
      ]
    },
    {
      "id": 285,
      "reference": "TSVN_U",
      "name": "v-neck t-shirt unisex",
      "image": "http://example.org/products/1/preview.png",
      "variants": [
        {
          "id": 165,
          "reference": "TSVN_U_WHITE_XXL",
          "name": "v-neck t-shirt unisex white XXL",
          "color": "white",
          "size": "XXL"
        },
        {
          "id": 164,
          "reference": "TSVN_U_WHITE_XL",
          "name": "v-neck t-shirt unisex white XL",
          "color": "white",
          "size": "XL"
        }
      ]
    }
  ],
  "count": 2
}
```

This endpoint retrieves Products and their associated Variants.

### HTTP Request

`GET http://plus.teezily.com/api/v2/catalog/products`

Parameter | Required | Type | Description |
--------- | -------- | ---- | ----------- |
page | No | Integer | A page number within the paginated result set
limit | No | Integer | Number of results to return per page
name | No | String | Filter by name
reference | No | String | Filter by reference

### HTTP Response

Parameter | Type | Description |
--------- | ---- | ----------- |
results | Array | An array of [Products](./#product) |
count | Integer | Number of results

### Product

Parameter | Type | Description |
--------- | ---- | ----------- |
id | String | The product id
reference | String | The product reference
name | String | The product name
image | String | The product image
variants | Array | An array of [Variants](./#variant) |

### Variant

Parameter | Type | Description |
--------- | ---- | ----------- |
id | String | The variant id
reference | String | The variant reference
name | String | The variant name
color | String | The variant color
size | String | The variant size

<!--
<aside class="success">
Mutable variant ID ? filter one att ? add count ? Price currency ? rename limit to page_size / page_limit ?
</aside>
-->

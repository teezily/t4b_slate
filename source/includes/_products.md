# Catalog Products

## Get all Products and Variants

```ruby

```

```python

```

```shell

```

```javascript

```

> The above command returns JSON structured like this:

```json
{
  "next": "http://api.example.org/?page=4",
  "previous": "http://api.example.org?page=2",
  "count": 42,
  "results": [
    {
      "name": "Classic T-Shirt",
      "id": "2",
      "reference": "TSRN_U",
      "image": "http://cdn.api.example.org/product/5000-front.png",
      "variants": [
        {
          "id": "1",
          "reference": "TSRN_U_RED_XXL",
          "name": "CLASSIC T-SHIRT RED XXL",
          "size": "XXL",
          "color": "red",
          "hex_color_code": "ff0000",
          "price": 12.45,
          "price_currency": "USD"
        },
        {
          "id": "2",
          "reference": "TSRN_U_RED_3XL",
          "name": "CLASSIC T-SHIRT RED 3XL",
          "size": "3XL",
          "color": "red",
          "hex_color_code": "ff0000",
          "price": 12.45,
          "price_currency": "USD"
        }
      ]
    }
  ]
}
```

This endpoint retrieves Products and their associated Variants.

### HTTP Request

`GET http://plus.teezily.com/api/v2/catalog/products`

Parameter | Required | Type | Description |
--------- | -------- | ---- | ----------- |
page[number] | No | Integer | A page number within the paginated result set
page[size] | No | Integer | Number of results to return per page
filter[name] | No | String | Filter by name
filter[reference] | No | String | Filter by reference

### HTTP Response

Parameter | Type | Description |
--------- | ---- | ----------- |
count | Integer | Number of results
next | String | URL for the next page
previous | String | URL for the previous page
results | Array | An array of [Products](/#product) |

### Product

Parameter | Type | Description |
--------- | ---- | ----------- |
name | String | The product name
id | String | The product id
image | String | The product image
reference | String | The product reference
variants | Array | An array of [Variants](/#variant) |

### Variant

Parameter | Type | Description |
--------- | ---- | ----------- |
id | String | The variant id
reference | String | The variant reference
name | String | The variant name
size | String | The variant size
color | String | The variant color
hex_color_code | String | An hexadecimal code representing the color
price | Float | The variant price in the currency defined in your account setting
price_currency | String | The price currency, as configured in your account


<aside class="success">
Mutable variant ID ? filter one att ? add count ? Price currency ? rename limit to page_size / page_limit ?
</aside>
# Products

## Get All Products and Variants

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
  "status": "success",
  "result": [
    {
      "name": "Classic T-Shirt",
      "id": "2",
      "img": "https://d33jplnp2vyxjf.cloudfront.net/exproduct/5000-front.png",
      "variants": [
        {
          "id": "1",
          "reference": "TSRN_U_RED_XXL",
          "name": "CLASSIC T-SHIRT RED XXL",
          "size": "XXL",
          "color": "red",
          "hex_color_code": "ff0000",
        },
        {
          "id": "2",
          "reference": "TSRN_U_RED_3XL",
          "name": "CLASSIC T-SHIRT RED 3XL",
          "size": "3XL",
          "color": "red",
          "hex_color_code": "ff0000",
        }
      ]
    }
  ] ...
}
```

This endpoint retrieves Products and their associated Variants.

### HTTP Request

`GET http://plus.teezily.com/api/v2/catalog/products`


### HTTP Response

Parameter | Type | Description |
--------- | ---- | ----------- |
status | String |
result | Array | An array of [Products](/#product) |

### Product

Parameter | Type | Description |
--------- | ---- | ----------- |
name | String |
id | String |
img | String |
variants | Array | An array of [Variants](/#variant) |

### Variant

Parameter | Type | Description |
--------- | ---- | ----------- |
id | String
reference | String
name | String
size | String
color | String
hex_color_code | String 


<aside class="success">
Mutable variant ID ? Should we include pagination ? price ? add reference in product ? filter, remove status, remove message, zipcode vs postcde, external_id vs external_reference, check async
</aside>
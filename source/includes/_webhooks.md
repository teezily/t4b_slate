# Webhooks

Webhooks allow your system to receive notifications about certain events.

When an event occurs, the Teezily server will make a POST request to your defined URL containing a JSON object in the request body. Your server has to respond with HTTP status 200 OK, otherwise the request will be retried 12 times in increasing intervals (after 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024 and 2048 minutes).

## Creating a webhook

Webhook URL and secret key are defined in the settings of your Shop API.

If you already have a Shop API you can find it [here](/account/shops) otherwise create a new Shop API [here](/account/shop_api/new).

## Event list

Object | Event | Description
------ | ----- | -----------
Order | order_status_updated | Order status updated
Order | tracking_added | Order tracking added

### HTTP Request

<!-- id | String | ID of the object being sent over.
object | String | The type of object being sent: for now only `order` is implemented -->

Parameter | Type | Description
--------- | ---- | -----------
event.uuid | String | UUID of the event.
event.object_id | String | ID of the event's object being sent over.
event.object_type | String | the type event's object type being sent over.
event.action | String | The name of the event.
event.message | String | Human readable message of event.
event.timestamp | String | When the event occured.
data | String | The latest data of the object. This data matches the same format as the `GET` requests.

<!-- event.user | String | Who triggered the event. ("<email>" | "Dreamship Staff" | "System") -->

## Securing your Webhooks

Once your server is configured to receive payloads, it'll listen for any payload sent to the endpoint you configured. For security reasons, you probably want to limit requests to those coming from Teezily.

There are a few ways to go about this - for example, you could opt to whitelist requests from Teezily's IP address. An easy method is to and validate the information with a shared secret.

### Setting your shared secret

You can generate the secret by running `openssl rand -hex 20`.

When your secret token is set into your account, Teezily will use it to create a hash signature with each payload body. Teezily uses an HMAC hexdigest to compute the hash sha256 signature with your provided secret.

#### Secret example

`b19a1922449421904e94c3e139616b2faebd9c9d`

The payload body signature is passed along with each request in the headers as X-Tzy-Signature. The signature format is: `sha256={digest}`.

#### Signature example

`X-Tzy-Signature: sha256=c5e896be0dc286e8fe901d5dc1eae1422478475da21d64dfb4563c08e05ca12f`

### Validating payloads from Teezily

Next, compute a request body hash using your API key, and ensure that the hash from Teezily matches. Teezily uses an HMAC hexdigest to compute the hash. Always use "constant time" string comparisons, which renders it safe from certain timing attacks against regular equality operators.

Ruby on Rails example:

```ruby
# The raw payload in the request body from Teezily
# ex: {"message":"test content"}
request_body = request.raw_post

# The signature in the `X-Tzy-Signature` header
# ex: sha256=3a0185ce8cc75387bc45dec59e4e119f8ba26823e10c0f60ba7522f001bf1627
request_signature = request.headers['X-Tzy-Signature']

# Your secret key
# You have set it with your ShopAPI callback URL in T4B application
your_secret = 'secret'

# Compute digest data
your_digest = OpenSSL::HMAC.hexdigest('sha256', your_secret, request_body)

# Prefix the digest to build your own signature
your_signature = "sha256=#{your_digest}"

# Compare with "constant time" string comparisons fonction:
# It should be true otherwise the request doesn't come from Teezily
Rack::Utils.secure_compare(request_signature, your_signature)
```

Where `[SECRET_KEY]` is your secret key.


<!---

Order |
---------------- |
order-created |
order-deleted |
order-reprinted |
order-status-updated |
order-details-updated |
tracking-added |
tracking-updated |
tracking-deleted |
print-file-added |
print-file-removed |
line-item-details-updated |
line-item-added |
line-item-removed |
line-ticket-opened |
line-ticket-closed |

Product |
----------------- |
product-created |
product-deleted |


Item Variant |
---------------------- |
item-variant-availability-updated |
item-variant-added |

## Gearment

All |
--- |
order_completed |
order_canceled |
tracking_updated |
shipping_address_unverified |

## Printify

Shop events |
-------------------- |
shop:disconnected |

Product events |
----------------------- |
product:deleted |
product:publish:started |

Order events |
--------------------- |
order:created |
order:updated |
order:sent-to-production |
order:shipment:created |
order:shipment:delivered |


## Printful

All |
--- |
Package shipped |
Package returned |
Order created |
Order updated |
Order failed |
Order canceled |
Product synced |
Product updated |
Stock updated |
Order put hold |
Order remove hold |


--->

<!--
<aside class="warning">I don't see the utility of registering webhooks.... if a webhook URL is registered we should just push on it, how about packages split tracking ? should we push line item or for tracking</aside>
-->

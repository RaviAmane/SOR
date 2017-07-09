**API Optimization for Mobile Applications (Efficient Network Usage)**
---
In order to improve the performance for mobile applications, the API uses partial resources.
- **Partial Response for `HTTP GET` on `/customers/{customerId}`.**
	- For `HTTP GET` operation, specify the response fields by using `fields` query parameter. This way only the required fields are returned optimizing the network traffic.
- **Update Selected Fields with `HTTP PATCH`**
	- Use of `HTTP PATCH` operation where only the fields that need changing are sent over the network.
	- In addition, like GET operation, specify the response fields by using `fields` query parameter. This way only the required fields are returned over the network. No fields are returned if this query parameter is not passed; in that case HTTP code `204` is returned further optimizing the network traffic.

**Examples**

The following example shows the use of the fields parameter.

- **Simple request** This HTTP GET request omits the fields parameter and returns the full resource.

`GET /v1/customers/123456`

For above request that does not send any query parameter, the full resource response is send back that would include the following fields.

  *HTTP Status*
  
  `200 OK`
  
  *Response Body*
  
  `{
      "id" : 123456,
      "firstName": "David",
      "lastName" : "J",
      "addresses" : [
        {
          "type" : "home",
          "value" : "David's home address"
        },
        {
          "type" : "shipping",
          "value" : "David's shipping address"
        },
        {
          "type" : "billing",
          "value" : "David's billing address"
        }
    ],
    "isDeleted" : false
  }`

Request for a partial response: The following request for this same resource uses the fields parameter to significantly reduce the amount of data returned.

GET /v1/123456?fields=firstName,lastName

Partial response: In response to the above request, the API returns back a response that contains only the requested fields, e.g. firstName and lastName.

200 OK

{
  "firstName": "David",
  "lastName" : "J",
}

PATCH Request:

You can also avoid sending unnecessary data when modifying resources. To send updated data only for the specific fields that you’re changing, use the HTTP PATCH verb.

The short example below shows how using patch minimizes the data you need to send to make a small update.

PATCH https://www.example.com/demo/v1/123456
Content-Type: application/json

{
  "firstName": "New First Name",
  "lastName": "New Last Name"
}

Response: In this case response body is null keeping the network traffic to least.

204 No Content

If you need the updated fields to be returned, use query parameter to do so.

PATCH https://www.example.com/demo/v1/123456?fields=firstName,lastName
Content-Type: application/json

{
  "firstName": "New First Name",
  "lastName": "New Last Name"
}

Response: In this case, the API returns the requested fields.

204 No Content

{
  "firstName": "New First Name",
  "lastName": "New Last Name"
}

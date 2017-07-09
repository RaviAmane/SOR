**API Optimization for Mobile Applications (Efficient Network Usage)**
---
In order to improve the performance for mobile applications, the API uses partial resources.
### Receive Partial Resource for `HTTP GET` on `/customers/{customerId}`
  - For `HTTP GET` operation, specify the response fields by using `fields` query parameter. This way only the required fields are returned optimizing the network traffic.
### Update Only Select Fields with `HTTP PATCH`
  - Use of `HTTP PATCH` operation where only the fields that need changing are sent over the network.
  - In addition, like GET operation, specify the response fields by using `fields` query parameter. This way only the required fields are returned over the network. No fields are returned if this query parameter is not passed; in that case HTTP code `204 No Content` is returned further optimizing the network traffic.
  - In order to enhance the developer experience however, we also provide `HTTP PUT`.

## Examples

The following is a series of examples that demonstrate the use of API with various netwrok traffic.

### Simple `GET` Request - Receive Full Resource

This HTTP GET request omits the `fields` query parameter. the API returns the full resource.

**Request**

`GET /v1/customers/123456`

**Response**

*HTTP Status*
  
`200 OK`
  
*Response Body*
  
`
{
  "id": 123456,
  "firstName": "David",
  "lastName": "J",
  "addresses": [
  {
    "type": "home",
    "value": "David's home address"
  },
  {
    "type": "shipping",
    "value": "David's shipping address"
  },
  {
    "type": "billing",
    "value": "David's billing address"
  }
  ],
  "isDeleted": false
}
`

### Optimized `GET` Request with the use of `fields` Query Parameters - Receive Partial Resource

This HTTP GET request adds the `fields` query parameter. The API returns the partial resource.

**Request**

`GET /v1/customers/123456?fields=firstName,lastName`

**Response**

*HTTP Status*
  
`200 OK`
  
*Response Body*
  
` { "firstName": "David", "lastName": "J" }`

### Update Partial Object with `PATCH` Request

You can also avoid sending unnecessary data when modifying resources. To send updated data only for the specific fields that you’re changing, use the `HTTP PATCH` verb. The example below shows how using patch minimizes the data you need to send to make the update.

**Request**

`PATCH /v1/123456`

*Request Body*

` { "firstName": "John", "lastName": "Doe" }`

**Response**

*HTTP Status*
  
`200 OK`
  
*Response Body*
  
`
{
  "id": 123456,
  "firstName": "John",
  "lastName": "Doe",
  "addresses": [
  {
    "type": "home",
    "value": "David's home address"
  },
  {
    "type": "shipping",
    "value": "David's shipping address"
  },
  {
    "type": "billing",
    "value": "David's billing address"
  }
  ],
  "isDeleted": false
}
`

### Update Partial Object with `PATCH` Request and Receive null Response by using `fields` Query Parameter

The example below shows how in addition to using PATCH, you could use `fields` query parameter to recieve null response thus further reducing the netwrok traffic.

**Request**

`PATCH /v1/123456?fields=null`

*Request Body*

` { "firstName": "John", "lastName": "Doe" }`

**Response**

*HTTP Status*
  
`204 No Content`
  
*No Response Body*

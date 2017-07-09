# System Of Records (SOR) API
> Best Practices for RESTful API Design using RAML

This is an example API design using RAML. The implementation of this API using Mulesoft Studio is coming soon. In its current state, the project demonstrates the following:

- Best practices for RESTful API design.
- Use of built in aspects of the HTTP protocol (status codes, headers, etc.).
- Use of various RAML features.
- Performance considerations when designing the API for mobile applicationsl; that is feficient use of the network.
- Important Note: In its current state, this projects includes the API design using RAML.
- Coming Soon: I am working on implementing this RESTful API in Mulesoft with test stubs for the consumer and provider systems. The implementation will be added to this project soon.

This API, in its present state, contains a single resource `/customers`. The operations allowed on the `/customers` resource include:

- List Customers
  - `HTTP GET`
  - The request must contain `If-Modified-Since` header to specify the datetime. The records updated since this datetime will be returned. For more details see [API Documentation](API_DOCUMENTATION.md).
  - This operation supports pagination.
- Create a New Customer
  - `HTTP POST`
- Update a Customer
  - Supports both `HTTP PATCH` and `HTTP PUT`
- Remove a Customer
  - `HTTP DELETE`

## Getting started

You can use this project in various ways:

- Use the api.raml (and the subdirectories/files) in your API design.
- Create your own Mulefost project by importing api.raml using APIkit.
- Create an API in API Designer (a part of Mulesoft Anypoint Platform) and import it into your Mulesoft project using APIkit.

### API Definition

A detailed API definition is provided at:

- [API Documentation](API_DOCUMENTATION.md)

### Commentary on API Usage

Detailed commentaries on various use cases of this API are provided at:

- [Use Case 1: Maintain a Copy of Customers Data](USE_CASE_1.md)
- [Use Case 2: API Optimization for Mobile Applications](USE_CASE_2.md)
- [Use Case 3: Extention of this API to Support Future Resources](USE_CASE_3.md)

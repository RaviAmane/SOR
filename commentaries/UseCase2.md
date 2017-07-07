API Optimization for Mobile Applications (Efficient Network Usage)

- Partial response
	- With GET operation, specify the response fields by using fields request parameter. This way only the required fields are returned over the network.
- Patch
	- Use of PATCH HTTP operation where the fields that need changing are sent over the network.
- gzip (not recommanded for this API)
	- The use of gzip is not recommanded for the customers API due to small resource size. For instance, google recommands NOT using gzip for resources smaller than 150 bytes; using gzip in such cases can actually make them larger. In addition, gzip uses additional CPU cycles.


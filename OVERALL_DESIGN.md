While seperate commentaries are given for each of three use cases, the following commetary applies to the entire API design.

- For customer object, instead of array of "addresses", I would have prefered to use specific address fields, e.g. billingAddress and shippingAddress.
		- Pros: This would give more granualarity especially needed for the network optimization for mobile applications. With this approach the API client could get and update the individual address.
		- Cons: This would make the object regid; i.e. customer can not hold any other address than the two.


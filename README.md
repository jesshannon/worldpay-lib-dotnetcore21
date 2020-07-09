# worldpay-lib-dotnetcore21
Directly ported from Worldpays official standard .net lib

This is still using the old style ConfigurationManager so will need an AppSettings section in Web.Config or App.Config.

DotNet Library for Worldpay REST API

## Usage

Initialize the REST client with the default URL and the specified service key and then use the required service:
```c#

WorldpayRestClient restClient = new WorldpayRestClient("https://api.worldpay.com/v1", "YOUR_SERVICE_KEY");

var orderRequest = new OrderRequest()
{
    amount = 1999,
    currencyCode = CurrencyCode.GBP,
    name = "Joe Bloggs",
    orderDescription = "Order description"
};

var address = new Address()
{
    address1 = "line 1",
    address2 = "line 2",
    city = "city",
    countryCode = CountryCode.GB,
    postalCode = "AB1 2CD"
};

orderRequest.billingAddress = address;

try {
    OrderResponse orderResponse = restClient.GetOrderService().Create(orderRequest);
    Console.WriteLine("Order code: " + orderResponse.orderCode);
} catch (WorldpayException e) {
	Console.WriteLine("Error code:" + e.apiError.customCode);
    Console.WriteLine("Error description: " + e.apiError.description);
    Console.WriteLine("Error message: " + e.apiError.message);
}
```

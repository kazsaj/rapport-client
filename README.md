# PHP Client Library for Venditan Rapport #

http://www.venditan.com/rapport

## Install with Composer ##

```bash
composer require venditan/rapport-client dev-master
```

# Examples #

In all the examples below, we will assume you have created a client object with the right credentials, like this:

```php
// Create the client with your supplied client id and api key
$obj_client = new \Venditan\Rapport\Client('company', 'api-key');
```

## Order Dispatch ##

```php
// Add and configure the target recipient/user
$obj_client->addUser()->id('1955')->name('Marty')->email('marty@mcfly.com')->mobile('07019551985');

// Set-up the transaction
$obj_client->addTransaction()->id('2015')->courier('Western Union')->tracking('ELB1885');

// Set the type of event and publish
$obj_client->event('order_dispatched')->send();
```

## Service Message ##

```php
// Add and configure the target recipient/user
$obj_client->addUser()->id('1955')->name('Marty')->email('marty@mcfly.com')->mobile('07019551985');

// Set-up the transaction (optional, useful context)
$obj_client->addTransaction()->id('2015');

// Set a service message
$obj_client->addMessage()->title('Order Update')->body('Hi Marty. I am safe in 1885.')->from('ELB');

// Set the type of event and publish
$obj_client->event('service_message')->send();
```

## Retrieve Thread Messages ##

```php
$obj_client->getThreadForTransaction('2015');
```

The response will be a stdClass object decoded from the following JSON

```json
{
    id: "oid-2015",
    topic: "Order 2015",
    messages: [
        {
            title: "Order Accepted",
            message: "Thank you for your order.",
            created: "2015-01-01 12:00:00"
        }
    ]
}
```
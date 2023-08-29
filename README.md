# PayTech - PHP API Client

## Forked from papihack/paytech-php-client

This is a simple `SDK Client` or `API Client` for `PayTech Online Payment Gateway`.

Check out [PayTech SN Website](https://paytech.sn).

## How to use it

First of all, install the package or library via composer

- `composer require supermalang/paytech-client`

After that, setup the API config with your parameters like this :

```php
    \PayTech\Config::setApiKey('your_api_key');
    \PayTech\Config::setApiSecret('your_api_secret');

    /*
     * you can set one of this two environment TEST or PROD
     * you can just set the env mode via \PayTech\Enums\Env::TEST or \PayTech\Enums\Env::PROD
     * Like the following example
     * !!! By default env is PROD !!!
     * You can also directly set test or prod as a string if you want
     * Like \PayTech\Config::setEnv('test') or \PayTech\Config::setEnv('prod')
    */

    \PayTech\Config::setEnv(\PayTech\Enums\Env::PROD);

    /*
     * The PayTech\Enums\Currency class defined authorized currencies
     * You can change XOF (in the following example) by USD, CAD or another currency
     * All allowed currencies are in \PayTech\Enums\Currency class
     * !!! Notice that XOF is the default currency !!!
    */

    \PayTech\Config::setCurrency(\PayTech\Enums\Currency::XOF);

    /* !!! Note that if you decide to set the ipn_url, it must be in https !!! */

    \PayTech\Config::setIpnUrl('your_ipn_url');
    \PayTech\Config::setSuccessUrl('your_success_url');
    \PayTech\Config::setCanceUrl('your_cancel_url');

    /*
     * if you want the mobile success or cancel page, you can set
     * the following parameter
    */

    \PayTech\Config::setIsMobile(true);
```

Then you can proceed with :

```php
    $article_price = 15000;
    $article = new \PayTech\Invoice\InvoiceItem('article_name', $article_price, 'command_name', 'ref_command');

    /* You can also add custom data or fields like this */

    \PayTech\CustomField::set('your_field_name', 'your_field_value');

    /* Make the payment request demand to the API */

    \PayTech\PayTech::send($article);

    /* Get the API Response */

    $response = [
        'success'      => \PayTech\ApiResponse::getSuccess(),
        'errors'       => \PayTech\ApiResponse::getErrors(),
        'token'        => \PayTech\ApiResponse::getToken(),
        'redirect_url' => \PayTech\ApiResponse::getRedirectUrl(),
    ];
```

After that, if you have a success response, you can redirect your user to the `$response['redirect_url']` so that he can make the payment.  
You can process the response as you wish by directly manipulating `\PayTech\ApiResponse`.
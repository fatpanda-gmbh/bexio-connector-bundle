# Bexio connector bundle

A Symfony bundle that wraps the [Bexio Connector](https://github.com/fatpanda-gmbh/bexio-connector) library.

## Setup

Add to composer.json

```js
composer require fatpanda-gmbh/bexio-connector-bundle
```

Then enable it in your kernel:

```php
// app/AppKernel.php
public function registerBundles()
{
    $bundles = array(
        //...
        new Fatpanda\BexioConnectorBundle\BexioConnectorBundle(),
        //...
```
## Usage

The bundle registers the `bexio_connector` service. 
To use it, you need a valid Bexio API token that you can generate at https://office.bexio.com/index.php/admin/apiTokens#/

```yaml
app.service.bexio:
  class: AppBundle\Service\BexioService
    arguments:
      $connector: '@bexio_connector'
      $token: %token%    
```

```php
use Fatpanda\BexioConnector\BexioConnector;

class BexioService
{
    /**
     * @var BexioConnector
     */
    private $connector;

    public function __construct(BexioConnector $connector, string $token)
    {
        $this->connector = $connector;
        $this->connector->setToken($token);
    }

    public function getContactsList()
    {
        $this->connector->getContactsList();
    }
}
```

## License
This bundle is under the MIT license. See the complete license in the bundle:

    Resources/meta/LICENSE



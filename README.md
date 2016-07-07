Chef
====

The Chef Server API is used to provide access to objects on the Chef Server, including nodes, environments, roles, cookbooks (and cookbook versions), and to manage an API client list and the associated RSA public key-pairs.

*This is a generic library and has additional support for the Laravel framework.*

This is forked from https://github.com/aashley/php-chef I have some different requirements and will be maintaining it independantly

Installation
------------

Add `aashley/chef` as a requirement to composer.json:

    {
        "require": {
            "aashley/chef": "dev-master"
        }
    }

Update your packages with `composer update` or install with `composer install`.

Usage
-----

Create a chef object like this:

    // composer
    require_once 'vendor/autoload.php';
    use aashley\Chef\Chef;
    
    // create chef object
    $chef = new Chef($server, $client, $key, $version);
    
    // API request
    $response = $chef->api($endpoint, $method, $data);

See http://docs.opscode.com/api_chef_server.html for all available endpoints.

Examples
--------

Get nodes:

    $nodes = $chef->get('/nodes');

Create a data bag:

    $bag = new stdClass;
    $bag->name = "test";
    
    $resp = $chef->post('/data', $bag);

Update a node:

    $node = $chef->get('/nodes/webserver1');
    $node->attributes->type = "webserver";
    
    $chef->put('/nodes/webserver1', $node);

Delete a data bag:

    $chef->delete('/data/test/item');
    

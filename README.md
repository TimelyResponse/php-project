## Installation

Download the "`api.php`" file from the latest release:

https://github.com/mevdschee/php-crud-api/releases/latest or direct from:  
https://raw.githubusercontent.com/mevdschee/php-crud-api/main/api.php

This is a single file application! Upload "`api.php`" somewhere and enjoy!

For local development you may run PHP's built-in web server:

    php -S localhost:8080

Test the script by opening the following URL:

    http://localhost:8080/api.php/records/posts/1

Don't forget to modify the configuration at the bottom of the file.

Alternatively you can integrate this project into the web framework of your choice, see:

- [Automatic REST API for Laravel](https://tqdev.com/2019-automatic-rest-api-laravel)
- [Automatic REST API for Symfony 4](https://tqdev.com/2019-automatic-rest-api-symfony)
- [Automatic REST API for SlimPHP 4](https://tqdev.com/2019-automatic-api-slimphp-4)

In these integrations [Composer](https://getcomposer.org/) is used to load this project as a dependency.

For people that don't use composer, the file "`api.include.php`" is provided. This file contains everything 
from "`api.php`" except the configuration from "`src/index.php`" and can be used by PHP's "include" function.

## Configuration

Edit the following lines in the bottom of the file "`api.php`":

    $config = new Config([
        'username' => 'xxx',
        'password' => 'xxx',
        'database' => 'xxx',
    ]);

These are all the configuration options and their default value between brackets:

- "driver": `mysql`, `pgsql`, `sqlsrv` or `sqlite` (`mysql`)
- "address": Hostname (or filename) of the database server (`localhost`)
- "port": TCP port of the database server (defaults to driver default)
- "username": Username of the user connecting to the database (no default)
- "password": Password of the user connecting to the database (no default)
- "database": Database the connecting is made to (no default)
- "command": Extra SQL to initialize the database connection (none)
- "tables": Comma separated list of tables to publish (defaults to 'all')
- "mapping": Comma separated list of table/column mappings (no mappping)
- "geometrySrid": SRID assumed when converting from WKT to geometry (`4326`)
- "middlewares": List of middlewares to load (`cors`)
- "controllers": List of controllers to load (`records,geojson,openapi,status`)
- "customControllers": List of user custom controllers to load (no default)
- "openApiBase": OpenAPI info (`{"info":{"title":"PHP-CRUD-API","version":"1.0.0"}}`)
- "cacheType": `TempFile`, `Redis`, `Memcache`, `Memcached` or `NoCache` (`TempFile`)
- "cachePath": Path/address of the cache (defaults to system's temp directory)
- "cacheTime": Number of seconds the cache is valid (`10`)
- "jsonOptions": Options used for encoding JSON (`JSON_UNESCAPED_UNICODE`)
- "debug": Show errors in the "X-Exception" headers (`false`)
- "basePath": URI base path of the API (determined using PATH_INFO by default)

All configuration options are also available as environment variables. Write the config option with capitals, a "PHP_CRUD_API_" prefix and underscores for word breakes, so for instance:

- PHP_CRUD_API_DRIVER=mysql
- PHP_CRUD_API_ADDRESS=localhost
- PHP_CRUD_API_PORT=3306
- PHP_CRUD_API_DATABASE=php-crud-api
- PHP_CRUD_API_USERNAME=php-crud-api
- PHP_CRUD_API_PASSWORD=php-crud-api
- PHP_CRUD_API_DEBUG=1

The environment variables take precedence over the PHP configuration.

## Limitations

These limitation and constrains apply:

  - Primary keys should either be auto-increment (from 1 to 2^53) or UUID
  - Composite primary and composite foreign keys are not supported
  - Complex writes (transactions) are not supported
  - Complex queries calling functions (like "concat" or "sum") are not supported
  - Database must support and define foreign key constraints
  - SQLite cannot have bigint typed auto incrementing primary keys
  - SQLite does not support altering table columns (structure)
    
## Features

The following features are supported:

  - Composer install or single PHP file, easy to deploy.
  - Very little code, easy to adapt and maintain
  - Supports POST variables as input (x-www-form-urlencoded)
  - Supports a JSON object as input
  - Supports a JSON array as input (batch insert)
  - Sanitize and validate input using type rules and callbacks
  - Permission system for databases, tables, columns and records
  - Multi-tenant single and multi database layouts are supported
  - Multi-domain CORS support for cross-domain requests
  - Support for reading joined results from multiple tables
  - Search support on multiple criteria
  - Pagination, sorting, top N list and column selection
  - Relation detection with nested results (belongsTo, hasMany and HABTM)
  - Atomic increment support via PATCH (for counters)
  - Binary fields supported with base64 encoding
  - Spatial/GIS fields and filters supported with WKT and GeoJSON
  - Mapping table and column names to support legacy systems
  - Generate API documentation using OpenAPI tools
  - Authentication via API key, JWT token or username/password
  - Database connection parameters may depend on authentication
  - Support for reading database structure in JSON
  - Support for modifying database structure using REST endpoint
  - Security enhancing middleware is included
  - Standard compliant: PSR-4, PSR-7, PSR-12, PSR-15 and PSR-17


                "id": 1,
                "title": "Hello world!",
                "content": "Welcome to the first post.",
                "created": "2018-03-05T20:12:56Z"
            }
        ]
    }

On list operations you may apply filters and joins.

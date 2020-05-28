# 👨🏾‍💻

## Slim 4 Simple Auth Starter

---

- Make sure you have composer downloaded and set up, run `composer` command

  ```
     ______
    / ____/___  ____ ___  ____  ____  ________  _____
   / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
  / /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
  \____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                      /_/
  Composer version 1.9.0 2019-08-02 20:55:32

  ```

- Create the project directory, cd into it and require slim 4
  - `composer require slim/slim:"4.*"`
  - `composer require slim/psr7`
- To test that everything is working as it should at this point, create a new dir & file `public/index.php`
- Copy the following hello world app in index.php

  ```php
      <?php

      use Slim\Factory\AppFactory;
      use Psr\Http\Message\ServerRequestInterface as Request;
      use Psr\Http\Message\ResponseInterface as Response;

      require __DIR__ . '/../vendor/autoload.php';

      $app = AppFactory::create();

      $app->get('/', function(Request $request, Response $response, $parameters){
          $response->getBody()->write("Hello World");
          return $response;
      });

      $app->run();

  ```

- Then cd into public and run `php -S localhost:8080`
  - Visiting url and a simple "Hello World" message should be on the page
- Now to start structuring the app, create a new dir & file in the root `bootstrap/index.php`
- For containers with dependency injection, require a di lib
  - `composer require php-di/php-di`
  - Requires php 7.2 or above.
- Copy all the code in `public/index.php` into `bootstrap/index.php`
  - replace with `require '../bootstrap/index.php'`
- in `bootstrap/index.php` add the following : create a DI enabled container and set it on the AppFactory.

  ```php
      <?php
      use DI\Container;
      use Slim\Factory\AppFactory;
      use Psr\Http\Message\ServerRequestInterface as Request;
      use Psr\Http\Message\ResponseInterface as Response;

      require __DIR__ . '/../vendor/autoload.php';

      $container = new Container;
      AppFactory::setContainer($container);

      $app = AppFactory::create();

      $app->get('/', function(Request $request, Response $response, $parameters){
          $response->getBody()->write("Hello World");
          return $response;
      });

      $app->run();

  ```

- Now the app object knows about the container and we can begin by putting some logging settings, so that error logs are formatted in a readable fashion...

  - create a new dir & file from project root `app/settings.php` and insert the following :

    ```php

        <?php

        use \Psr\Container\ContainerInterface;

        return function(ContainerInterface $container){
            $container->set('settings', function(){
                return [
                    'displayErrorDetails' => true,
                    'logErrorDetails' => true,
                    'logErrors' => true,
                ];
            });
        };

    ```

  - To test, try accessing an endpoint that doesn't exist.

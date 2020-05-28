# 👨🏾‍💻

## Slim 4 Simple Auth Starter

---

- Make sure you have composer downloaded and setup, run `composer` command

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

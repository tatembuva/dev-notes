## ✏️

### Laravel ECommerce Starter Template

_Steps I took setting up laravel with tailwind,svelte and paynow..._

[_back_](../../README.md)

---

#### Sections

- [Initial Setup](#initial-setup)
- [Models](#models)
- [Static Pages](#static-pages)
- [SSR Pages](#ssr-pages)
- [SPA Pages](#spa-pages)

## Initial Setup

Firstly from a start, get the laravel installer with composer...

```bash
composer global require "laravel/installer=~1.1"

```

Start a new project with installer...

```bash
laravel new <project-name>
```

Serve the base project...
The `--port=` option is optional, defaults to `8000`

```bash
php artisan serve --port=8080
```

Now we add Tailwindcss...

```bash
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```

Create the default tailwind.config.js file...

```bash
npx tailwindcss init
```

---

**OR you could just install laravel/breeze and the tailwind css will be setup for you**

```bash
laravel new <project-name>
cd <project-name>
composer require laravel/breeze --dev
```

Then for the setup...

```bash
php artisan breeze:install
npm install && npm run dev
```

To run...

```bash
php artisan serve
```

Adding svelte...

```bash
npm install wewowweb/laravel-mix-svelte
```

To `webpack.mix.js` add a mix task for svelte...

```javascript
require("laravel-mix-svelte");

mix
  .js("resources/js/svelte/app.js", "public/js/svelte")
  .sass("resources/sass/app.scss", "public/css")
  .svelte();
```

Lastly...

```bash
php artisan migrate
```

## Role Based Auth

Using the laratrust package...

```bash
composer require santigarcor/laratrust
```

Publish config file...

```bash
php artisan vendor:publish --tag="laratrust"
```

If the above 👆🏾command throws an error then try clear artisan config cache...

```bash
php artisan config:clear
```

This command will generate the migrations, create the Role and Permission models (if you are using the teams feature it will also create a Team model) and will add the trait to the configured user models.👇🏽
_Before running this go to `config/laratrust.php` file and change defaults_

```bash
php artisan laratrust:setup && composer dump-autoload
```

Run a fresh migration...

```bash
php artisan migrate:fresh
```

Laratrust comes with a database seeder, this seeder helps you fill the permissions for each role depending on the module, and creates one user for each role.

```bash
php artisan laratrust:seeder
```

Then publish files to project...

```bash
php artisan vendor:publish --tag="laratrust-seeder" && composer dump-autoload
```

In the database/seeds/DatabaseSeeder.php file you have to add this to the run method...

```php
$this->call(LaratrustSeeder::class);
```

To setup the roles and permissions edit `config/laratrust_seeder.php` and run a migaration...

Then finally...

```bash
php artisan db:seed
```

Now all the roles defined in `config/laratrust_seeder.php` are stored on the db,
create a new controller for the 3 types of dashboards in this project...

```bash
php artisan make:controller DashboardController
```

Each type of dashboard `[customer|admin|superadmin]` will be its own svelte app,
svelte will be attached to an element within the blade template, the navbar will remain a blade component...

Put dashboard routes in a group, with auth middleware for all endpoints, roles are enforced at each endpoint...( nested route groups ? )

In `routes/web.php` add :

```php
Route::group(['middleware' => ['auth']], function() {
    Route::get('/dashboard', 'App\Http\Controllers\DashboardController@index')->name('dashboard');
});
```

The DashboardController will switch between user_roles and render the apropriate view, and each view is its own independant svelte app, modular : later mobile clients can be added with little friction...

---

For api auth, the laravel Sanctum package...

```bash
composer require laravel/sanctum
```

Publish the sanctum service provider and migrate...

```bash
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
&& php artisan migrate
```

---

## Models/Database Schema

- Product
  - name
  - slug
  - description
  - price
  - timestamps\*

## Static Pages

- [ ] Static Pages
  - [ ] Frontpage
    - [ ] Navbar (guest, logged in, admin )
    - [ ] Header/Hero Section
  - [ ] Contact page (will also be the about us page + google maps store location)
  - [ ] Login & Register

## SSR Pages

- [ ] ?SSR Pages
  - [ ] Shop
  - [ ] can take a category add display category products
  - [ ] product search and filter search
  - [ ] Product detail page

#### SPA Pages/Components

- [ ] SPA (Svelte) Pages
  - [ ] Admin Dashboard
    - [x] creating independent svelte app and routing to it based on user-role
  - [ ] User Dashboard
    - [x] creating independent svelte app and routing to it based on user-role
  - [ ] Payment Wizard
    - [x] creating independent svelte app and routing to it based on user-role

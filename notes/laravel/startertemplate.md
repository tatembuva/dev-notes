## ✏️

### Laravel ECommerce Starter Teemplate

_Steps I took setting up laravel with tailwind,svelte and paynow..._

[_back_](../../README.md)

---

#### Sections

- [Initial Setup](#initial-setup)
- [Static Pages](#static-pages)

#### Initial Setup

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

#### Static Pages

- [o] Static Pages
  - [o] Frontpage
    - [] Navbar (guest, logged in, admin )
    - [] Header/Hero Section
  - [] Contact page (will also be the about us page + google maps store location)
  - [] Login & Register

#### SSR Pages

- [] ?SSR Pages
  - [] Shop
  - [] can take a category add display category products
  - [] product search and filter search
  - [] Product detail page

#### SPA Pages/Components

- [] SPA (Svelte) Pages
  - [] Admin Dashboard
  - [] User Dashboard
  - [] Payment Wizard

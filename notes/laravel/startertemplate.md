## ✏️

### Laravel ECommerce Starter Teemplate

_Steps I took setting up laravel with tailwind,svelte and paynow..._

[_back_](../README.md)

---

#### Sections

- [Initial Setup](#initial-setup)

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

# Installation
Documentation: (https://backpackforlaravel.com/docs/5.x/installation)
---

<a name="requirements"></a>
## Requirements

If you can run Laravel 8 or 9, you can install Backpack. Backpack does _not_ have additional requirements. 

For the following process, we assume:

- you have a [working installation of Laravel](https://laravel.com/docs/9.x#installation) (an existing project is fine, you don't need a *fresh* Laravel install);

- you have configured your .ENV file with your database and mail information;

- you can run the ```composer``` command from any directory (you have ```composer``` registered as a global command); if you need to run ```php composer.phar``` or reference another directory, please remember to adapt the commands below to your configuration;

<a name="installation"></a>
## Installation

<a name="install-core-packages"></a>
### Install using Composer

Go to your Laravel project's directory, in your terminal, then:

``` bash
composer require backpack/crud
php artisan backpack:install
```

Follow the prompts - in the end, the installer will also tell you your admin panel's URL, where you should go and login.

> **NOTE:** When the installer asks you if you would like to create and admin user, Backpack assumes that you are using the default user structure with `name, email and password` fields. If that's not the case, please reply **NO** to that question and manually create your admin user.

> **NOTE:** The installation command is interactive - it will ask you questions. You can bypass the questions by adding the `--no-interaction` argument to the install command. 

### Configure 

In most cases, it's a good idea to look at the configuration files and make the admin panel your own:
- You should change the configuration values in ```config/backpack/base.php``` to make the admin panel your own. Backpack is white label, so you can change everything: menu color, project name, developer name etc.
- By default all users are considered admins; If that's not what you want in your application (you have both users and admins), please:
    - Change ```app/Http/Middleware/CheckIfAdmin.php```, particularly ```checkIfUserIsAdmin($user)```, to make sure you only allow admins to access the admin panel;
    - Change ```app/Providers/RouteServiceProvider::HOME```, which will send logged in (but not admin) users to `/home`, to something that works for your app;
- If your User model has been moved from the default ```App\Models\User.php```, please change ```config/backpack/base.php``` to use the correct user model under the ```user_model_fqn``` config key;

### Create your Eloquent Models

Backpack assumes you already have your Eloquent Models properly set up. If you don't, **consider using something to quickly generate Migrations & Models**. You can use anything you want, but here are the options we recommend:

- a) Generate from a **web interface** - [Backpack Devtools](https://backpackforlaravel.com/products/devtools) - premium product, paid separately. A simple GUI to quickly generate Migrations, Models, Factories, Seeders and CRUDs, right from your browser. Works well for entities of all sizes.

- b) Generate from the **command-line** - [Laracasts Generators](https://github.com/laracasts/Laravel-5-Generators-Extended) - free & open-source. Adds a new artisan command so that you can do `php artisan make:migration:schema create_users_table --schema="username:string, email:string:unique"`. Works well for smaller entities.

- c) Generate from a **YAML file** - [LaravelShift's Blueprint](https://blueprint.laravelshift.com/) - free & open-source. Enables you to create a `draft.yml` file in your repo, where you can specify the column using their custom YAML syntax. Works well for small & medium entities.

### Create your CRUDs

For each Eloquent model you want to have an admin panel, run:

```bash
php artisan backpack:crud {model} # use the model name (singular)
```

Alternatively, you can generate CRUDs for all Eloqunet models, by running:

```bash
php artisan backpack:build
```

Then go through each CRUD file (Controller, Request, Route Item, Sidebar Item) and customize as you fit. If you don't know what those are, and how you can customize them... please take go through our [Getting Started](https://backpackforlaravel.com/docs/5.x/introduction#how-to-start) section, it's important. At the very least, read our [Crash Course](https://backpackforlaravel.com/docs/5.x/crud-tutorial).

<a name="install-add-ons"></a>
### Install Add-ons

In case you want to add extra functionality that's already been built, check out [the installation steps for the add-ons we've developed](/docs/{{version}}/install-optionals).

<a name="frequently-asked-questions"></a>
## Frequently Asked Questions

- **Error: The process X exceeded the timeout of 60 seconds.** It might mean GitHub or Packagist is unavailable at the moment. This usually doesn't last for more than a few minutes, so you can run ```php artisan backpack:install --timeout=600``` to increase the timeout to 10 minutes. If this doesn't work either, take a look behind the scenes with ```php artisan backpack:install --timeout=600 --debug```;

- **Error: SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long**. Your MySQL version might be a bit old. Please [apply this quick fix](https://laravel-news.com/laravel-5-4-key-too-long-error), then run ```php artisan migrate:fresh```.

- **Any other installation error?** If you can't install Backpack because of a different error, you can [try the manual installation process](/docs/{{version}}/crud-how-to#manually-install-backpack), which you can tweak to your needs.

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 2000 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the Laravel [Patreon page](https://patreon.com/taylorotwell).

### Premium Partners

- **[Vehikl](https://vehikl.com/)**
- **[Tighten Co.](https://tighten.co)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Cubet Techno Labs](https://cubettech.com)**
- **[Cyber-Duck](https://cyber-duck.co.uk)**
- **[Many](https://www.many.co.uk)**
- **[Webdock, Fast VPS Hosting](https://www.webdock.io/en)**
- **[DevSquad](https://devsquad.com)**
- **[Curotec](https://www.curotec.com/services/technologies/laravel/)**
- **[OP.GG](https://op.gg)**
- **[WebReinvent](https://webreinvent.com/?utm_source=laravel&utm_medium=github&utm_campaign=patreon-sponsors)**
- **[Lendio](https://lendio.com)**

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

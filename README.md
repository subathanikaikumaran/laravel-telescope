# laravel-telescope
> Telescope is a debugging tool which is a combination of different watchers for incoming requests on your application such as HTTP Request,Command Line Requests, Scheduler or Queue.Laravel telescope introduced in the latest Laravel version which is 5.7 and requires 
a minimum of Laravel 5.7.7 to work.Telescope provides insight into the requests coming into your application, exceptions, log entries, database queries, queued jobs, mail, notifications, cache operations, scheduled tasks, dumps and ect. '/telescope'is the path within your application which will allow you to access telescope. The default value is /telescope. Telescope will store the data into database by default. This will determine which database connection to use. It will use your default database connection.

## Installation
To begin create a new Laravel project

```composer create-project --prefer-dist laravel/laravel Laravel-telescope```

Edit your database data in .env file.
```
DB_DATABASE=dbtelescope
DB_USERNAME=<your database username>
DB_PASSWORD=<your database password>
```

##### Install telescope in your laravel project
```composer require laravel/telescope --dev``` then 
```php artisan telescope:install```

Once you installed telescope in your project, run migrate command.

```php artisan migrate```

'telescope_monitoring', 'telescope_entries_tags' and 'telescope_entries' tables will your database.

Now you navigate to telescope page localhost/Laravel-telescope/public/telescope. if it is not working change your \vendor\laravel\telescope\resources\views\layout.blade.php file. And try it will work.
Change these lines <!-- Global Telescope Object -->
```
<script>
   window.Telescope = @json($telescopeScriptVariables);
</script>
```

to this

```
<script>
   window.Telescope = @json($telescopeScriptVariables);
   window.Telescope.path = 'your_project_folder/public/telescope';
</script>
```

> You can setup who has access to Telescope, app/Providers/TelescopeServiceProvider.php and find the gate function.
```
protected function gate()
    {
        Gate::define('viewTelescope', function ($user) {
            $ids = env('TELESCOPE_USERS', '');
            $ids = explode(',', $ids);
            return in_array($user->id, $ids);
        });
    }
```
Add TELESCOPE_USERS=1,2 into your .env file.

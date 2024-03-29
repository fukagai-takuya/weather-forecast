<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

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

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 1500 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

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

# weather-forecast

This code gathers weather forecast information from the following site by using Web API.

https://openweathermap.org/api
(https://api.openweathermap.org/data/2.5/forecast)

# about this program

English Blog Posts

https://www.leafwindow.com/en/create-a-weather-forecast-web-api-with-laravel-en/
https://www.leafwindow.com/en/create-a-weather-forecast-web-api-with-laravel-2-en/
https://www.leafwindow.com/en/create-a-weather-forecast-web-api-with-laravel-3-en/


Japanese Blog Posts

https://www.leafwindow.com/create-a-weather-forecast-web-api-with-laravel/
https://www.leafwindow.com/create-a-weather-forecast-web-api-with-laravel-2/
https://www.leafwindow.com/create-a-weather-forecast-web-api-with-laravel-3/

# setup

1. Prepare vendor directory with the following command

```
$ composer install
```

2. Prepare .env file

- You can use .env.weather-forecast as a reference file.

3. Prepare SQLite file

- Since I used SQLite with php 7.4 on Ubuntu 20.04, I installed sqlite3 and php-sqlite3 with the following command.

```
$ sudo apt install sqlite3
$ sudo apt-get install php7.4-sqlite3
```

- Prepare the empty database file with the following command.

```
$ touch database/database.sqlite
```

- Prepare the database tables with the following command.

```
$ php artisan migrate
```

4. Prepare a crontab setting (It's not required for a simple Web API test.)

- This code collects weather forecasts for New York, London, Paris, Berlin and Tokyo every 6 hours.
- You need to add a single cron configuration entry to your server that runs the schedule:run command every minute.

```
* * * * * cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1
```

# a simple Web API test

1. Start server for a simple test

```
$ php artisan serve
```

2. Access the following address

```
http://localhost:8000/api/get-weather-forecast?date=2022-05-13 10:25:49
```

- The format of the date parameter is 'YYYY-MM-DD HH:mm:ss'.
- An example is '2022-05-13 10:25:49'.
- If you specify a date and time within 5 days of today, you will get the weather information.
- The following is an example of JSON response given by this Web API.

```
{
    "id": "9",
    "dt": "1652432400",
    "dt_txt": "2022-05-13 09:00:00",
    "new_york_main": "Clouds",
    "new_york_description": "overcast clouds",
    "london_main": "Clouds",
    "london_description": "overcast clouds",
    "paris_main": "Clouds",
    "paris_description": "scattered clouds",
    "berlin_main": "Clouds",
    "berlin_description": "broken clouds",
    "tokyo_main": "Rain",
    "tokyo_description": "moderate rain",
    "updated_at": "2022-05-12 06:11:20",
    "created_at": "2022-05-12 06:11:20"
}
```

- First, it tries to retrieve data from the local SQLite server.
- If it fails to retrieve data from the SQLite server, it accesses the following site to collect weather information.
- If the weather information cannot be retrieved from the following site, an error response is returned.

```
https://openweathermap.org/api
(https://api.openweathermap.org/data/2.5/forecast)
```

# test commands

- You can test the codes with the following command.

```
$ php artisan test
```

- You can test task scheduling with the following commands.
```
$ php artisan schedule:run
$ php artisan queue:work
```

- When testing task scheduling, the scheduling method was modified as follows. (app/Console/Kernel.php)
```
protected function schedule(Schedule $schedule)
{
    // $schedule->job(new WeatherForecastInquiryJob)->everySixHours();
    $schedule->job(new WeatherForecastInquiryJob)->everyMinute();
}
```

# other information
- I added or updated the following files on Laravel Framework 8.83.11.
```
.env.weather-forecast
.env.testing
phpunit.xml
routes/api.php
app/Console/Kernel.php
app/Providers/EventServiceProvider.php
app/Http/Controllers/WeatherForecastInquiryController.php
app/Events/WeatherForecastInquiryEvent.php
app/Jobs/WeatherForecastInquiryJob.php
app/Listeners/WeatherForecastInquiryNotification.php
tests/Feature/WeatherForecastInquiryTest.php
database/migrations/2022_05_05_074622_create_jobs_table.php
database/migrations/2022_05_06_013400_weather_data.php
database/database.sqlite
```

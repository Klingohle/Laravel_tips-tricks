# Laravel Tipps & Tricks
## in case Controllers cannot be found 
## error message: on website being called: ~UserController doesn't exist
### solution: adjust App->Providers->RouteServiceProvider.php:
#### 


```

    public const HOME = '/home';
    // add this line
    protected $namespace = "App\Http\Controllers";   

    public function boot()
    {
        $this->configureRateLimiting();

        $this->routes(function () {
            Route::middleware('api')
                ->prefix('api')
                ->group(base_path('routes/api.php'));

            Route::middleware('web')
            // add this line
                ->namespace($this->namespace)
                ->group(base_path('routes/web.php'));
        });
    }
```

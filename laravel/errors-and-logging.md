# Logging

### 建立Log

**app/Http/Controllers**

```
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

use App\Http\Requests;

class UserController extends Controller
{
    /**
     * 顯示給定使用者的個人資料。
     *
     * @param  int  $id
     * @return Response
     */
    public function showProfile($id)
    {
        Log::info('Showing user profile for user: '.$id);

        return view('user.profile', ['user' => User::findOrFail($id)]);
    }
}
```

**打印出Log在terminal，並執行php artisan serve**

```
tail -f storage/logs/laravel.log & sudo php artisan serve
```

### Log類型

```
Log::emergency($error);
Log::alert($error);
Log::critical($error);
Log::error($error);
Log::warning($error);
Log::notice($error);
Log::info($error);
Log::debug($error);
```

**config/app.php**

統一指定紀錄Log訊息到storage/logs/laravel.log

```
'log'=> env('APP_LOG','single'),
```

每日依照年月日不同，指定紀錄Log訊息到storage/logs/laravel-yyyy-mm-dd.log

```
'log'=> env('APP_LOG','daily'),
```

# Errors

### Try&Catch

```
use Exception;
use Log;

try {
        var_dump($val);
    } catch (\Exception $e) {
        throw $e;
    }
```

### 回傳客製Errors回應

```
return parent::render($request, $e);
```

### 回傳客製Http例外

```
return abort(403, 'Unauthorized action.');
```

### 回傳客製Errors Html樣板

```
return response()->view('errors.503', [], 503);
```

 


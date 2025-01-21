
```
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
```
```
composer global require laravel/installer
```
```
laravel new example-app
```
mariaDB

### .env
```
DB_CONNECTION=mariadb
DB_HOST=127.0.0.1
DB_PORT=8306
DB_DATABASE=mydatabase
DB_USERNAME=root
DB_PASSWORD=root
```

## api install
```
php artisan install:api
```

## make model
```
php artisan make:model nmModul -m
```

## NM
```php
Schema::create('nm_moduls', function (Blueprint $table) {

            $table->id();

            $table->foreignId('modulID')->constrained('moduluak')->onDelete('cascade');

            $table->foreignId('userID')->constrained('users')->onDelete('cascade');

            $table->timestamps();

        });
```

## User nm
```php
public function modulos()

    {

        return $this->belongsToMany(Moduluak::class, 'nm_moduls', 'userID', 'modulID');

    }
```

## Moduluak nm
```php
 public function users()

    {

        return $this->belongsToMany(Moduluak::class, 'nm_moduls', 'modulID', 'userID');

    }
```

## Users model
```php
use Laravel\Sanctum\HasApiTokens;  // Asegúrate de tener esta línea   
use HasFactory, Notifiable, HasApiTokens;
```

## Crear usuario
```php
public function createUser(Request $request)

    {

  

        $validator = Validator::make($request->all(), [

            'izena' => 'required|string|max:255',

            'email' => 'required|email|unique:users',

            'password' => 'required|string|min:6',  

        ]);

  

        // Si la validación falla, devolver un 400 Bad Request

        if ($validator->fails()) {

            return response()->json([

                'message' => 'Datos incorrectos o incompletos.',

                'errors' => $validator->errors()

            ], 400); // 400 Bad Request

        }

  

        try {

            $user = User::create([

                'name' => $request->izena,

                'email' => $request->email,

                'password' => Hash::make($request->password),

            ]);

  

            return response()->json([

                'message' => 'Usuario creado exitosamente',

                'user' => $user,

            ], 201); // 201 Created

  

        } catch (\Exception $e) {

            // En caso de error inesperado (ej. problemas con la base de datos)

            return response()->json([

                'message' => 'Ocurrió un error al crear el usuario.',

                'error' => $e->getMessage(),

            ], 500); // 500 Internal Server Error

        }

  

    }
```
## Saioa asi
```php
public function loging(Request $request)

    {

  

        $validator = Validator::make($request->all(), [

            'email' => 'required|email',

            'password' => 'required|string|min:6',  

        ]);

  

        // Si la validación falla, devolver un 400 Bad Request

        if ($validator->fails()) {

            return response()->json([

                'message' => 'Datos incorrectos o incompletos.',

                'errors' => $validator->errors()

            ], 400); // 400 Bad Request

        }

  

        $user = User::where('email', $request->email)->first();

  

        if (!$user || !Hash::check($request->password, $user->password)) {

            return response()->json([

                'error' => 'Las credenciales proporcionadas son incorrectas.',

            ], 401);

        }

  

        $token = $user->createToken(64)->plainTextToken;

  
  

        return response()->json([

            'user' => $user,

                'token' => $token

            ]);

  
  

    }
```
## Delete sesion
```php
public function logOut(Request $request)

    {

  

        $user = Auth::user();

        if (!$user) {

            return response()->json(['message' => 'No autenticado'], 401);

        }

  

        $user->tokens()->delete(); // Revoca todos los tokens del usuario

        return response()->json(['message' => 'Sesión cerrada correctamente']);

  

    }
```
## Up a server
```bash
php artisan serve --host=0.0.0.0 --port=8000
```

## NM select
```php
 $idUser = $user->id;

        $moduluakID = \App\Models\nmModul::where('userID', $idUser)->get()->pluck('modulID');;

  

        $moduluak = \App\Models\moduluak::whereIn('id', $moduluakID)->get();
```

## API 
```php
Route::get('/matrikulatutako-moduluak', 'App\Http\Controllers\ModuluakController@matrikulatutakoModuluak')->middleware('auth:sanctum');
```

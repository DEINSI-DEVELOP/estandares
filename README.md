# Estándares

# Estándares PSR

## PSR-12

Esta especificación amplía, expande y sustituye a PSR-2, la guía de estilo de codificación, y exige el cumplimiento de PSR-1, la norma básica de codificación.

Al igual que PSR-2, la intención de esta especificación es reducir la fricción cognitiva al escanear código de diferentes autores. Lo hace enumerando un conjunto compartido de reglas y expectativas sobre cómo formatear el código PHP. Esta PSR busca proporcionar un conjunto de formas que las herramientas de estilo de codificación puedan implementar, los proyectos puedan declarar su adhesión y los desarrolladores puedan relacionar fácilmente entre diferentes proyectos. Cuando varios autores colaboran a través de múltiples proyectos, ayuda tener un conjunto de directrices para ser usadas entre todos esos proyectos.

La PSR-2 fue aceptada en 2012 y, desde entonces, se han introducido una serie de cambios en PHP que repercuten en las directrices de estilo de codificación. Mientras que la PSR-2 es muy completa en cuanto a la funcionalidad de PHP que existía en el momento de su redacción, la nueva funcionalidad está muy abierta a la interpretación. Esta PSR, por lo tanto, pretende aclarar el contenido de la PSR-2 en un contexto más moderno con la nueva funcionalidad disponible, y hacer que la fe de erratas de la PSR-2 sea vinculante.

Ejemplo
Este ejemplo engloba algunas de las reglas que figuran a continuación a modo de resumen rápido:

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction(int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

> 2.1 Norma básica de codificación
> 

El código DEBE seguir todas las reglas descritas en PSR-1.

El término 'StudlyCaps' en PSR-1 DEBE interpretarse como PascalCase donde la primera letra de cada palabra se escribe en mayúscula, incluyendo la primera letra.

> 2.2 Archivos
> 

Todos los archivos PHP DEBEN usar únicamente el final de línea Unix LF (salto de línea).

Todos los archivos PHP DEBEN terminar con una línea que no esté en blanco, terminada con una sola LF.

La etiqueta de cierre ?> DEBE ser omitida en archivos que contengan únicamente PHP.

> 2.3 Líneas
> 

NO DEBE haber un límite duro en la longitud de las líneas.

El límite blando de longitud de línea DEBE ser de 120 caracteres.

Las líneas NO DEBEN ser más largas de 80 caracteres; las líneas más largas DEBEN ser divididas en múltiples líneas subsecuentes de no más de 80 caracteres cada una.

NO DEBE haber espacios en blanco al final de las líneas.

Pueden añadirse líneas en blanco para mejorar la legibilidad y para indicar bloques de código relacionados, excepto cuando esté explícitamente prohibido.

NO DEBE haber más de una sentencia por línea.

> 2.4 Sangría
> 

El código DEBE usar una sangría de 4 espacios por cada nivel de sangría, y NO DEBE usar tabuladores para sangrar.

2.5 Palabras clave y tipos

Todas las palabras clave y tipos reservados de PHP [1][2] DEBEN estar en minúsculas.

Cualquier nuevo tipo y palabra clave añadida a futuras versiones de PHP DEBE estar en minúsculas.

Se DEBE usar la forma corta de las palabras clave de tipo, p.e. bool en lugar de boolean, int en lugar de integer, etc.

# Estándares de nombramiento en laravel

| Clases | Convención | Ejemplo |
| --- | --- | --- |
| Controller | singular | ArticleController |
| Route | plural | articles/1 |
| Named route | snake_case with dot notation | users.show_active |
| Model | singular | User |
| hasOne or belongsTo relationship | singular | articleComment |
| All other relationships | plural | articleComments |
| Table | plural | article_comments |
| Pivot table | singular model names in alphabetical order | article_user |
| Table column | snake_case without model name | meta_title |
| Foreign key | singular model name with _id suffix | article_id |
| Primary key | - | id |
| Migration | - | 2017_01_01_000000_create_articles_table |
| Method | camelCase | getAll |
| Function | snake_case | abort_if |
| Method in resource controller | more infos: table | store |
| Method in test class | camelCase | testGuestCannotSeeArticle |
| Model property | snake_case | $model->model_property |
| Variable | camelCase | $anyOtherVariable |
| Collection | descriptive, plural | $activeUsers = User::active()->get() |
| Object | descriptive, singular | $activeUser = User::active()->first() |
| Config and language files index | snake_case | articles_enabled |
| View | kebab-case | show-filtered.blade.php |
| Config | kebab-case | google-calendar.php |
| Contract (interface) | adjective or noun | Authenticatable |
| Trait | adjective | Notifiable |

# Siempre que sea posible, utilice una sintaxis más corta y legible.

| Sintáxis Común | Sintaxis más corta y legible |
| --- | --- |
| Session::get('cart') | session('cart') |
| $request->session()->get('cart') | session('cart') |
| Session::put('cart', $data) | session(['cart' => $data]) |
| $request->input('name'), Request::get('name') | $request->name, request('name') |
| return Redirect::back() | return back() |
| is_null($object->relation) ? $object->relation->id :                             null                             } | optional($object->relation)->id |
| return view('index')->with('title', $title)->with('client',                             $client) | return view('index', compact('title', 'client')) |
| $request->has('value') ? $request->value :                             'default'; | $request->get('value', 'default') |
| Carbon::now(), Carbon::today() | now(), today() |
| App::make('Class') | app('Class') |
| ->where('column', '=', 1) | ->where('column', 1) |
| ->orderBy('created_at', 'desc') | ->latest() |
| ->orderBy('age', 'desc') | ->latest('age') |
| ->orderBy('created_at', 'asc') | ->oldest() |
| ->select('id', 'name')->get() | ->get(['id', 'name']) |
| ->first()->name | ->value('name') |

# Principio de responsabilidad única

Principio de responsabilidad única es un principio de programación que indica que una clase y un método deben tener una sola responsabilidad. Esto significa que cada clase y método debe tener una única tarea o responsabilidad y no debe tener más de una razón para cambiar.

Este principio se aplica en Laravel a través de la separación de responsabilidades en las diferentes capas de la arquitectura del framework. Por ejemplo, los modelos son responsables de interactuar con la base de datos, los controladores son responsables de manejar las solicitudes HTTP y las vistas son responsables de mostrar la información al usuario final.

Siguiendo el principio de responsabilidad única, es más fácil mantener y escalar una aplicación ya que cada componente es responsable de una única tarea y no tiene dependencias innecesarias. Esto también facilita la reutilización del código ya que las clases y métodos se pueden utilizar en diferentes partes de la aplicación sin tener que modificarlos.

## Una clase y un método deben tener una sola responsabilidad.

### Ejemplo `INCORRECTO`

```php
public function getFullNameAttribute()
    {
        if (auth()->user() && auth()->user()->hasRole('client') && auth()->user()->isVerified()) {
            return 'Mr. ' . $this->first_name . ' ' . $this->middle_name . ' ' . $this->last_name;
        } else {
            return $this->first_name[0] . '. ' . $this->last_name;
        }
    }
```

### Ejemplo `CORRECTO`

```php
public function getFullNameAttribute()
    {
        return $this->isVerifiedClient() ? $this->getFullNameLong() : $this->getFullNameShort();
    }

    public function isVerifiedClient()
    {
        return auth()->user() && auth()->user()->hasRole('client') && auth()->user()->isVerified();
    }

    public function getFullNameLong()
    {
        return 'Mr. ' . $this->first_name . ' ' . $this->middle_name . ' ' . $this->last_name;
    }

    public function getFullNameShort()
    {
        return $this->first_name[0] . '. ' . $this->last_name;
    }
```

# Modelos robustos, controladores débiles

Pon toda la lógica relacionada con la BD en modelos Eloquent o en clases Repositorio si estás usando Query Builder o consultas SQL sin procesar.

### Ejemplo `INCORRECTO`

```php
public function index()
    {
        $clients = Client::verified()
            ->with(['orders' => function ($q) {
                $q->where('created_at', '>', Carbon::today()->subWeek());
            }])
            ->get();

        return view('index', ['clients' => $clients]);
    }
```

### Ejemplo `CORRECTO`

```php
public function index()
    {
        return view('index', ['clients' => $this->client->getWithNewOrders()]);
    }

    class Client extends Model
    {
        public function getWithNewOrders()
        {
            return $this->verified()
                ->with(['orders' => function ($q) {
                    $q->where('created_at', '>', Carbon::today()->subWeek());
                }])
                ->get();
        }
    }
```

# Validación

Trasladar la validación de los controladores a las clases Request.

### Ejemplo `INCORRECTO`

```php
public function store(Request $request)
    {
        $request->validate([
            'title' => 'required|unique:posts|max:255',
            'body' => 'required',
            'publish_at' => 'nullable|date',
        ]);

        ....
    }
```

### Ejemplo `CORRECTO`

```php
public function store(PostRequest $request)
    {
        ....
    }

    class PostRequest extends Request
    {
        public function rules()
        {
            return [
                'title' => 'required|unique:posts|max:255',
                'body' => 'required',
                'publish_at' => 'nullable|date',
            ];
        }
    }
```

# La lógica empresarial debe estar en la clase de servicio

Un controlador debe tener una sola responsabilidad, así que mueve la lógica de negocio de los controladores a las clases de servicio.

### Ejemplo `INCORRECTO`

```php
public function store(Request $request)
    {
        if ($request->hasFile('image')) {
            $request->file('image')->move(public_path('images') . 'temp');
        }

        ....
    }
```

### Ejemplo `CORRECTO`

```php
public function store(Request $request)
    {
        $this->articleService->handleUploadedImage($request->file('image'));

        ....
    }

    class ArticleService
    {
        public function handleUploadedImage($image)
        {
            if (!is_null($image)) {
                $image->move(public_path('images') . 'temp');
            }
        }
    }
```

# No repetir código

Reutiliza el código siempre que puedas. SRP te ayuda a evitar la duplicación. Además, reutiliza las plantillas de Blade, usa los ámbitos de Eloquent, etc.

### Ejemplo `INCORRECTO`

```php
public function getActive()
    {
        return $this->where('verified', 1)->whereNotNull('deleted_at')->get();
    }

    public function getArticles()
    {
        return $this->whereHas('user', function ($q) {
                $q->where('verified', 1)->whereNotNull('deleted_at');
            })->get();
    }
```

### Ejemplo `CORRECTO`

```php
public function scopeActive($q)
    {
        return $q->where('verified', 1)->whereNotNull('deleted_at');
    }

    public function getActive()
    {
        return $this->active()->get();
    }

    public function getArticles()
    {
        return $this->whereHas('user', function ($q) {
                $q->active();
            })->get();
    }
```

# Utilizar Eloquent en lugar de Query Builder y consultas SQL sin procesar. Usar primero las colecciones a las matrices

Eloquent permite escribir código legible y fácil de mantener. Además, Eloquent tiene grandes herramientas integradas como soft deletes, events, scopes etc.

### Ejemplo `INCORRECTO`

```sql
SELECT *
    FROM `articles`
    WHERE EXISTS (SELECT *
                  FROM `users`
                  WHERE `articles`.`user_id` = `users`.`id`
                  AND EXISTS (SELECT *
                              FROM `profiles`
                              WHERE `profiles`.`user_id` = `users`.`id`)
                  AND `users`.`deleted_at` IS NULL)
    AND `verified` = '1'
    AND `active` = '1'
    ORDER BY `created_at` DESC
```

### Ejemplo `CORRECTO`

```php
Article::has('user.profile')->verified()->latest()->get();
```

# Asignación masiva

### Ejemplo `INCORRECTO`

```php
$article = new Article;
$article->title = $request->title;
$article->content = $request->content;
$article->verified = $request->verified;
// Add category to article
$article->category_id = $category->id;
$article->save();
```

### Ejemplo `CORRECTO`

```php
$category->article()->create($request->all());
```

# No ejecutar consultas en plantillas Blade y utilizar eager loading (problema N + 1)

### `INCORRECTO`(para 100 usuarios, se ejecutarán 101 consultas a la base de datos):

```php
@foreach (User::all() as $user)

    @endforeach
```

### `CORRECTO` (para 100 usuarios, se ejecutarán 2 consultas a la base de datos):

```php
$users = User::with('profile')->get();

    ...

    @foreach ($users as $user)

    @endforeach
```

# El código se comenta usando nombres descriptivos de métodos y variables a los comentarios.

### `INCORRECTO`

```php
if (count((array) $builder->getQuery()->joins) > 0)
```

### `ACEPTABLE`

```php
// Determine if there are any joins.
    if (count((array) $builder->getQuery()->joins) > 0)
```

### `CORRECTO`

```php
if ($this->hasJoins())
```

# No poner código JS y CSS en las plantillas Blade y no ponga HTML en las clases PHP.

### `INCORRECTO`

```jsx
let article = ``;
```

### `ACEPTABLE`

```html
<input id="article" type="hidden" value="">

    Or

    <button class="js-fav-article" data-article=""><button>
```

### `CORRECTO`

```jsx
let article = $('#article').val();
```

La mejor manera es utilizar el paquete especializado PHP a JS para transferir los datos.

# `(Debería)`Utilizar archivos de configuración y de idioma, constantes en lugar de texto en el código.

### `INCORRECTO`

```php
public function isNormal()
    {
        return $article->type === 'normal';
    }

    return back()->with('message', 'Your article has been added!');
```

### `CORRECTO`

```php
public function isNormal()
    {
        return $article->type === Article::TYPE_NORMAL;
    }

    return back()->with('message', __('app.article_added'));
```

# Utilizar herramientas Laravel estándar aceptadas por la comunidad

| Tarea | Herramientas estandar | Herramientas de terceros |
| --- | --- | --- |
| Authorization | Policies | Entrust, Sentinel and other packages |
| Compiling assets | Laravel Mix | Grunt, Gulp, 3rd party packages |
| Development Environment | Homestead | Docker |
| Deployment | Laravel Forge | Deployer and other solutions |
| Unit testing | PHPUnit, Mockery | Phpspec |
| Browser testing | Laravel Dusk | Codeception |
| DB | Eloquent | SQL, Doctrine |
| Templates | Blade | Twig |
| Working with data | Laravel collections | Arrays |
| Form validation | Request classes | 3rd party packages, validation in controller |
| Authentication | Built-in | 3rd party packages, your own solution |
| API authentication | Laravel Passport | 3rd party JWT and OAuth packages |
| Creating API | Built-in | Dingo API and similar packages |
| Working with DB structure | Migrations | Working with DB structure directly |
| Localization | Built-in | 3rd party packages |
| Realtime user interfaces | Laravel Echo, Pusher | 3rd party packages and working with WebSockets directly |
| Generating testing data | Seeder classes, Model Factories, Faker | Creating testing data manually |
| Task scheduling | Laravel Task Scheduler | Scripts and 3rd party packages |
| DB | MySQL, PostgreSQL, SQLite, SQL Server | MongoDB |

# No obtener directamente los datos del archivo ".env

Pasar los datos a los archivos de configuración en su lugar y luego utilizar la función de ayuda config() para utilizar los datos en una aplicación.

### `INCORRECTO`

```php
$apiKey = env('API_KEY');
```

### `CORRECTO`

```php
// config/api.php
    'key' => env('API_KEY'),

    // Use the data
    $apiKey = config('api.key');
```
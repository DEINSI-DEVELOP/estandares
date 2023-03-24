# Estándares

# Estándares PSR

## PSR-4

Laravel utiliza el estándar PSR-4 para la carga automática de clases. Este estándar define la estructura de directorios y nombres de archivos para las clases de PHP. En Laravel, todas las clases deben estar en el espacio de nombres `App` y deben estar en el directorio `app/`. Además, la estructura de archivos debe reflejar la estructura de los espacios de nombres.

## PSR-2

Laravel también sigue el estándar PSR-2 para el estilo de codificación. Este estándar define reglas para la indentación, el uso de espacios en blanco, las líneas en blanco, las llaves y otros elementos del código. En Laravel, las reglas de PSR-2 se aplican a todo el código, incluyendo el núcleo del framework y las aplicaciones desarrolladas con Laravel.

## PHPDoc

Laravel utiliza PHPDoc para documentar el código. PHPDoc es un formato de comentarios para documentar el código PHP. Laravel utiliza PHPDoc para documentar las clases, los métodos y las propiedades. Las etiquetas de PHPDoc se utilizan para documentar los tipos de datos, las descripciones y otros elementos del código.

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

### Ejemplo de lo que `NO DEBES HACER`

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

### Ejemplo de lo que `SI DEBES HACER`

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

### Ejemplo de lo que `NO DEBES HACER`

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

### Ejemplo de lo que `SI DEBES HACER`

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

### Ejemplo de lo que `NO DEBES HACER`

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

### Ejemplo de lo que `SI DEBES HACER`

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

### Ejemplo de lo que `NO DEBES HACER`

```php
public function store(Request $request)
    {
        if ($request->hasFile('image')) {
            $request->file('image')->move(public_path('images') . 'temp');
        }

        ....
    }
```

### Ejemplo de lo que `SI DEBES HACER`

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
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
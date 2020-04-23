# Rotas e URLs amigáveis

**Notas importantes**

- Por padrão nenhum arquivo **HTML** ou **PHP** é possivel ser acessado diretamente, se você tentar acessar retornara um erro 404.
- Todos as arquivos devem estar dentro da pasta `public`.
- Extensões válidas para os arquivos são `.php` e `.blade.php`.
- Métodos aceitos são: **GET**, **POST**, **PUT**, **PATCH** e **DELETE**.

## URLs amigáveis

Não é necessário definir uma rota para acessar uma view.

Quando você acessar a URL `/home`, o motor do framework ira buscar o arquivo `home` na pasta `public`.

Caso tente acessar `/admin/home`, é o equivalente a `public/admin/home`.

## Index

Num servidor apache todos sabemos que por padrão é buscado pelo arquivo `index.html` ou `index.php`.

No Attla isso não é diferente, caso não for definido um index, o motor do framework ira buscar pelo arquivo `index` dentro da pasta `public`.

Definindo um index pelo arquivo `config.json`

```json
{
	"routes": {
		"index": "welcome"
	}
}
```

## Exclusão de rotas

É comum que existam arquivos que não devem ser acessados aparte, como um header ou footer, ou até  mesmo um template. Por esse motivo você pode optar por excluir a rota, assim retornando um erro 404 caso seja acessado via URL.

Excluindo rotas pelo arquivo `config.json`

```json
{
	"routes": {
		"exclude_routes":[
			"error",
			"header",
			"footer"
		],
	}
}
```

## Definindo rotas

Existem 2 meios de manipular as rotas do seu site.

Pelo arquivo `config.json`

```json
{
	"routes": {
		"GET":[
			"/home",
			"/blog"
		]
	}
}
```

ou pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->get('/home', function(){
	echo "<h1>home</h1>";
});

$app->run();
```

## Nomeclatura de rotas

Ja reparou o quão complicado é ter que trocar uma URL em uma aplicação de médio a grande porte ?

Por isso é recomendado que sua aplicação não conheça as URLs e manipule as rotas unicamente pelos seus nomes.

Mas como fazemos isso ? Simples..

Pelo arquivo `config.json`

!> Note que ao invés de um array é passado um objeto

```json
{
	"routes": {
		"GET":{
			"home": "/home",
			"blog": "/blog"
		},
		"POST":{
			"login": "/login"
		}
	}
}
```

ou pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->get('/blog', function(){
	echo '<h1>Blog</h1>';
})->setName('blog');

$app->post('/login', function(){
	echo '<h1>Login</h1>';
})->name('login');

$app->run();
```

E para recuperar a URL de uma rota é usado a função `route()`.

```html
<a href="<?= route('blog') ?>">Ir para o blog</a>
```

## Parâmetros de rota

É comun você precisar recuperar valores da URL durante sua aplicação. Por esse motivo quando definir uma rota, é possivel definir valores que seram convertidos em variaveis. Entenda no exemplo abaixo:

Pelo arquivo `config.json`

```json
{
	"routes": {
		"GET":{
			"blog.artigo": "/artigo/:id",
			"blog.autor": "/blog/autor/:id/:nome"
		}
	}
}
```
No arquivo `artigo` voce pode recuperar o valor chamando a variável `$id`.

Tudo que não for variável é convertido em path, ou seja `/blog/autor/:id/:nome` é o equivalente a `public/blog/autor`.

Pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->get('/artigo/:id', function($id){
	echo "<h1>Artigo $id</h1>";
})->name('blog.artigo');

$app->get('/blog/autor/:id/:nome', function($id, $nome){
	echo "<h1>Autor $id, $nome</h1>";
})->name('blog.autor');

$app->run();
```

## Restrições de parâmetros com expressões regulares

Você pode restringir o formato dos seus parâmetros de rota usando o método `where` em uma instância de rota. O método `where` aceita o nome do parâmetro e uma expressão regular que define como o parâmetro deve ser restringido.

Pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->get('/artigo/:id', function($id){
	echo "<h1>Artigo $id</h1>";
})->where('id', '[0-9]+')->name('blog.artigo');

$app->get('/blog/autor/:id/:nome', function($id, $nome){
	echo "<h1>Autor $id, $nome</h1>";
})->where(['id' => '[0-9]+', 'nome' => '[a-z\-]+'])->name('blog.autor');

$app->run();
```

Se a rota nomeada conter parâmetros, você poderá passar os parâmetros como o segundo argumento para a função `route()`. Os parâmetros fornecidos serão automaticamente inseridos na URL em suas posições corretas.

```php
$artigo_url = route('blog.artigo', ['id' => 123]);

$autor_url = route('blog.autor', ['id' => 42, 'nome' => 'lucas-nicolau']);
```

## Parâmetros fantasma

Ao definir uma rota `/autor`, e acessando `/autor/42/lucas-nicolau` ainda caira na rota `/autor` pois o framework compara o inicio da URL com a rota. O restante da URL é convertido em array numérico. Veja como recuperar esses parâmetros fantasma abaixo.

```php
$id = $_GET[0]; // 42

$author_name = $_GET[1]; // lucas-nicolau
```

Tenha em mente que esse método so funciona se houver uma rota definida que seja compatível com o inicio da URL.

## Agrupamento de rotas

Conforme sua aplicação for crescendo é normal ter varias rotas com o mesmo prefixo por exemplo `/admin`. Entenda no exemplo abaixo como agrupar rotas por um prefixo.

Pelo arquivo `config.json`

```json
{
	"routes": {
		"/admin":{
			"index": "/dashboard",
			"GET":{
				"admin.dashboard": "/dashboard",
				"admin.user": "/user"
			},
			"POST":{
				"admin.login": "/login",
			}
		}
	}
}
```

A posição `index` define o arquivo padrão que sera chamado ao acessar `/admin`.

Pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->group('/admin', function() use ($app){
	$app->get('/dashboard', function(){
		echo '<h1>Dashboard</h1>';
	})->name('admin.dashboard');

	$app->get('/user', function(){
		echo '<h1>Login</h1>';
	})->name('admin.user');

	$app->post('/login', function(){
		echo '<h1>Login</h1>';
	})->name('admin.login');
});

$app->run();
```

## Rotas globais

Possa ser que tenha rotas do seu site que precisem ser acessadas tanto via **GET** ou **POST** como por exemplo uma página de login.

Assim você pode definir uma rota e não se preocupar por qual método sera acessado.

Pelo arquivo `config.json`

```json
{
	"routes": {
		"GLOBAL":{
			"site.login": "/login",
			"site.cadastro": "/cadastro"
		}
	}
}
```

Pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->global('/login', function(){
	echo "<h1>Login</h1>";
})->name('site.login');

$app->run();
```

Qualquer uma dessas chaves [ **GLOBAL**, **GLOBALS**, **REQUEST** ] podem ser usadas pra definir uma rota global.

## Falsificando método de formulário

Os formulários HTML não suportam ações **PUT**, **PATCH** ou **DELETE**. Portanto, ao definir rotas **PUT**, **PATCH** ou **DELETE** chamadas a partir de um formulário HTML, você precisará adicionar um campo `_method` oculto ao formulário. O valor enviado com o campo `_method` será usado como o método de solicitação HTTP.

```html
<form action="/foo/bar" method="POST">
	<input type="hidden" name="_method" value="PUT">
</form>
```

Você pode usar a diretiva `@method` Blade para gerar a entrada `_method`.

```html
<form action="/foo/bar" method="POST">
    @method('PUT')
</form>
```

## View Routes

Como você ja deve ter reparado que no arquivo `config.json` as rotas são orientadas a views. Porem esse recurso não é exclusivo do arquivo `config.json`.

Pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->get('/blog/artigo/:id', 'blog/artigo')->name('blog.artigo');

$app->run();
```

## Controladores de rota

O Attla não utiliza MVC por padrão, porem você pode utilizar controladores ao invez de um Closure.

Pelo arquivo `index.php`

```php
$app = new Attla\App();

$app->get('/blog', 'blogControler:index')->name('blog');

$app->run();
```

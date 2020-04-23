# Helpers

Lista de funções que podem lhe auxiliar durante o desenvolvimento da sua aplicação.

| Método | Parâmetros | Descrição |
| - | - | - |
[dd($var)](#dd) | Mixed | Equivalente ao `dd()` do laravel. É um `var_dump()` mais estilizado
[config()](#config) | - | Retorna um objeto com as configurações da aplicação
[route($routeName, $params)](#route) | String, Array | Retorna a URL da rota pelo nome
[redirect($url)](#redirect) | String | Faz um redirecionamento
[get($key)](#get) | String | Retorna um valor da variável `$_GET`
[post($key)](#post) | String | Retorna um valor da variável `$_POST`
[input($key)](#input) | String | Retorna um valor da variável `$_REQUEST`
[name($name)](#name) | String | Retorna o nome e sobrenome a partir do nome completo
[year()](#year) | - | Retorna o ano no formato 2018 - 2020 a partir do ano no `config.json`
[uri($location)](#uri) | String | Retorna a URL da aplicação
[url($location)](#url) | String | Alias de `uri()`
[assets($file)](#assets) | String | Retorna o caminho absoluto apontando para a pasta `assets`
[asset($file)](#asset) | String | Alias de `assets()`
[set_global($key, $val)](#set_global) | String or Array, Mixed | Define uma variável globalmente
[set_globals($key, $val)](#set_globals) | String or Array, Mixed | Alias de `set_global()`
[get_global($key)](#get_global) | String | Retorna o valor de uma variável global
[get_globals($key)](#get_globals) | String | Alias de `get_global()`
[get_header($title, $description, $path)](#get_header) | String, String, String | Inclui o arquivo `header` com a extensão `.php` ou `.blade.php` com acesso a todas as variáveis globais
[page_header($title, $description, $path)](#page_header) | String, String, String | Alias de `get_header()`
[get_footer($path)](#get_footer) | String | Inclui o arquivo `footer` com a extensão `.php` ou `.blade.php` com acesso a todas as variáveis globais
[page_footer($path)](#page_footer) | String | Alias de `get_footer()`
[import($file)](#import) | String | Inclui um arquivo, seja ele com a extensão `.php` ou `.blade.php`, com acesso a todas as variáveis globais
[is_ajax()](#is_ajax) | - | Verifica se é uma requisição AJAX
[is_browser($key)](#is_browser) | String | Verifica se a requisição foi feita por um browser
[browser()](#browser) | - | Retorna o nome do browser
[browser_version()](#browser_version) | - | Retorna a versão do browser
[is_mobile($key)](#is_mobile) | String | Verifica se a requisição foi feita por um dispositivo mobile
[mobile()](#mobile) | - | Retorna o nome do dispositivo mobile
[is_robot($key)](#is_robot) | String | Verifica se a requisição foi feita por um bot
[robot()](#robot) | - | Retorna o nome do bot
[is_referral()](#is_referral) | - | Verifica se a requisição foi originada de outro site
[referrer()](#referrer) | - | Retorna a URL do referrer
[user($key)](#user) | String | Retorna o valor de um índice dos dados de usuário
[new_sign()](#new_sign) | - | Renova a sessão de usuário e retorna os dados
[is_logged()](#is_logged) | - | Verifica se o usuário está logado
[query($query, $bindParams)](#query) | String, Array | Executa uma query, caso houver apenas 1 resultado, somente esse sera retornado
[query_list($query, $bindParams)](#query_list) | String, Array | Executa uma query, e força o retorno de uma lista de arrays com os resultados
[exist($table, $key, $value)](#exist) | String, String, Mixed | Verifica se um registro existe no banco de dados
[array_random($array)](#array_random) | Array | Retorna o mesmo array porem com as posições em ordem embaralhada
[array_random_value($array)](#array_random_value) | Array | Retorna o valor de uma posição do array de forma randômica
[is_empty($val)](#is_empty) | String | Verifica se uma string está vazia
[is_email($email)](#is_email) | String | Verifica se o valor é um email válido
[is_username($username)](#is_username) | String | Verifica se o valor é um username válido
[is_url($url)](#is_url) | String | Verifica se o valor é uma URL válida
[is_name($name)](#is_name) | String | Verifica se o valor é um nome completo
[json($data)](#json) | Mixed | Converte o data em json, exibe depois para a aplicação

### dd()

Equivalente ao `dd()` do laravel. É um `var_dump()` mais estilizado.

```php
dd(['id' => 42, 'email' => 'example@email.com', 'name' => 'Lucas Nicolau']);
```

### config()

Retorna um objeto com as configurações da aplicação.

```php
$version = config()->version;
```

### route()

Retorna a URL da rota pelo nome.

```php
$login_url = route('login');

$edit_user_url = route('edit.user', ['id' => 42]);
```

### redirect()

Faz um redirecionamento.

```php
redirect('/login');

redirect('https://google.com');
```

### get()

Retorna um valor da variável `$_GET`.

```php
$email = get('email');
```

### post()

Retorna um valor da variável `$_POST`.

```php
$email = post('email');
```

### input()

Retorna um valor da variável `$_REQUEST`.

```php
$email = input('email');
```

### name()

Retorna o nome e sobrenome a partir do nome completo.

```php
$name = name('John Smith Doe');
```

### year()

Retorna o ano no formato 2018 - 2020 a partir do ano no `config.json`.

```php
$year = year();
```

### uri()

Retorna a URL da aplicação.

```php
$app_url = uri();

$app_login_url = uri('/login');
```

### url()

Alias de `uri()`.

```php
$app_url = url();

$app_login_url = url('/login');
```

### assets()

Retorna o caminho absoluto apontando para a pasta `assets`.

```php
$style_url = assets('css/style.css');

$mainjs_url = assets('js/main.js');
```

### asset()

Alias de `assets()`.

```php
$style_url = asset('css/style.css');

$mainjs_url = asset('js/main.js');
```

### set_global()

Define uma variável globalmente.

```php
set_global('user', [
	'id' => 42,
	'name' => 'Lucas Nicolau'
]);

// defini varias variáveis ao mesmo tempo
set_global([
	'user' => [
		'id' => 42,
		'name' => 'Lucas Nicolau'
	],
	'is_logged' => true
]);
```

### set_globals()

Alias de `set_global()`.

```php
set_globals('user', [
	'id' => 42,
	'name' => 'Lucas Nicolau'
]);

// defini varias variáveis ao mesmo tempo
set_globals([
	'user' => [
		'id' => 42,
		'name' => 'Lucas Nicolau'
	],
	'is_logged' => true
]);
```

### get_global()

Retorna o valor de uma variável global.

```php
$uri = get_global('uri');
```

### get_globals()

Alias de `get_global`.
```php
$uri = get_globals('uri');
```

### get_header()

Inclui o arquivo `header` com a extensão `.php` ou `.blade.php` com acesso a todas as variáveis globais.

```php
get_header('titulo da página');

// caso o header esteja em um diretório dentro da pasta public ex public/admin/
// você pode passar o terceiro parâmetro sendo o path do diretório
get_header('titulo da página', 'descrição da página', '/admin');
```

### page_header()

Alias de `get_header()`.
```php
page_header('titulo da página');

// caso o header esteja em um diretório dentro da pasta public ex public/admin/
// você pode passar o terceiro parâmetro sendo o path do diretório
page_header('titulo da página', 'descrição da página', '/admin');
```

### get_footer()

Inclui o arquivo `footer` com a extensão `.php` ou `.blade.php` com acesso a todas as variáveis globais.

```php
get_footer();

// caso o footer esteja em um diretório dentro da pasta public ex public/admin/
// você pode passar o path do diretório
get_footer('/admin');
```

### page_footer()

Alias de `get_footer()`.
```php
page_footer();

// caso o footer esteja em um diretório dentro da pasta public ex public/admin/
// você pode passar o path do diretório
page_footer('/admin');
```

### import()

Inclui um arquivo, seja ele com a extensão `.php` ou `.blade.php`, com acesso a todas as variáveis globais.

```php
import('file');

import('admin/dashboard_sidebar');
```

### is_ajax()

Verifica se é uma requisição AJAX.

```php
$is_ajax = is_ajax();
```

### is_browser()

Verifica se a requisição foi feita por um browser.

```php
$is_browser = is_browser();

$is_chrome_browser = is_browser('Chrome');
$is_firefox_browser = is_browser('Firefox');
$is_opera_browser = is_browser('OPR');
```

### browser()

Retorna o nome do browser.

```php
$browser = browser();
```

### browser_version()

Retorna a versão do browser.

```php
$browser_version = browser_version();
```

### is_mobile()

Verifica se a requisição foi feita por um dispositivo mobile.

```php
$is_mobile = is_mobile();

$is_iphone = is_mobile('iphone');
```

### mobile()

Retorna o nome do dispositivo mobile.

```php
$mobile = mobile();
```

### is_robot()

Verifica se a requisição foi feita por um bot.

```php
$is_robot = is_robot();

$is_google_robot = is_robot('googlebot');
$is_yahoo_robot = is_robot('yahoo');
$is_bing_robot = is_robot('bingbot');
```

### robot()

Retorna o nome do bot.

```php
$robot = robot();
```

### is_referral()

Verifica se a requisição foi originada de outro site.

```php
$is_referral = is_referral();
```

### referrer()

Retorna a URL do referrer.

```php
$referrer = referrer();
```

### user()

Retorna o valor de um índice dos dados de usuário.

```php
// todos os dados de usuário
$user_email = user();

// apenas o email
$user_email = user('email');
```

### new_sign()

Renova a sessão de usuário e retorna os dados.

```php
$user_data = new_sign();
```

### is_logged()

Verifica se o usuário está logado.

```php
$is_logged = is_logged();
```

### query()

Executa uma query, caso houver apenas 1 resultado, somente esse sera retornado.

```php
$users = query("SELECT * FROM users"); // Ex: ['id' => 42, 'name' => 'Lucas Nicolau']

// bind params
$users2 = query('SELECT * FROM users WHERE id = :id', ['id' => 42]);
```

### query_list()

Executa uma query, e força o retorno de uma lista de arrays com os resultados.

```php
$users = query_list("SELECT * FROM users"); // Ex: [ ['id' => 42, 'name' => 'Lucas Nicolau'] ]

// bind params
$users2 = query_list('SELECT * FROM users WHERE id = :id', ['id' => 42]);
```

### exist()

Verifica se um registro existe no banco de dados.

```php
$user_exist = exist('users', 'email', 'example@email.com');
```

### array_random()

Retorna o mesmo array porem com as posições em ordem embaralhada.

```php
$array_random = array_random(['id' => 42, 'email' => 'example@email.com', 'name' => 'Lucas Nicolau']);
```

### array_random_value()

Retorna o valor de uma posição do array de forma randômica.

```php
$array_random_value = array_random_value(['id' => 42, 'email' => 'example@email.com', 'name' => 'Lucas Nicolau']);
```

### is_empty()

Verifica se uma string está vazia.

```php
$is_empty = is_empty('test');
```

### is_email()

Verifica se o valor é um email válido.

```php
$valid_email = is_email('example@email.com');

$invalid_email = is_email('example');
```

### is_username()

Verifica se o valor é um username válido.

```php
// ^[a-z\d_.-]{3,20}$
$valid_username = is_username('nicolauns');

$invalid_username = is_username('1');
$invalid_username2 = is_username('example@email.com');
```

### is_url()

Verifica se o valor é uma URL válida.

```php
$valid_url = is_url('https://google.com');

$invalid_url = is_url('google.com');
```

### is_name()

Verifica se o valor é um nome completo.

```php
$valid_name = is_name('Lucas Nicolau');

$invalid_name = is_name('Lucas');
```

### json()

Converte o data em json, exibe depois para a aplicação.

```php
json([
	'id' => 42,
	'email' => 'example@email.com',
	'name' => 'Lucas Nicolau'
]);
```

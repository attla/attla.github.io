# Blade template

O Attla framework utiliza o motor do blade template do laravel. Sendo assim você pode criar uma view com a extensão `.blade.php` e usufruir de quase todas as diretivas padrões.

Então caso não esteja familiarizado com o blade leia a [documentação oficial](https://laravel.com/docs/7.x/blade#introduction).

## Diretivas removidas

Algumas diretivas foram removidas pois são exclusivas do laravel, assim tornando-se inuteis no framework.

- @each
- @inject
- @can
- @elsecan
- @endcan
- @cannot
- @elsecannot
- @endcannot
- @canany
- @elsecanany
- @endcanany
- @error
- @enderror
- @env
- @elseenv
- @endenv
- @unlessenv

## Diretivas exclusivas

Existem algumas diretivas exclusivas do Attla framework que podem lhe auxiliar. Veja abaixo:

### @header

Essa diretiva inclui o arquivo `header` seja ele com a extensão `.php` ou `.blade.php`.

```php
<!-- inclui o header -->

@header('titulo da página')

<!-- caso o header esteja em um diretório dentro da pasta public ex public/admin/ -->
<!-- você pode passar o terceiro parâmetro sendo o path do diretório -->

@header('titulo da página', 'descrição da página', '/admin')
```

No arquivo `header` é possivel acessar o título e descrição pelas variáveis  `$title` e `$description` respectivamente.

### @footer

Inclui o arquivo `footer` com a extensão `.php` ou `.blade.php`.

```php
<!-- inclui o footer -->

@footer()

<!-- caso o footer esteja em um diretório dentro da pasta public ex public/admin/ -->
<!-- você pode passar o path do diretório -->

@footer('/admin')
```

### @assets

Retorna o caminho absoluto até o arquivo.

É recomendado que todos os arquivos de imagem, css, js e afins fiquem dentro da pasta `public/assets/`.

```php
@assets('/css/style.css')

<!-- alias -->

@asset('/js/main.js')
```

### @url

Retorna a URL da aplicação.

```php
@url()

<!-- você pode passar um path de um arquivo ou rota como parâmetro -->

@url('/login')

<!-- alias -->

@uri('/dashboard')
```

### @set_global

Define uma ou mais variáveis como global dentro da aplicação, sendo possível recuperar o valor em qualquer view.

```php
<!-- define uma variável globalmente -->
@set_global('user', [
	'id' => 42,
	'name' => 'Lucas Nicolau'
])

<!-- você também pode definir varias variáveis ao mesmo tempo -->

@set_globals([
	'user' => [
		'id' => 42,
		'name' => 'Lucas Nicolau'
	],
	'is_logged' => true
])
```

### @import

Inclui um arquivo, seja ele com a extensão `.php` ou `.blade.php`, com acesso a todas as variáveis globais.

```php
@import('file')

@import('admin/dashboard_sidebar')
```

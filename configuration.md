# Configurações

Todas as configurações ficam no arquivo `config.json`.

Como a extensão já diz, a estrutura deve obedecer a hierarquia de um objeto JSON válido.

### Consultando dados

Utilize a função `config()` para acessar as configurações do framework.

```php
$version = config()->version;
```

Você pode definir qualquer informação extra no arquivo `config.json` para poder reutilizar durante o projeto.

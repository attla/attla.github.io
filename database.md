# Banco de dados

A configuração da conexão com o banco de dados fica no arquivo `config.json`

```json
{
	"db" : {
		"driver": "mysql",
		"host": "localhost",
		"port": "3306",
		"database": "attla",
		"username": "root",
		"password": ""
	},
}
```

A conexão é feita a partir da biblioteca PDO.

No Attla framework não é utilizado models, então existem funções que auxiliarão na execução de querys ao banco de dados.

```php
// executa uma query, caso houver apenas 1 resultado, somente esse sera retornado
$users = query("SELECT * FROM users"); // Ex: ['id' => 42, 'name' => 'Lucas Nicolau']

// bind params
$users2 = query('SELECT * FROM users WHERE id = :id', ['id' => 42]);

// executa uma query, e força o retorno de uma lista de arrays com os resultados
// recomendado para uso em loops
$users3 = query_list("SELECT * FROM users"); // Ex: [ ['id' => 42, 'name' => 'Lucas Nicolau'] ]

// bind params
$users4 = query_list('SELECT * FROM users WHERE id = :id', ['id' => 42]);
```

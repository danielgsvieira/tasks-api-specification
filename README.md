# API de Lista de Tarefas

## Autenticação (Opcional)
#### POST /auth/register
Request data:
```
{
  name: string,
  username: string,
  password: string
}
```
Response:
Vazia

---

#### POST /auth/login
Request data:
```
{
  username: string,
  password: string
}
```
Response:
```
{
  authToken: string,
  userInfo: {
    name: string,
    username: string
  }
}
```

---

#### GET /auth/user-info
Response:
```
{
  name: string,
  username: string
}
```

---

### Observações gerais para a autenticação
- Verificação do usuário autenticado deve ser feita por meio de um token enviado via header `Authorization`.
- A forma como o token será gerado e como autenticação que será feita internamente fica a critério do desenvolvedor. Basta seguir o padrão de token enviado no header `Authorization` nas requests.
- O campo `username` deve ser único entre os usuários, ou seja, não podem haver dois usuários com o mesmo `username`.

---

## Tarefas

#### GET /tarefas
Response:
```
[
  {
    id: idType,
    titulo: string,
    descricao?: string,
    dataLimite?: dateString,
    dataConclusao?: dateString
  }
]
```
Opcionais:
  - Receber via query params o parâmetro opcional `search` do tipo string. Caso este parâmetro seja enviado, retornar na lista apenas as Tarefas em que o título ou a descrição contenham a string enviada no `search`.

---

#### GET /tarefas/{id}
Response:
```
{
  id: idType,
  titulo: string,
  descricao?: string,
  dataLimite?: dateString,
  dataConclusao?: dateString
}
```

---

#### POST /tarefas
Request data:
```
{
  titulo: string,
  descricao?: string,
  dataLimite?: dateString,
  dataConclusao?: dateString
}
```
Response:
```
{
  id: idType,
  titulo: string,
  descricao?: string,
  dataLimite?: dateString,
  dataConclusao?: dateString
}
```

---

#### PUT /tarefas/{id}
Request data:
```
{
  titulo: string,
  descricao?: string,
  dataLimite?: dateString,
  dataConclusao?: dateString
}
```
Response:
```
{
  id: idType,
  titulo: string,
  descricao?: string,
  dataLimite?: dateString,
  dataConclusao?: dateString
}
```

---

#### DELETE /tarefas/{id}
Response: Vazia

---

#### (Opcional) PATCH /tarefas/{id}/concluir
Conclui a Tarefa adicionando a data atual no atributo `dataConclusao`.

Response:
```
{
  id: idType,
  titulo: string,
  descricao?: string,
  dataLimite?: dateString,
  dataConclusao?: dateString
}
```

---

## Opcionais
  - A autenticação como um todo é um opcional. Não será um problema caso não seja feita. Foi adicionada somente para aumentar o nível de complexidade e não ser simplesmente um CRUD.
  - Permitir que o usuário visualize, edite e delete somente as Tarefas criadas por ele.
  - Campos do tipo `dateString` incluírem hora, minutos e segundos. Sempre seguindo o padrão ISO para data (yyyy/MM/dd'T'HH:mm:ss). Ex: "2024-07-24T16:20:00".

## Referências de tipo
  - `idType`: um inteiro sendo um auto increment do banco ou um UUID. Deve ser usando o mesmo tipo de `id` para todas as tabelas.

  - `dateString`: string no formato ISO Date ("yyyy-MM-dd"). Ex: "2024-07-24"

Obs: Campos com um "?" no final são campos opcional. Nas responses os campos opcionais devem vir com o valor `null` caso o valor não exista.
  

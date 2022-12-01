# CRUD de usuário com relação às recipes

### Introdução

Aprendemos a criar e inserir documentos no banco de dados diretamente com `Mongoose`, fixando o conhecimento sobre seus métodos.
Hoje aprendemos a relacionar esses documentos também utilizando o mongoose através do `Types.ObjectId`. Vamos praticar esse aprendizado criando rotas de usuário relacionando as receitas que iremos criar.

## Requerimentos

Você irá trabalhar no mesmo arquivo do `Lab-mongoose-recipes`, apenas adicionando rotas. Caso queira, pode-se utilizar o [gabarito](https://github.com/tatialveso/mongoose-recipes).

## Instruções

### Iteração 1 User Schema

Crie um Schema para um usuário contendo as seguintes informações:

- username: tipo `String` deve ser `required` e `unique`
- bio: tipo `String`
- age: tipo `Number`
- email: tipo `String` deve ser `required` e `unique`
- isChef: tipo `Boolean` default `false`
- recipes: [ tipo `ObjectId` referência à recipe ]

### Iteração 2 Crie as rotas de usuário `/user`

### 2.1 Crie a rota `POST /create`

Essa rota irá receber `requests` contendo um objeto com as informações do usuário: `username`, `bio`, `age`, `email`, `isChef`. Você pode acessar essas informações através do `req.body`.

A rota deve:

- Criar um novo usuário com os valores recebidos da requisição, utilizando o `userModel` do usuário.
- Retornar uma `response` em `JSON` contendo o novo documento criado.

### 2.2 Crie a rota `GET /read/:userId`

Essa rota irá receber o `userId` pelos parâmetro de rota e deverá retornar apenas um usuário. Você pode acessar esses valores através de `req.body` e `req.params` para o parâmetro de rota.

A rota deve:

- Retornar um único documento contendo as informações do usuário pelo `_id`
- Retornar uma `response` em `JSON` contendo as informações do usuário com a chave `recipes` populada. `Lembre-se do .populate() 😉`

### 2.3 Crie a rota `PUT /update/:userId`

Esta rota irá receber o `userId` pelos parâmetros de rota para atualizar as informações do usuário e deve retornar uma `response` com os dados atualizados do `usuário`.

A rota deve:

- Encontrar um usuário pelo `_id` e atualizar os campos que vieram na `req.body`
- Retornar uma `response` em `JSON` incluindo o documento atualizado do usuário.

### 2.4 Crie a rota `DELETE /delete/:userId`

Essa rota irá receber o `userId` pelos parâmetros de rota para deletar um usuário e as receitas que esse usuário criou.

A rota deve:

- Encontrar um usuário pelo `_id` e deletá-lo.
- Encontrar as `recipes` que esse usuário criou e deletá-las. `Lembra do deleteMany()? 👀`.
- Retornar uma `response` em `JSON` retornando apenas o status HTTP de _`204`_.

### Iteração 3 Crie as rotas das receitas `/recipes`

### 3.1 Crie a rota `POST /create/:userId`

Esta rota irá criar uma nova recipe baseada no `model` das receitas e irá receber o `userId` pelos parâmetros de rota para incluirmos a nova receita no documento do usuário que a criou.

A rota deve:

- Criar um novo documento na coleção de `recipes` com as informações adquiridas no `req.body`.
- Inserir essa nova `recipe` na coleção de usuários dentro do objeto do usuário que a criou buscando através do `userModel` e `userId`.
- Retornar uma `response` em `JSON` com o documento criado da `recipe`.

### 3.2 Crie a rota `DELETE /delete/:recipeId`

Esta rota irá buscar uma `recipe` pela `recipeId` e irá deletá-la. Lembre-se de atualizar o usuário e retirar a referência da `recipe` deletada. `Lembre-se do campo`_`creator`_ no `recipeModel`.

A rota deve:

- Encontrar a `recipe` pela `recipeId` e deletá-la.
- Encontrar o usuário que a criou e deletar a referência da `recipe` no campo `recipes`.
- Retornar uma `response` em `JSON` contendo apenas o status HTTP de _`204`_.

**Bons códigos!!** 🎇

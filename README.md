<h1 align="center">
    <img alt="Rocketseat GoStack" src="https://camo.githubusercontent.com/d25397e9df01fe7882dcc1cbc96bdf052ffd7d0c/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f676f6c64656e2d77696e642f626f6f7463616d702d676f737461636b2f6865616465722d6465736166696f732e706e67" width="100%" />
</h1>

## Rocketseat

# :rocket: Desafio 06: Database upload

> TUDO ESTÁ BEM!!!!!.  <img src="https://user-images.githubusercontent.com/20192309/80777643-4202cd80-8b3c-11ea-8f32-5348bda4486b.jpg" width="10%" />

## Sobre o desafio

Nesse desafio aprendemos a trabalhar com upload de arquivos e banco de dados postgres. Vamos criar transações financeiras, categorias e inserir novas trasaçẽos com upload de um arquivo .csv.

![desafio06](https://user-images.githubusercontent.com/20192309/80894945-34715300-8cb6-11ea-8aee-af98410c1ecb.png)

## Versão

<a href="https://nodejs.org/pt/"> NodeJS 12.16.2 </a> <br/>
<a href="https://www.notion.so/Instalando-Docker-6290d9994b0b4555a153576a1d97bee2"> Docker 19.03.6 </a> <br/>
<a href="https://hub.docker.com/_/postgres"> Banco de dados Postgres </a>

## Instalação

````sh
yarn
````

## Iniciar uma API

````sh
yarn dev
````

## Usando a API

Adicionar uma nova transação financeira com método POST, chame a URL http://localhost:3333/transactions/ no <a href="https://www.postman.com/downloads/">Postman</a>, no <a href="https://insomnia.rest/download/>Insomnia</a> ou na sua aplicação e informe o corpo da requisição:

Corpo da requisição:

Utilizando type como "income" para entradas e "outcome" para saídas de dinheiro

JSON

````sh
{
  "title": "Salario",
  "value": 3000,
  "type": "income",
  "category": "Salary"
}
````

Ele retorna todos os projetos cadastrados e o que acabou de ser cadastrado:

JSON

````sh
{
    "title": "Salario",
    "type": "income",
    "value": 3000,
    "category_id": "a07aeb42-1f90-4bb1-b5c9-a9807a66e2f9",
    "category": {
        "id": "a07aeb42-1f90-4bb1-b5c9-a9807a66e2f9",
        "title": "Salary",
        "created_at": "2020-05-03T02:50:36.993Z",
        "updated_at": "2020-05-03T02:50:36.993Z"
    },
    "id": "1b04f96c-cebf-43ad-8cc3-eee98adaef6f",
    "created_at": "2020-05-03T02:50:37.002Z",
    "updated_at": "2020-05-03T02:50:37.002Z"
}
````

Buscando as transações registrados, e o balance chame o método GET, chame um URL http://localhost:3333/transactions/

Ele retorna todas as transações e o balanço de entrada, saída e total cadastrados:

JSON

````sh
{
    "transactions": [
        {
            "id": "cfd92f00-0639-44d2-9c40-c2d0eba1b182",
            "title": "Loan",
            "type": "income",
            "value": "1500.00",
            "category_id": "1d9568a4-3f9d-484c-b5c1-7bf6b8cf95c6",
            "created_at": "2020-05-03T01:52:47.365Z",
            "updated_at": "2020-05-03T01:52:47.365Z"
        },
        {
            "id": "a602ee14-e438-41ae-84ad-3188411e05d9",
            "title": "Website Hosting",
            "type": "outcome",
            "value": "50.00",
            "category_id": "1d9568a4-3f9d-484c-b5c1-7bf6b8cf95c6",
            "created_at": "2020-05-03T01:52:47.365Z",
            "updated_at": "2020-05-03T01:52:47.365Z"
        },
        {
            "id": "1b04f96c-cebf-43ad-8cc3-eee98adaef6f",
            "title": "Salario",
            "type": "income",
            "value": "3000.00",
            "category_id": "a07aeb42-1f90-4bb1-b5c9-a9807a66e2f9",
            "created_at": "2020-05-03T02:50:37.002Z",
            "updated_at": "2020-05-03T02:50:37.002Z"
        }
    ],
    "balance": {
        "income": 4500,
        "outcome": 50,
        "total": 4450
    }
}
````

Buscando as transações registrados, e o balance chame o método GET, chame um URL http://localhost:3333/transactions/id da transação = 4b0edfbb-e502-4c46-9b2d-04c0a7f4b2ba

Ele retornará o código:

JSON

````sh
204
````

Para importar um arquivo CSV com mais de uma transação ele deverá seguir padrão abaixo:

````sh
title, type, value, category
Loan, income, 1500, Others
Website Hosting, outcome, 50, Others
Ice cream, outcome, 3, Food
````
E salvar o aquirvo com o nome que quiser com a extenção .csv, você pode se basear na imagem abaixo para importar o arquivo com as transações.

![importarFile](https://user-images.githubusercontent.com/20192309/80895164-2de3db00-8cb8-11ea-9cc6-9a6b60f13ede.png)

Ao executar a importação do arquivo o resultado será parecido com:

````sh
[
    {
        "title": "Loan",
        "type": "income",
        "value": "1500",
        "category_id": "1d9568a4-3f9d-484c-b5c1-7bf6b8cf95c6",
        "category": {
            "id": "1d9568a4-3f9d-484c-b5c1-7bf6b8cf95c6",
            "title": "Others",
            "created_at": "2020-05-03T01:52:47.358Z",
            "updated_at": "2020-05-03T01:52:47.358Z"
        },
        "id": "39228e5e-f94f-4656-a332-5869927c9368",
        "created_at": "2020-05-03T03:03:54.458Z",
        "updated_at": "2020-05-03T03:03:54.458Z"
    },
    {
        "title": "Website Hosting",
        "type": "outcome",
        "value": "50",
        "category_id": "1d9568a4-3f9d-484c-b5c1-7bf6b8cf95c6",
        "category": {
            "id": "1d9568a4-3f9d-484c-b5c1-7bf6b8cf95c6",
            "title": "Others",
            "created_at": "2020-05-03T01:52:47.358Z",
            "updated_at": "2020-05-03T01:52:47.358Z"
        },
        "id": "744d2379-0f3d-40ce-aefe-25cd29516c84",
        "created_at": "2020-05-03T03:03:54.458Z",
        "updated_at": "2020-05-03T03:03:54.458Z"
    },
    {
        "title": "Ice cream",
        "type": "outcome",
        "value": "3",
        "category_id": "52e186d4-0fff-41e6-b897-a9ab9fd33d87",
        "category": {
            "id": "52e186d4-0fff-41e6-b897-a9ab9fd33d87",
            "title": "Food",
            "created_at": "2020-05-03T01:52:47.358Z",
            "updated_at": "2020-05-03T01:52:47.358Z"
        },
        "id": "245f1e55-fa46-466e-bf91-edeb4805f596",
        "created_at": "2020-05-03T03:03:54.458Z",
        "updated_at": "2020-05-03T03:03:54.458Z"
    }
]
````

Caso o usuário informe qualquer type diferente de "income" e "outcome" ele retornará o seguinte erro:

````sh
{
    "error": "Transaction type is invalid"
}
````

Se o total de saída "outcome" informado for maior que o saldo ele retornará a seguinte mensagem de erro:


````sh
{
    "error": "You do not have enough balance"
}
````

Feito com ♥ by Kayza :wave:

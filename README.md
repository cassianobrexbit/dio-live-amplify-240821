# dio-live-amplify-240821
Repositório para o live codingo do dia 24/08/2021

### Pré requisitos
- Node.js
- npm
- git
- Conta na AWS

### Instalar e configurar o Amplify CLI

```
npm install -g @aws-amplify/cli
amplify configure
```

#### Criar usuáirio no AWS IAM
- Selecionar a  política ```AdministratorAccess```

-Configurar o usuário 

```
Enter the access key of the newly created user:
? accessKeyId:  # YOUR_ACCESS_KEY_ID
? secretAccessKey:  # YOUR_SECRET_ACCESS_KEY
This would update/create the AWS Profile in your local machine
? Profile Name:  # (default)

Successfully set up the new user.
```

#### Criar o projeto fullstack

```
mkdir -p amplify-js-app/src && cd amplify-js-app
touch package.json index.html webpack.config.js src/app.js
```
- A estrutura de diretórios do projeto é a seguinte:
```
amplify-js-app
├── index.html
├── package.json
├── src
│   └── app.js
└── webpack.config.js
```
- Adicionar o seguinte conteúdo ao arquivo ```package.json```:
```
{
  "name": "amplify-js-app",
  "version": "1.0.0",
  "description": "Amplify JavaScript Example",
  "dependencies": {
    "aws-amplify": "latest"
  },
  "devDependencies": {
    "webpack": "^4.17.1",
    "webpack-cli": "^3.1.0",
    "copy-webpack-plugin": "^6.1.0",
    "webpack-dev-server": "^3.1.5"
  },
  "scripts": {
    "start": "webpack && webpack-dev-server --mode development",
    "build": "webpack"
  }
}
```
- Instalar as dependências
```
npm install
```
- Adicionar o seguinte conteúdo ao arquivo ```index.html```
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Amplify Framework</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <style>
      html, body { font-family: "Amazon Ember", "Helvetica", "sans-serif"; margin: 0; }
      a { color: #ff9900; }
      h1 { font-weight: 300; }
      hr { height: 1px; background: lightgray; border: none; }
      .app { width: 100%; }
      .app-header { color: white; text-align: center; background: linear-gradient(30deg, #f90 55%, #ffc300); width: 100%; margin: 0 0 1em 0; padding: 3em 0 3em 0; box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.3); }
      .app-logo { width: 126px; margin: 0 auto; }
      .app-body { width: 400px; margin: 0 auto; text-align: center; }
      .app-body button { background-color: #ff9900; font-size: 14px; color: white; text-transform: uppercase; padding: 1em; border: none; }
      .app-body button:hover { opacity: 0.8; }
    </style>
  </head>

  <body>
    <div class="app">
      <div class="app-header">
        <div class="app-logo">
          <img
            src="https://aws-amplify.github.io/images/Logos/Amplify-Logo-White.svg"
            alt="AWS Amplify"
          />
        </div>
        <h1>Welcome to the Amplify Framework</h1>
      </div>
      <div class="app-body">
        <h1>Mutation Results</h1>
        <button id="MutationEventButton">Add data</button>
        <div id="MutationResult"></div>
        <hr />

        <h1>Query Results</h1>
        <div id="QueryResult"></div>
        <hr />

        <h1>Subscription Results</h1>
        <div id="SubscriptionResult"></div>
      </div>
    </div>
    <script src="main.bundle.js"></script>
  </body>
</html>

```

- Adicionar o seguinte conteúdo ao arquivo ```webpack.config.json```:
```
const CopyWebpackPlugin = require('copy-webpack-plugin');
const webpack = require('webpack');
const path = require('path');

module.exports = {
    mode: 'development',
    entry: './src/app.js',
    output: {
        filename: '[name].bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/
            }
        ]
    },
    devServer: {
        contentBase: './dist',
        overlay: true,
        hot: true
    },
    plugins: [
        new CopyWebpackPlugin({
            patterns: ['index.html']
        }),
        new webpack.HotModuleReplacementPlugin()
    ]
};
```
- Iniciar a aplicação
``` npm start ```

- Obs: O botão de ```Add data``` não funciona ainda.

#### Inicializar o back-end Amplify:
```
amplify init
```

O Amplify solicitará algumas informações sobre o seu projeto. Para esta Live, serão mantidos as informações padrões

```
Enter a name for the project (amplifyjsapp)

# All AWS services you provision for your app are grouped into an "environment"
# A common naming convention is dev, staging, and production
Enter a name for the environment (dev)

# Sometimes the CLI will prompt you to edit a file, it will use this editor to open those files.
Choose your default editor

# Amplify supports JavaScript (Web & React Native), iOS, and Android apps
Choose the type of app that you're building (javascript)

What JavaScript framework are you using (none)

Source directory path (src)

Distribution directory path (dist)

Build command (npm run-script build)

Start command (npm run-script start)

# This is the profile you created with the `amplify configure` command in the introduction step.
Do you want to use an AWS profile

? Initialize the project with the above configuration? Yes
Using default provider  awscloudformation
? Select the authentication method you want to use: AWS profile
```
- Para criar uma API

```
amplify add api
```
- O Amplify solicitará mais algumas informações para a sua API
```
? Please select from one of the below mentioned services:
# GraphQL
? Provide API name:
# amplifyjsapp
? Choose the default authorization type for the API:
# API Key
? Enter a description for the API key:
# todos
? After how many days from now the API key should expire:
# 7 (or your preferred expiration)
? Do you want to configure advanced settings for the GraphQL API:
# No
? Do you have an annotated GraphQL schema?
# No
? Choose a schema template:
# Single object with fields (e.g., “Todo” with ID, name, description)
? Do you want to edit the schema now?
# Yes
```
- O CLI irá abrir em sua IDE o arquivo ```schema.graphql```

#### Publicar a API GraphQL

```
amplify push
```
- Mantenha todas as configurações padrão sugeridas:
```
? Do you want to generate code for your newly created GraphQL API (Yes)
? Choose the code generation language target (javascript)
? Enter the file name pattern of graphql queries, mutations and subscriptions (src/graphql/**/*.js)
? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions (Yes)
? Enter maximum statement depth [increase from default if your schema is deeply nested] (2)
```
- Verificar o status da API:
```
amplify status
```
- Testando a API
```
amplify console api
```
#### Conectando o front-end com a a API

- Atualize o arquivo ``` src/app.js ``` com o seguinte código:
```
import Amplify, { API, graphqlOperation } from "aws-amplify";

import awsconfig from "./aws-exports";
import { createTodo } from "./graphql/mutations";

Amplify.configure(awsconfig);

async function createNewTodo() {
  const todo = {
    name: "Use AppSync",
    description: `Realtime and Offline (${new Date().toLocaleString()})`,
  };

  return await API.graphql(graphqlOperation(createTodo, { input: todo }));
}

const MutationButton = document.getElementById("MutationEventButton");
const MutationResult = document.getElementById("MutationResult");

MutationButton.addEventListener("click", (evt) => {
  createNewTodo().then((evt) => {
    MutationResult.innerHTML += `<p>${evt.data.createTodo.name} - ${evt.data.createTodo.description}</p>`;
  });
});
```
- Reinicie o projeto com o comando ``` npm start ```

- Atualize o projeto com os seguintes códigos para listar os itens registrados no DynamoDB:
```
import { listTodos } from "./graphql/queries";
```
```
async function getData() {
      API.graphql(graphqlOperation(listTodos)).then((evt) => {
        evt.data.listTodos.items.map((todo, i) => {
          QueryResult.innerHTML += `<p>${todo.name} - ${todo.description}</p>`;
        });
    });
}
```
```
getData();
```

Para subscrever um item registrado insira o seguinte código:
```
import { onCreateTodo } from "./graphql/subscriptions"
```
```
const SubscriptionResult = document.getElementById("SubscriptionResult");
```

```
API.graphql(graphqlOperation(onCreateTodo)).subscribe({
    next: (evt) => {
        const todo = evt.value.data.onCreateTodo;
        SubscriptionResult.innerHTML += `<p>${todo.name} - ${todo.description}</p>`;
    },
});
```
#### Deploy e host da aplicação

- Para publicar a aplicação insira o seguinte comando:
```
amplify add hosting
```
- Mantenha as configurações padrão para as respostas solicitadas pelo Amplify:
```
? Select the plugin module to execute: # Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
? Choose a type: # Manual Deployment
```
- Para o deploy da aplicação, inicie o comando:
 ```
 amplify publish
 ```

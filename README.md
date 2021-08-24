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

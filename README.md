### Configuração da base projeto com React

### PASSO A PASSO APP REACT
### Criando package.json - Dependências do Projeto(Códigos de terceiros, também bibliotecas)
    yarn init -y

### PRÓXIMO PASSO:
Vamos criar a pasta public e dentro dela o arquivo index.html

Vamos criar também a nossa pasta src que armazena todo nosso código da aplicação

### Instalação de Dependências

### 1 - React
    yarn add react

### 2 - React-dom - A forma de se trabalhar com React na web
DOM -> é árvore de elementos da nossa aplicação, é o HTML convertido na sintaxe de Objetos do JavaScript

    yarn add react-dom

### 3 - Babel
BABEL -> Converte nosso código para um maneira que todos os browsers e todo o ambiente da nossa aplicação consigam entender todos os códigos
Mas porque usamos o Babel? -> Converte o códigos para que os navegadores mais modernos entendam
Documentação: https://babeljs.io
   
    yarn add @babel/core @babel/cli @babel/preset-env -D

### Para que servem as dependências do babel instaladas?
@babel/core -> A biblioteca do babel 99% das funcionalidades do babel estão aqui.

@babel/cli -> Permite executar o babel através da linha de comando ex: yarn babel -h

@babel/preset-env -> Uma biblioteca ou extensão do babel, serve para identificar o ambiente que a aplicação está sendo executada para converter o código da melhor maneira possível.

Após a instalação das dependências do babel vamos criar o arquivo de configuração do babel o babel.config.js.

### Vamos criar dentro da pasta src o nosso arquivo index.js
Para isso vamos criar um arquivo chamado index.js dentro da pasta src

### EXEMPLO: Convertendo código javascript com o babel
Para executar o babel vamos usar a dependência @babel/cli para executar comando no terminal.

    yarn babel src/index.jsx --out-file dist/bundle.js

yarn babel o arquivo a ser convertido seguido do comando -o ou --out-file para gerar o arquivo de saída bundle.js na pasta dist
bundle geralmente é o arquvivo utilizado ou o nome(convensão utilizada pelo babel).

### Instalação do @babel/preset-react 
Serve para entender o código react dentro do arquivo

     yarn add @babel/preset-react -D
    
Após a instalação da dependência vamos configurar dentro do babel dentro de presets vamos adicionar:

    '@babel/preset-react'

### Instalação do WebPack   

    yarn add webpack webpack-cli webpack-dev-server -D

Após a instalação da dependência do webpack vamos criar o arquivo de configuração chamado:

    webpack.config.js

Arquivo que contém todas as configurações da aplicação.

### Instalação do babel-loader
    yarn add babel-loader -D

O babel-loader é basicamente a integração entre o babel e o webpack

### Criando o arquivo App.tsx

Agora que configuramos o webpack vamos criar o arquivo App.tsx dentro da pasta src

### Instalação da html-webpack-plugin   
    yarn add html-webpack-plugin -D

### Instalação do webpack-dev-server
    yarn add webpack-dev-server -D

A dependência serve para gerar o bundle novamente sem precisar ficar rodando o comando yarn webpack

Após a instalação da dependência rodar o comando:
    
    yarn add webpack-dev-server -D

Com isso ao salvar o arquivo o webpack já faz a compilação e retorna as novas alterações

### Observação: 
Lembramos que a aplicação vai subir na URL: http://localhost:8080

### Outro passo importante é a configuração do sourcemap
Para que serve? Com a configuração do source map melhoramos a forma com que visualizamos os erros
Com isso fica mais fácil de debugar e entender onde está um erro que pode ter acontecido

para configura-lo basta adicionar ao webpack.config.js: 

    devtool: 'eval-source-map',

### Configurando ambiente de Produção e ambiente de Desenvolvimento
Com a configuração diferente dos ambiente temos uma configuração do webpack em Dev e outra em Prod
Para isso vamos adicionar no arquivo webpack.config.js as seguintes configurações:


    const isDevelopment = process.env.NODE_ENV !== 'production';

    module.exports = {
        mode: isDevelopment ? 'development' : 'production',
        devtool: isDevelopment ? 'eval-source-map' : 'source-map',

Para isso precisamos criar a variável NODE_ENV e temos algumas formas: `

Para LINUX e MAC:

    NODE_ENV=production yarn webpack

### Outra forma de criamos nossas variáveis de ambiente é instalando o cross-env
O cross-env permite criar variáveis de ambiente independente do sistema operacional

    yarn add cross-env -D

Agora vamos criar no package.json dois scripts um para dev outro para prod como no exemplo abaixo:

    "scripts":{
        "dev": "webpack serve",
        "build": "cross-env NODE_ENV=production webpack"
    },

Após a configuração podemos rodar o ambiente de desenvolvimento

Ambiente de desenvolvimento:

    yarn dev

Ambiente de Produção:

    yarn build


### Também precisamos configurar a importação de arquivos CSS na nossa aplicação

Para isso vamos instalar as seguintes dependencias

    yarn add style-loader -D
    yarn add css-loader -D

São usados em conjuntos

também precisamos configurar o nosso webpack com as seguintes informaçõe dentro de rules:

    {
        test: /\.css$/,
        exclude: /node_modules/,
        use: ['style-loader', 'css-loader'],
    },

### Por fim vamos configurar o nosso Pré-processador de CSS o SAAS
O SAAS é um pré-processador de CSS

primeiro vamos instalar o sass-loader com o serguinte comando:

    yarn add sass-loader -D

O sass-loader é um loader do webpack que serve para entender arquicos sass

Precisamos também do node-sass

    yarn add node-sass -D



Também precisamos configurar o webpack.config.js com isso vamos ter a seguinte configuração: 

Vamos substituir o arquivo anterior para este:

    {
        test: /\.scss$/,
        exclude: /node_modules/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
    },


Também vamos precisar alterar o arquivo global.css para global.scss
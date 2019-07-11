?
*** Modulo04 ***

#Conceitos do React

#Configurando estrutura
md modulo04
cd modulo04
yarn init -y
yarn add @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli
yarn add react react-dom
code .
criar babel.config.js
criar webpack.config.js
criar index.js
yarn add babel-loader -D
alterar package.json
yarn build
é gerado o arquivo public/bundle.js
criar public/index.html
Botão direito sobre public/index.html e Reveal in Explorer
yarn add webpack-dev-server -D
Atualiza o navegador automaticamente
alterar o webpack.config.js com
  devServer: { contentBase: path.resolve(__dirname, 'public'), },

alterar o script de package.json com "dev": "webpack-dev-server --node development"
yarn dev

#Criando componente raiz
Modificar os arquivos src/index.js e public/index.html
Componetizar
Criar src/App.js
Quando usar sintaxe html deve importa o 'react'
em src/index.js importar App from src/App.js

#Importando CSS
Single-Page Applications SPA. Forma de controlar as rotas, recebe JSON.
Babel não entende css, usar o webpack.
Webpack faz o live reload.

#Importando imagens
Cancelar o servidor yarn dev
yarn add file-loader -D
nova rule em webpack.config.js
  test: /.*\.(git|png|jpg|jpe?g)$/i,
  use: { loader: 'file-loader',}
yarn dev

#Class Components
Armazena estados em classes.
Funções e variáveis não eram possíveis.
Obrigatoriamente usa o nome state = {}
para poder mudar os valores na classe
Novo plugin do babel
Cancelar servidor
yarn add @babel/plugin-proposal-class-properties -D
alterar babel.config.js
    plugins: [ '@babel/plugin-proposal-class-properties' ]

#Estado & Imutabilidade
Para ter acesso ao this.state tem que usar arrow function e não função comum.
 handleInputChange = e => { console.log(e.target.value); }
 Para mudar valor do state usar this.setState();

#Removendo itens do estado

#Propriedades do React
criar TechItem.js no formato de function e não de classe pois não terá um estado.
Manter a key no TechList, enviar a tech com parâmetro.
No TechItem receber desestruturando a props como { tech }.
As propriedades de um componente dentro de classes ficam como this.props.tech
No TechList enviar a função como propriedade onDelete={this.handleDelete}

#Default Props & PropTypes
TechItem.defaultProps
Em TechList <TechItem /> ou <TechItem tech='Nova Propriedade2'/>
Pode definir de maneira statica na classe como:
  static defaultProps = { tech: 'Oculto' }
Em TechItem:
      TechItem.propTypes = {
            tech: PropTypes.string,
            onDelete: PropTypes.func.isRequired,
      }

#Ciclo de vida do componente
  // Executado assim que o componente aparece em tela
  componentDidMount() {    }
  // Executado sempre que houver alterações nas props ou estado
  componentDidUpdate(prevProps, prevState) { // this.props, this.state }
  // Executado quando o componete deixa de existir
  componentWillUpdate() { }

  componentDidUpdate(_, prevState) {
    if (prevState.techs !== this.state.techs) {
      localStorage.setItem('techs', JSON.stringify(this.state.techs));
    }
  }
  No navegador ir para [inspecionar][Application][Local Storage][http://localhost:8080]
  componentDidMount() {
    const techs = localStorage.getItem('techs');
    if (techs) {
      this.setState({ techs: JSON.parse(techs) });
    }
  }
  Ao cadastrar iten e dar F5 já vem com os dados cadastrados


#Debugando React com DevTools
React Developer Tools
[inspecionar][React]

Para o módulo05
yarn create react-app modulo05
cd modulo05
code .


*** Módulo 05 ***

#Criando projeto do zero
yarn create react-app modulo05
cd modulo05
code .
package.json
deletar   "eslintConfig": { "extends": "react-app" },
deletar em public index.html os comentários e manifest
deletar o arquivo manifest.json
yarn start


#ESLint, Prettier & EditorConfig
Já tem o EditorConfig instalado [botão Direito][Generation .editorConfig]
alterar no .editoconfig:
  end_of_line = lf
  trim_trailing_whitespace = true
  insert_final_newline = true
yarn add eslint -d
yarn eslint --init
### configurar eslint ###
  1a. Última opção: To check syntax, find problems, and enforce code style
  2a. Primeira opção: JavaScript modules (import/export)
  3a. Última opção: React
  4a. Selecionar: Browser
  5a. Primeira opção: Use a popular style guide
  6a. Primeira opção: Airbnb (https://)
  7a. Primeira opção: JavaScript
  8a. Y/N: Y
  Remover o arquivo: package-lock.json e rodar novamente o yarn
yarn
  Gerado o arquivo .eslintrc.js, fazer as configurações
  instalar a extensão (CTRL+SHIF+X) do ESlint (já tem)
  CTRL+SHIF+P e alterar o Open Settings (JSON) (ok!)
  editar o arquivo .eslintrc.js (ok!)

yarn add prettier eslint-config-prettier eslint-plugin-prettier babel-eslint -d
  mudar o arquivo .eslintrc.js para extends: ['airbnb-base', 'prettier', 'prettier/react]
  parser: 'babel-eslint',
  plugins: ['react', 'prettier',],
  rules: {'prettier/prettier': 'error', 'react/jsx-filename-extension': [ 'warn', { extensions: ['.jsx', '.js'] } ], import/prefer-default-export': 'off', },
  Criar o arquivo .prettierrc para sobrescrever regras e não entrar em conflito com airbnb-base
  { "singleQuote": true, "trailingComma": "es5" }

************************
### Corrigir erros em todos os arquivos ###
yarn eslint --fix src --ext .js
************************

#Roteamento no React
Rotear entre páginas sem precisar recarregar a página.
Construir um SPA Simple Page Application, ou seja, nunca recarrega completamente a página, a não ser que o usurário digite F5.
yarn add react-router-dom
Faz o roteamento no frontEnd.
src/routes.js
src/Main/index.js
src/Repository/index.js

#Styled Components
yarn add styled-components
baixar plugi-in styled components
Estilição fica no formato de .js com sintaxe css.




#Estilos globais
Ok!

#Estilizando página Main
yarn add react-icons


#Adicionando repositórios
Api para fazer requisições
yarn add axios
api do github
estados do botão
animação de load
atributos e props do keyframes e css
mudar no navegador velocida da internet


#Listando repositórios
Estilo de listas.
& + li Aplica estilos em todos da lista li menos no primeiro.
#Utilizando LocalStorage
Main/index
componentDiMount() e componentDiUpdate()
#Navegação de rotas
Link para navegação sem recarregar toda a página.
trocar o <href a> por <lint to>
decodeURIComponent
#Carregando dados da API
Dois await, o segundo espera o primeiro, viram uma array de promisses que rodam simultaneamento.
Passar parâmetros para promisses, filtrar por itens por página.
Salvar os dados no state.
#Definindo PropTypes
yarn add prop-types
compartilhar um componente entre duas rotas.

#Exibindo repositório
Informações sobre o repositório, nome e descrição, e sobre o dono <Owner> do repositório.
Cria estilos para Owner.
Link de retorno.

#Exibindo issues
Listagem sobre issues dos repositórios.
Usar a key Unique como string: key={String(issude.id)}
Css com Estilos na issue.


## Desafio 02 ##

*** Configurando estrutura ***
md modulo02
cd modulo02
yarn init -y
code .
yarn add express
gerado os arquivos: package.json e yarn.lock
### estrutura de pastas ###
src
  app.js      --> configurar o servidor com classes, usa express, define middlewares e rotas, é chamado uma única vez.
  routes.js   --> Usa express para criar as rotas, .get(req, res)
  server.js   --> Fica ouvindo a porta, chama o app.js.
node src/server.js

*** Nodemon & Sucarase ***
sucrase --> novas nomenclatura do javascript
nodemon --> atualiza o servidor quando alterar os arquivos no visual studio
yarn add sucrase nodemon -D
yarn sucrase-node src/server.js
### mudar e criar arquivos ###
  mudar o arquivo do package.json para incluir script "dev"
  criar o arquivo nodemon.json para usar o sucrase-node e não o nodemon
yarn dev
?

*** Configurando Docker docker 2:40 ***
https://docs.docker.com/toolbox/toolbox_install_windows/
docker -v
docker help
IP 192.168.99.100
docker run --name meudatabase -e POSTGRES_PASSWORD=minhasenha -p 5432:5432 -d postgres
docker ps
baixar Postbird 7:30 em electronjs.org/apps/postbird
docker stop meudatabase
docker ps -a
docker start meudatabase
docker logs meudatabase

*** Sequelize & MVC ***
Abstração do banco de dados
Models, View e Controllers
Substitui a linguagem SQL para javascript
Usa a funcionalidade de Migrations para controle de versões de banco de dados.
Migrations cria e altera as tabelas no banco de dados com as functions up nova migration e down desfaz a migration (callback).
Cada migration e para uma tabela.
Dados fictícios: Seeds para popular arquivos através de códigos.
Não usar Seeds para dados em produção, usar Migrations
Model --> Abstração do banco
Controller -> Regra de negócios, rotas, é uma classe, retorna JSON ou HTML, não chama outro Controller ou método. Cada Model tem um Controller, tem Controller que não tem Model.
  Tem no máximo 5 métodos: index() --> Listar, show() --> Exibir um, store() --> Cadastrar, update() --> Alterar, delete() --> Remover. Se precisar de mais funções crie outra entidade.
View --> Visualização do usuário

*** ESLint, Prettier & EditorConfig ***
yarn add eslint -d
yarn eslint --init
### configurar eslint ###
  1a. Última opção: To check syntax, find problems, and enforce code style
  2a. Primeira opção: JavaScript modules (import/export)
  3a. Última opção: None of these
  4a. Selecionar: Node
  5a. Primeira opção: Use a popular style guide
  6a. Primeira opção: Airbnb (https://)
  7a. Primeira opção: JavaScript
  8a. Y/N: Y
  Remover o arquivo: package-lock.json e rodar novamente o yarn
yarn
  Gerado o arquivo .eslintrc.js, fazer as configurações
  instalar a extensão (CTRL+SHIF+X)do ESlint
  CTRL+SHIF+P e alterar o Open Settings (JSON)
  editar o arquivo .eslintrc.js

yarn add prettier eslint-config-prettier eslint-plugin-prettier -d
  mudar o arquivo .eslintrc.js para extends: ['airbnb-base', 'prettier'] e mais.
  Criar o arquivo .prettierrc para sobrescrever regras e não entrar em conflito com airbnb-base
### Corrigir erros em todos os arquivos ###
yarn eslint --fix src --ext .js
### Para editores diferentes ###
plugin editorconfig
  Ir para raiz do projeto: [botão direito][Generate .editorconfig]

*** Configurando o Sequelize ***
Criar as pastas
### estrutura de pastas ###
src
  app
    controllers
    models
  config
    database.js
  database
    migrations
  app.js      --> configurar o servidor com classes, usa express, define middlewares e rotas, é chamado uma única vez.
  routes.js   --> Usa express para criar as rotas, .get(req, res)
  server.js   --> Fica ouvindo a porta, chama o app.js.

yarn add sequelize
yarn add sequelize-cli -D

criar arquivo .sequelizerc com sintaxe javaScript para exportar os caminhos criados na estrutura: database, models, migrations e no futuro seeds.
### Dependências para postgres ###
yarn add pg pg-hstore
  Configurar o database.js

*** Migration de usuário ***
  Cria um arquivo de migration dentro da pasta src/database/migrations
yarn sequelize migration:create --name=create-users
  Abrir e modificar o arquivo criado
yarn eslint --fix src/database/migrations --ext .js
yarn eslint --fix migrations --ext .js

yarn sequelize db:migrate
Se precisar desfazer alteração no db:
yarn sequelize db:migrate:undo
      ou
yarn sequelize db:migrate:undo:all

*** Model de usuário ***
Abrir o arquivo User.js
  Enviar apenas colunas que serão alteradas pelo usuário.
  Repassa dois parâmetros: 1 do banco de dados, 2. sequelize e outros.
  this.addHook('beforeSave', ()) --> Realiza o códio antes de salvar.

*** Criando loader de models ***
criar o arquivo src/database/index.js, Sequelize é quem faz a conexão com o banco de dados. Variável sequelize poderia ser variável connection.
Rodar o servidor
yarn dev
2:20 Falha ao criar variável de ambiente.

*** Cadastro de usuários ***
**** Gerando hash da senha
yarn add bcryptjs

Não consigo fazer a minha variável de ambiente no Insomnia funcionar.
Alguma sugestão? Digitar e esperar a recomendação.

*** Conceitos de JWT, Jason Web Token ***
Vai gerenciar uma rota de sessão, recebe e-mail e senha, acessa BD e gera o Token

### Ao reiniciar a máquina ###
Abrir: Visual Studio, Docker, Insomnia, Postbir
yarn dev
docker start meudatabase
No Postbird Connect
Selecionar gobarber

*** Autenticação JWT ***
Cria uma SeesionControler para criar uma sessão e não um usuário, pois UserController já tem um store.

yarn add jsonwebtoken

www.md5online.org --> Para digitar um texto aleatório e gerar um token para salvar na aplicação.
O Token na aplicação tem id, token e data expiração.
Deixar as informações da autenticação em app/config/auth.js

*** Middleware de autenticação ***
Só faz sentido para usuários logados.
Em routes.js interceptar requisição com middlewares.
Em cada requisição usar o Header da requisição.
Em routes.js ele vai bloquear as rotas que vem a seguir dele, caso a autenticação falhe.
Utiliza promisify from 'util' para função assíncrona e não callback.
recupera o id e data de expiração que estava criptografada.
Insere o id do usuário no req.userId

*** Update do usuário ***
Faz checagem de usuário já existe e senhas

*** Validando dados de entrada ***
yarn add yup
Fazer validação no backend e frontend
Segue o schema validation
Tem os mesmos campos do body que usuário envia
*** MODULO 03 ***
*** Configurando o Multer ***
yarn add multer

*** Avatar do usuário ***
yarn sequelize migration:create --name=create-files
yarn sequelize migration:create --name=add-avatar-field-to-users
yarn sequelize db:migrate

*** Migration e model de agendamento ***
yarn sequelize migragtion:create --name=create-appintments
yarn sequelize db:migrate
*** Validações de agendamento ***
yarn add date-fns@next

*** Configurando o MongoDB ***
docker run --name mongobarber -p 27017:27017 -d -t mongo
yarn add mongoose
https://www.mongodb.com/products/compass
yarn dev

*** Configurando Nodemailer ***
yarn add nodemailer
https://mailtrap.io

*** Configurando templates de e-mail ***
https://handlebarsjs.com
yarn add express-handlebars nodemailer-express-handlebars

*** Configurando fila com Redis ***
docker run --name redisbarber -p 6379:6379 -d -t redis:alpine
https://github.com/bee-queue/bee-queue
yarn add bee-queue
Em outro terminal
yarn queue

*** Tratamento de exceções ***
https://sentry.io
yarn add @sentry/node@5.4.3
yarn add express-async-errors
yarn add youch

*** Variáveis ambiente ***
yarn add dotenv


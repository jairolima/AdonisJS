# AdonisJS
Estudos

-instalando adonis global
sudo npm install -g @adonisjs/cli

-criando projeto
adonis new gonode --api-only

-colocando servidor online
adonis serve --dev

-Eslint como dependencia de desenvolvimento
npm install -D eslint

-executar eslint
npx eslint --init
vai gerar arquivo eslintrc.json e configurar

-vai na pasta config -> database.js escolhe o banco e executa o comando
npm i --save mysql

-configura o arquivo .env com banco, usuario e senha

-para testar se funcionou
adonis migration:run
ele cria as tabelas padrao no banco

-criando controller User
adonis make:controller User

-Lista todas as rotas
adonis route:list

=======================

Autenticação JWT

-Criar controller
adonis make:controller Session

-Recuperar senha
adonis make:controller ForgotPassword

-criar 2 novos campos na tabela
nao é recomendavel alterar a migration, porem o projeto ainda nao foi pro git
adonis migration:rollback

-apos adicionar os campos na model
adonis migration:run

adonis install @adonisjs/mail

-trabalhar com datas
ni moment (npm install moment)

=========================



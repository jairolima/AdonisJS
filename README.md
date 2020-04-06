# AdonisJS
Estudos

-instalando adonis global (Instalando o cli do adonis só precisa uma vez)
sudo npm install -g @adonisjs/cli

-Listar comandos
adonis

-criando projeto
adonis new nomedoprojeto --api-only

-colocando servidor online (Não precisa usar o nodemon para reiniciar o servidor toda vez)
adonis serve --dev

-Eslint como dependencia de desenvolvimento
npm install -D eslint

-executar eslint (Respeitar a guia de estilos do framework)
npx eslint --init
vai gerar arquivo eslintrc.json e configurar assim:

{
    "extends": "standard",
    "globals": {
      "use": true
    }
}

-vai na pasta config -> database.js escolhe o banco e executa o comando
npm i --save mysql

-configura o arquivo .env com banco, usuario e senha

-para testar se funcionou
adonis migration:run
ele cria as tabelas padrao no banco

-criando controller User
adonis make:controller User

'use strict'

const User = use('App/Models/User')

class UserController {
  async store ({ request }) {
    const data = request.only(['username', 'email', 'password'])

    const user = await User.create(data)

    return user
  }
}

module.exports = UserController

vai no routes e coloca:
Route.post('users', 'UserController.store')

-Lista todas as rotas
adonis route:list

=======================

Autenticação JWT

-Criar controller (No config auth.js vc pode configurar se o usuario vai se autenticar por cpf, email etc)
adonis make:controller Session

async store ({ request, response, auth }) {
    const { email, password } = request.all()

    const token = await auth.attempt(email, password)

    return token
  }

-Recuperar senha
adonis make:controller ForgotPassword


'use strict'

const crypto = require('crypto')
const User = use('App/Models/User')
const Mail = use('Mail')

class ForgotPasswordController {
  async store ({ request, response }) {
    try {
      const email = request.input('email')
      const user = await User.findByOrFail('email', email)

      user.token = crypto.randomBytes(10).toString('hex')
      user.token_created_at = new Date()

      await user.save()

      await Mail.send(
        [''],
        {},
        message => {
          message
            .to(user.email)
            .from('msgjairo@gmail.com', 'Jairo | gocorals')
            .subject('Recuperação de senha')
        }
      )
    } catch (err) {
      return response.status(err.status)
        .send({ error: { message: 'Algo nao deu certo, esse email existe?' } })
    }
  }
}

module.exports = ForgotPasswordController


lembrar de criar a rota

-criar 2 novos campos na tabela
nao é recomendavel alterar a migration, porem o projeto ainda nao foi pro git
adonis migration:rollback

-apos adicionar os campos na model
adonis migration:run

adonis install @adonisjs/mail

-trabalhar com datas
ni moment (npm install moment)

=========================



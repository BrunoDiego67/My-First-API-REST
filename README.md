# My-First-API-REST

Estrutura de Pastas:
src/ (Pasta raiz do código-fonte)
  -index.js (Arquivo principal que inicia o servidor)
  -rotas.js (Definição das rotas da API)
  -bancodedados.js (Módulo para interagir com o banco de dados)
  -controladores/ (Pasta com os controladores)
    -instrutores.js (Arquivo com funções que lidam com as requisições)
.gitignore (Ocultar Arquivos)
package-lock.json (Framework Express)
package.json (Servidor)

Recursos Principais:

Servidor Express: Utiliza o framework Express.js para criar um servidor web que lida com as requisições HTTP.

Nodemon: Facilita o desenvolvimento, monitorando automaticamente as mudanças no código e reiniciando o servidor quando necessário.

Gitignore: Ignora arquivos e pastas não necessários para o controle de versão, como arquivos de dependência e logs.

Rotas HTTP: Implementa rotas HTTP para gerenciar operações CRUD (Create, Read, Update, Delete) em usuários.

Exemplos de Endpoints:
<div>
GET /users: Retorna a lista de usuários.
GET /users/:id: Retorna detalhes de um usuário específico.
POST /users: Cria um novo usuário.
PUT /users/:id: Atualiza um usuário existente.
PATCH /users/:id: Atualiza parcialmente um usuário existente.
DELETE /users/:id: Exclui um usuário.
Inicialização do Servidor:
</div>

No arquivo index.js, você inicia o servidor Express na porta 3000 usando o método listen.

    // Importa o módulo 'express' para criar um servidor web.
    const express = require('express');

    // Importa o arquivo de rotas que define as rotas da API.
    const rotas = require('./rotas');

    // Cria uma instância do servidor Express.
    const app = express();

    // Adiciona um middleware que interpreta as solicitações HTTP como JSON.
    app.use(express.json());

    // Adiciona as rotas definidas no arquivo './rotas' à aplicação.
    app.use(rotas);

    // Inicia o servidor na porta 3000.
    app.listen(3000);

instrutores.js:

    // Importa o módulo 'instrutores' e 'identificadorInstrutor' do arquivo '../bancodedados'.
    let { instrutores, identificadorInstrutor } = require('../bancodedados');

    // Função para listar todos os instrutores.
    const listarInstrutores = (req, res) => {
    return res.status(200).json(instrutores);
    }

    // Função para obter um instrutor por ID.
    const obterInstrutor = (req, res) => {
    const { id } = req.params;

    // Procura o instrutor no array de instrutores com base no ID.
    const instrutor = instrutores.find((instrutor) => {
        return instrutor.id === Number(id);
    });

    if (!instrutor) {
        return res.status(404).json({ mensagem: 'Instrutor não encontrado.' });
    }

    return res.status(200).json(instrutor);
    }

    // Função para cadastrar um novo instrutor.
    const cadastrarInstrutor = (req, res) => {
    const { nome, email, status } = req.body;

    // Verifica se o nome e o email são fornecidos na requisição.
    if (!nome) {
        return res.status(400).json({ mensagem: 'O nome é obrigatório' });
    }

    if (!email) {
        return res.status(400).json({ mensagem: 'O email é obrigatório' });
    }

    // Cria um novo instrutor com um ID único e os dados fornecidos.
    const instrutor = {
        id: identificadorInstrutor++,
        nome,
        email,
        status: status ?? true
    }

    // Adiciona o novo instrutor ao array de instrutores.
    instrutores.push(instrutor);

    return res.status(201).json(instrutor);
    }

    // Função para atualizar os dados de um instrutor.
    const atualizarInstrutor = (req, res) => {
    const { id } = req.params;
    const { nome, email, status } = req.body;

    // Verifica se o nome e o email são fornecidos na requisição.
    if (!nome) {
        return res.status(400).json({ mensagem: 'O nome é obrigatório' });
    }

    if (!email) {
        return res.status(400).json({ mensagem: 'O email é obrigatório' });
    }

    // Procura o instrutor no array de instrutores com base no ID.
    const instrutor = instrutores.find((instrutor) => {
        return instrutor.id === Number(id);
    });

    if (!instrutor) {
        return res.status(404).json({ mensagem: 'Instrutor não encontrado.' });
    }

    // Atualiza os dados do instrutor com os novos valores.
    instrutor.nome = nome;
    instrutor.email = email;
    instrutor.status = status;

    return res.status(204).send();
    }

    // Função para atualizar o status de um

Rotas:

No arquivo rotas.js, você associa os endpoints às funções controladoras.

    // Importa o módulo 'express' para criar um aplicativo de rotas.
    const express = require('express');

    // Importa as funções controladoras relacionadas aos instrutores do arquivo './controladores/instrutores'.
    const instrutores = require('./controladores/instrutores');

    // Cria uma instância do aplicativo de rotas Express.
    const rotas = express();

    // Define as rotas e associa cada rota a uma função controladora correspondente.

    // Rota para listar todos os instrutores.
    rotas.get('/instrutores', instrutores.listarInstrutores);

    // Rota para obter detalhes de um instrutor específico com base no ID.
    rotas.get('/instrutores/:id', instrutores.obterInstrutor);

    // Rota para cadastrar um novo instrutor.
    rotas.post('/instrutores', instrutores.cadastrarInstrutor);

    // Rota para atualizar os dados de um instrutor existente com base no ID.
    rotas.put('/instrutores/:id', instrutores.atualizarInstrutor);

    // Rota para atualizar o status de um instrutor com base no ID.
    rotas.patch('/instrutores/:id/status', instrutores.atualizarStatusInstrutor);

    // Rota para excluir um instrutor com base no ID.
    rotas.delete('/instrutores/:id', instrutores.excluirInstrutor);

    // Exporta as rotas configuradas para serem utilizadas em outras partes do aplicativo.
    module.exports = rotas;
Este é um resumo da sua API de cadastro de usuários com Express, Nodemon e a estrutura de pastas mencionada. Observe que os detalhes específicos das implementações e lógica de negócios não estão incluídos aqui e devem ser adaptados de acordo com os requisitos do seu projeto real.


## My-First-API-REST
Folder Structure:
.src/ (Source Root Folder). 
  -index.js (Main File Starting Server). 
  -routes.js (API Route Definition). -
  -bancodedados.js (Module for interacting with the database). 
  -controllers/ (Folder with the controllers). 
   -instructors.js (File with functions that handle requests). 
gitignore (Hide Files).
package-lock.json (Framework Express)
package.json (Server)

Main Features:. Express Server: Uses the Express.js framework to create a web server that handles HTTP requests. 
Nodemon: Facilitates development by automatically monitoring code changes and restarting the server when needed. 
Gitignore: Ignores files and folders not needed for version control, such as files dependency and logs. 
HTTP routes: Implements HTTP routes to manage CRUD operations (Create, Read, Update, Delete) on users.

Examples of Endpoints:

<div>
  GET /users: Returns the list of users. 
  GET /users/:id: Returns details of a specific user. 
  POST /users: Creates a new user.
  PUT /users/:id: Updates an existing user.
  PATCH /users/:id: Partially updates an existing user.
  DELETE /users/:id: Deletes a user.
  Initialization of the Server:
</div>


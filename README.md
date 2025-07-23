[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/fO8pjV07)

## 🚀 Projeto: DevBurger – Cardápio Digital com Node.js

Desenvolvido como parte da Etapa 1 do Journey Backend (https://www.sympla.com.br/evento-online/journey-backend/3002580), este projeto simula um sistema de cardápio digital para uma hamburgueria fictícia. Aqui, pratiquei criação de rotas com Express.js, recebimento de dados via formulário e retorno de respostas dinâmicas, com estrutura organizada e boas práticas REST.


🔗 Acesse a API publicada aqui: https://wt-journey-backend-01-etapa-1-oklu.onrender.com/


# Informações do Desafio: Protótipo de Cardápio Digital - DevBurger

Bem-vindo(a) ao desafio de desenvolvimento do protótipo de um cardápio digital para a nossa nova hamburgueria gourmet, a "DevBurger"!

O objetivo é criar uma aplicação web simples e funcional utilizando Node.js e Express. Nesta primeira fase, não nos preocuparemos com bancos de dados; toda a lógica de exibição e recebimento de dados será gerenciada diretamente pelo servidor.

## Visão Geral do Projeto

Este projeto consiste em um pequeno servidor web que apresenta o cardápio da hamburgueria e permite que os clientes enviem sugestões de novos lanches. É uma excelente oportunidade para praticar conceitos fundamentais de back-end com Node.js, como a criação de servidores, o gerenciamento de rotas e o tratamento de formulários.

## Estrutura de Arquivos

Para manter o projeto organizado, tente seguir a seguinte estrutura de diretórios e arquivos:

```bash
devburger/
├── public/
│   ├── css/
│   │   └── style.css
│   ├── images/
│   │    └── logo.png (opcional)
│   ├── data
│   │     └── lanches.json
│   └── 404.html (opcional)
│
├── views/
│   ├── index.html
│   └── contato.html        
│
├── .gitignore
├── package-lock.json
├── package.json
├── README.md
└── server.js
```

- **`public/`**: Contém todos os arquivos estáticos que serão servidos diretamente ao cliente, como folhas de estilo (CSS), imagens, arquivos JSON e scripts do lado do cliente.
- **`views/`**: Contém os arquivos HTML estáticos que serão servidos por cada endpoint.
- **`server.js`**: O coração da nossa aplicação, onde o servidor Express será configurado e todas as rotas serão definidas.
- **`package.json`**: Arquivo de manifesto do projeto Node.js, que inclui as dependências (como o Express).
- **`README.md`**: Este arquivo, com a documentação do projeto.

## Como Iniciar o Servidor

Siga os passos abaixo para configurar e rodar o projeto em sua máquina local.

**1. Crie o projeto seguindo a estrutura**

Clone o repositório e execute o seguinte comando: 

```npm init -y```

Depois, crie os repositórios e arquivos e diretórios seguindo a estrutura de exemplo.

**2. Instale as Dependências**

Navegue até o diretório raiz do projeto pelo terminal e instale o Express.js:

```bash
npm install express
```
Se você estiver recebendo os dados do formulário via POST, precisará de um middleware para interpretar o corpo da requisição. O Express já inclui o express.urlencoded.

**Observação:** não devem ser utilizadas outras dependências além do express, como template engines.

**3. Crie o servidor**

Insira este código no arquivo server.js

```
const express = require('express')

const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
    res.send("Hello World!");
});

app.listen(PORT, () => {
    console.log(`Servidor da DevBurger rodando em localhost:${PORT}`);
});
```

**4. Inicie o Servidor**

Execute o seguinte comando no terminal:

```bash
npm start
```

O servidor será iniciado, e você deverá ver uma mensagem no console, por exemplo:

Servidor da DevBurger rodando em http://localhost:3000

Agora, você pode abrir seu navegador e acessar http://localhost:3000. O texto "Hello World!" deverá ser exibido no seu navegador.

## Rotas Implementadas
A aplicação possui as seguintes rotas:

| Rota  | Descrição | Método | Status code esperado | Resposta | Observações |
| :----: | -------- | :------: | :--------------------: | ------ | ----------|
| Raíz ```/``` | Serve a página principal da aplicação (index.html), que exibe o cardápio da "DevBurger" e um formulário para que os clientes possam sugerir um novo sabor de lanche. | ```GET``` | ```200``` | arquivo index.html. | - |
| ```/sugestao``` | Recebe os dados enviados pelo formulário da página inicial. O servidor processa esses dados e exibe uma página de agradecimento personalizada. | ```GET``` | ```200``` | página de agradecimentos com os dados passados no formulário da rota raíz. | O envio do formulário deve ser feito utilizando query string, com os parâmetros ```nome``` e ```ingredientes ```|
| ```/contato``` | Serve a página de de contato (contato.html), que exibe um formulário para que os clientes possam enviar mensagens. | ```GET``` | ```200``` | arquivo contato.html. | - |
| ```/contato``` | Recebe os dados do cliente e do contato fornecidos no formulário da página de contato. O servidor processa esses dados e exibe a página de contato recebido. | ```POST``` | ```200``` | págna HTML gerada dinamicamente contendo os dados do cliente passados no formulário. | Exemplo de payload abaixo |
| ```/api/lanches``` | Uma rota de API simulada que retorna uma lista de lanches pré-definidos em formato JSON. Ideal para ser consumida por um futuro front-end dinâmico. | ```GET``` | ```200``` | retorna um JSON listando lanches, simulando uma API | Exemplo abaixo |

## Observações

### **1) Exemplo de URL com query string- Rota de Sugestão:**  

```/sugestao?nome=Banh+mi&ingredientes=pao,vegetais,frango```

### **2) Payload do envio de contato:** 

**JSON**
```
{
  "nome": "Tram Anh Nguyen",
  "email": "tramanh@gmail.com",
  "assunto": "Sugestão de Evento",
  "mensagem": "Gostaria de sugerir que vocês organizassem um evento de degustação de novos lanches!"
}
```

- **Corpo da requisição (Payload):**
   - nome (String): nome do cliente
   - email (String): e-mail do cliente
   - assunto (String): assunto do contato
   - mensagem (String): mensagem explicando o motivo do contato
       
### **3) Retorno da API de lanches:** 

O endpoint /api/lanches deverá retornar um JSON com a seguinte estrutura:

**JSON**
```
[
  {
    "id": 1,
    "nome": "DevBurger Clássico",
    "ingredientes": "Pão brioche, Carne 150g, Queijo cheddar, Alface americana, Tomate fresco, Molho especial"
  },
  {
    "id": 2,
    "nome": "Burger de Bacon",
    "ingredientes": "Pão australiano, Carne 180g, Queijo prato, Bacon crocante, Cebola caramelizada, Molho barbecue"
  },
  {
    "id": 3,
    "nome": "Commit Veggie",
    "ingredientes": "Pão integral, Burger de grão de bico, Queijo vegano, Rúcula, Tomate seco, Maionese de ervas"
  }
]
```

A resposta deve conter uma lista com no mínimo 3 lanches e cada lanche deve possuir os mesmos atributos exibidos acima.

## Views:
Deverão ser implementadas as seguintes views com as seguintes especificações:

| Página | Descrição | Requisitos | Observações |
| :------: | --------- | ---------- | ----------- |
| index.html | Template exibido na rota raíz ```/```. | deve possuir, pelo menos, um formulário com os campos ```nome``` e ```ingredientes``` (utilize tags ```<input>``` ou ```<textarea>```) e um botão de tipo submit, além de âncoras (tag <a>) para a rota de contato ```/contato``` e para a API simulada ```/api/lanches```. Layout e estilização ficam ao seu critério.| é altamente recomendado o uso da tag label e atributos de ID, juntamente com os campos do formulário. |
| Página de agradecimento | Template exibido após uma requisição ```GET``` à ```/sugestao```. | Deverá exibir uma mensagem de agradecimento pela sugestão e os dados inseridos no formulário durante seu envio, presente nos parâmetros da URL. | - |
| contato.html | Template exibido após uma requisição ```GET``` à ```/contato``` | Deve conter um formulário com os campos de ```nome```, ```email```, ```assunto``` e ```mensagem```, um botão do tipo "submit" e uma âncora (tag <a>) para à rota raíz ```/```. | É altamente recomendado o uso da tag label e IDs, juntamente com os campos do formulário. |
| Página de contato | Template exibido após uma requisição ```POST``` à ```/contato``` | Deve exibir uma mensagem de agradecimento pela mensagem, os dados passados no formulário da página ```contato.html``` e possuir uma âncora para a rota raíz ```/``` | - |
| 404.html (opcional) | Template exibido quando uma rota não existente é acessada. | Deve conter uma mensagem de erro qualquer e uma âncora para a rota raíz ```/```  | - |

## Opcional:

### Tratamento de Página Não Encontrada (Erro 404)
- Foi implementado um middleware no final da cadeia de rotas em server.js.

- Se uma requisição chegar ao servidor e não corresponder a nenhuma das rotas definidas (/, /sugestao, /contato, /api/lanches), o servidor responderá com um status 404 e uma página de erro amigável, informando ao usuário que a página não foi encontrada.

### Uso do padrão PRG (POST, REDIRECT, GET)

- Ao realizar a requisição ```POST /contato``` o servidor recebe o payload, o processa e retorna uma ordem de redirecionamento para a rota ```/contato-recebido```.

- O servidor realiza a ordem com uma requisição ```GET``` para a rota especificada, servindo a página de ```/contato-recebido```.

- Dica: não armazene estado no servidor.

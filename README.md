<h1>🚀 Sobre o desafio</h1>
<p>Nesse desafio, você deve continuar desenvolvendo a aplicação de gestão de transações, treinando o que você aprendeu até agora no Node.js junto ao TypeScript, mas dessa vez incluindo o uso de banco de dados com o TypeORM e envio de arquivos com o Multer!
Essa será uma aplicação que deve armazenar transações financeiras de entrada e saída e permitir o cadastro e a listagem dessas transações, além de permitir a criação de novos registros no banco de dados a partir do envio de um arquivo csv.</p>
<br>
<h1>Rotas da aplicação</h1>
<br>
<p><strong>POST /transactions</strong>: A rota deve receber title, value, type, e category dentro do corpo da requisição, sendo o type o tipo da transação, que deve ser income para entradas (depósitos) e outcome para saídas (retiradas). Ao cadastrar uma nova transação, ela deve ser armazenada dentro do seu banco de dados, possuindo os campos id, title, value, type, category_id, created_at, updated_at.
<br><br>
<strong>Dica 1:</strong> Para a categoria, você deve criar uma nova tabela, que terá os campos id, title, created_at, updated_at.

<strong>Dica 2:</strong> Antes de criar uma nova categoria, sempre verifique se já existe uma categoria com o mesmo título. Caso ela exista, use o id já existente no banco de dados.</p>
<p>{
  "id": "uuid",
  "title": "Salário",
  "value": 3000,
  "type": "income",
  "category": "Alimentação"
}</p>
<p><strong>GET /transactions:</strong> Essa rota deve retornar uma listagem com todas as transações que você cadastrou até agora, junto com o valor da soma de entradas, retiradas e total de crédito. Essa rota deve retornar um objeto o seguinte formato:</p>
<p>{
  "transactions": [
    {
      "id": "uuid",
      "title": "Salário",
      "value": 4000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Salary",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Freela",
      "value": 2000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Pagamento da fatura",
      "value": 4000,
      "type": "outcome",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Cadeira Gamer",
      "value": 1200,
      "type": "outcome",
      "category": {
        "id": "uuid",
        "title": "Recreation",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    }
  ],
  "balance": {
    "income": 6000,
    "outcome": 5200,
    "total": 800
  }
}</p>
<p><strong>Dica 1:</strong> Dentro de balance, o income é a soma de todos os valores das transações com type income. O outcome é a soma de todos os valores das transações com type outcome, e o total é o valor de income - outcome.</p>

<p><strong>Dica 2:</strong> Para fazer a soma dos valores, você pode usar a função reduce para agrupar as transações pela propriedade type, assim você irá conseguir somar todos os valores com facilidade e obter o retorno do balance.</p>
<p><strong>DELETE /transactions/:id:</strong> A rota deve deletar uma transação com o id presente nos parâmetros da rota;</p>
<p><strong>POST /transactions/import:</strong> A rota deve permitir a importação de um arquivo com formato .csv contendo as mesmas informações necessárias para criação de uma transação id, title, value, type, category_id, created_at, updated_at, onde cada linha do arquivo CSV deve ser um novo registro para o banco de dados, e por fim retorne todas as transactions que foram importadas para seu banco de dados. O arquivo csv, deve seguir o seguinte <a href="https://github.com/rocketseat-education/bootcamp-gostack-desafios/blob/master/desafio-database-upload/assets/file.csv"</a>modelo</p>
<h1>Específicação dos testes</h1>
<p>Em cada teste, tem uma breve descrição no que sua aplicação deve cumprir para que o teste passe.</p>
<p>Para esse desafio, temos os seguintes testes:</p>
<p align="center">⚠️ <strong>Antes de rodar os testes, crie um banco de dados com o nome "gostack_desafio06_tests" para que todos os testes possam executar corretamente</strong> ⚠️</p>
<ul>
<li><p><strong>should be able to create a new transaction:</strong> Para que esse teste passe, sua aplicação deve permitir que uma transação seja criada, e retorne um json com a transação criado.</p>
</li>
<li><p><strong>should create tags when inserting new transactions:</strong> Para que esse teste passe, sua aplicação deve permitir que ao criar uma nova transação com uma categoria que não existe, essa seja criada e inserida no campo category_id da transação com o id que acabou de ser criado.</p>
</li>
<li><p><strong>should not create tags when they already exists:</strong> Para que esse teste passe, sua aplicação deve permitir que ao criar uma nova transação com uma categoria que já existe, seja atribuído ao campo category_id da transação com o id dessa categoria existente, não permitindo a criação de categorias com o mesmo title.</p>
</li>
<li><p><strong>should be able to list the transactions:</strong> Para que esse teste passe, sua aplicação deve permitir que seja retornado um array de objetos contendo todas as transações junto ao balanço de income, outcome e total das transações que foram criadas até o momento.</p>
</li>
<li><p><strong>should not be able to create outcome transaction without a valid balance:</strong> Para que esse teste passe, sua aplicação não deve permitir que uma transação do tipo outcome extrapole o valor total que o usuário tem em caixa (total de income), retornando uma resposta com código HTTP 400 e uma mensagem de erro no seguinte formato: { error: string }.</p>
</li>
<li><p><strong>should be able to delete a transaction:</strong> Para que esse teste passe, você deve permitir que a sua rota de delete exclua uma transação, e ao fazer a exclusão, ele retorne uma resposta vazia, com status 204.</p>
</li>
<li><p><strong>should be able to import transactions:</strong> Para que esse teste passe, sua aplicação deve permitir que seja importado um arquivo csv. Com o arquivo importado, você deve permitir que seja criado no banco de dados todos os registros e categorias que estavam presentes nesse arquivo, e retornar todas as transactions que foram importadas.</p>
</li>
</ul>
<h1>📆 Entrega</h1>
<p>Esse desafio deve ser entregue a partir da plataforma da Rocketseat, envie o link do repositório que você fez suas alterações. Após concluir o desafio, fazer um post no Linkedin e postar o código no Github é uma boa forma de demonstrar seus conhecimentos e esforços para evoluir na sua carreira para oportunidades futuras.</p>

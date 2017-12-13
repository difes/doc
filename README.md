Dife
=======

Com o painel Dife seu cliente terá um site com o conteúdo totalmente gerenciável sem que você precise programá-lo. Basta fazer o front-end conforme o desejo do cliente, cadastrar o site no painel Dife e fazer a integração de forma simples.

Utilizando o painel Dife na criação dos sites, você:

 * Não precisa de servidor com suporte à PHP, Python, Rails, etc;
 * Não precisa de banco de dados;
 * Não precisa de servidor e-mails para enviar formulários;
 * Basta criar o site com HTML e CSS e integrar.


Quickstart
---------------

Deixe o conteúdo do seu front-end totalmente gerenciável com apenas 3 passos:

 * Crie um conta no Dife;
 * Cadastre as funcionalidades desejadas;
 * Use nossa API para consulta as informações cadastradas.


### Criar um Conta Dife

Acesse o painel de controle Dife atráves [deste link](https://dife.com.br/register), cadastre-se e crie um site.


### Criar Funcionalidades


No painel de controle, acesse o menu [Funcionalidades](https://dife.com.br/features) e clique no botão *Adicionar* para cadastrar funcionalidades.


### Consumindo a API

No código fonte do seu site, importe a nossa biblioteca [javascript](#bibliotecas-javascript). Informe a chave pública do seu site.

``` javascript
var dife = new Dife('CHAVE_PUBLICA_SITE');

dife.listFeatures(function (response) {
  for (var i = 0; u < response.data.length; i++) {
    document.getElementById('features').innerHTML += '<p>'+ response.data[i].name +'</p>';
  }
});
```

O método `listFeatures()` retorna a lista das funcionalidades cadastradas. O método `listValues(ID)` retorna a lista dos conteúdos cadastrados na funcionalidade com `ID` correspondente.

``` html
<div id="features"></div>
```

Você pode exibir os dados da maneira que desejar, utilizando a biblioteca de manipulação DOM que desejar. Nos exemplos acima utilizamos javascript, mas você pode utilizar jQuery, Angular, Ember, etc.


### Enviando um Formulário


``` javascript
var dife = new Dife('CHAVE_PUBLICA_SITE');

var ID = 10;
var DADOS = {
  nome: 'João Paulo',
  email: 'joao.paulo@gmail.com',
  mensagem: 'Isso é apenas um teste'
};

dife.form(ID, DADOS, function (response) {
  // sucesso
}, function (response) {
  // erro
  console.log(response.data.erros);
});
```

No exemplo acima, a variável `ID` é um identificador do formulário. A variável `DADOS` é um objeto com o slug do campo do formulário e o valor que deseja enviar.

O método `form()` recebe até quatro parâmetros: o identificador do formulário, os dados, o callback de sucesso e callback de erro.

Painel de Controle Dife
---------------

O painel de controle Dife é o local onde o webdesigner cadastra o site, define as funcionalidades que existirão e cadastra os clientes. O cliente irá acessar o painel de controle para criar, editar ou excluir publicações, de acordo com as permissões.


### Cadastro de Funcionalidades

Para cadastrar uma funcionalidade, acesse a opção *Funcionalidades* no menu.

![enter image description here](https://user-images.githubusercontent.com/146581/33672371-d5e39cb2-da88-11e7-8fae-b7af1b46d5ae.jpg)

![enter image description here](https://user-images.githubusercontent.com/146581/33672373-d606f9aa-da88-11e7-9bd8-a5a02764c917.jpg)

Clique no botão *Adicionar*. No formulário, clique no botão *Adicionar Campo*. Você pode definir as regras de cada campo, como:

 * **Tipo do Campo:** define o tipo (texto curto, texto longo, inteiro, decimal...);
 * **Rótulo do Campo:** o rótulo que será exibido na hora de preencher o campo;
 * **Tamanho Mínimo:** o tamanho mínimo do preenchimento do campo. Por exemplo 10, não permite que seja inserido um texto com 10 de caracteres;
 * **Tamanho Máximo:** o tamanho máximo do preenchimento do campo;
 * **Expressão Regular:** caso queira fazer uma validação específica. Lembrando que já possuímos campos como data e hora;
 * **Texto de Ajuda:** um texto com mais detalhes sobre o preenchimento do campo;
 * **Campo Obrigatório:** se marcado, o campo fica sendo de preenchimento obrigatório.

Se a opção **Usuários comuns poderão somente editar conteúdos?** for marcada, os usuários que não forem administrador, não poderão adicionar ou excluir conteúdos da funcionalidade. Eles poderão apenas editar conteúdos. Isso pode ser definido para cada funcionalidades.

Após o cadastro da funcionalidade, ela irá aparecer no menu ao lado para que possa cadastro conteúdos nela. Você pode ordenar as funcionalidades, isso influência apenas na ordem em que ela irão aparecer no menu.


### Cadastro de Usuários

Caso esteja criando um site para algum cliente, você pode cadastrá-lo para que ele possa gerenciar o conteúdo. Para cadastrar um usuário, acesse a opção *Usuários* no menu.

![enter image description here](https://user-images.githubusercontent.com/146581/33672374-d65740fe-da88-11e7-898f-245805ecb8f0.jpg)

Clique no botão *Adicionar* e preencha o formulário.

Se o usuário cadastrado for marcado como **administrador**, ele poderá gerenciar outros usuários e funcionalidades. Se essa opção não for marcada, ele poderá apenas gerenciar conteúdos.


Chave de acesso
---------------

Para utilizar a API no front-end, você precisa de uma chave pública de seu site. A chave é que identifica seu site e dá permissão para retornar os conteúdos. Como as informações são públicas, a chave também é pública.

Para obter uma chave, basta acessar o painel de controle e ir em [Configurações](https://dife.com.br/sites/edit).

![enter image description here](https://user-images.githubusercontent.com/146581/33672370-d5c46bb2-da88-11e7-9659-8623c2df00e0.jpg)


Bibliotecas
=======

Criamos bibliotecas para facilitar sua integração do painel Dife com o site de seu cliente. Elas estão disponíveis de forma open-source no nosso [GitHub](https://github.com/difepanel/).


Javascript
---------------

Você tem várias opções de instalação da nossa biblioteca Javascript:

Via Bower:

```
bower install dife-js --save
```

Utilizando direto de nosso servidor:

```html
<script src="https://dife.com.br/assets/js/dife-0.0.6.min.js"></script>
```

Você pode baixar o arquivo:

[Baixar >][download]

[download]: https://dife.com.br/assets/js/dife-0.0.6.min.js

### Métodos

A biblioteca Javascript possui alguns métodos.

#### listFeatures()

O método `listFeatures()` retorna uma lista com as funcionalidades cadastradas no site. Para utilizá-lo é necessário criar um instância do objeto `Dife`.

``` javascript
var dife = new Dife('CHAVE_PUBLICA_SITE');

dife.listFeatures(function (response) {
  // sucesso
});
```

Parâmetros:

| Parâmetro | Tipo     | Descrição                                  |
|-----------|----------|--------------------------------------------|
| sucesso   | function | Função a ser executada em caso de sucesso. |
| erro      | function | Função a ser executada em caso de erro.    |


#### listValues()

O método `listValues()` retorna uma lista (com paginação) dos registros de uma determinada funcionalidade. Para utilizá-lo é necessário criar um instância do objeto `Dife`.

``` javascript
var dife = new Dife('CHAVE_PUBLICA_SITE');

dife.listValues(id, function (response) {
  // sucesso
});
```

Parâmetros:

| Parâmetro | Tipo     | Descrição                                  |
|-----------|----------|--------------------------------------------|
| id        | int      | ID da funcionalidade.                      |
| sucesso   | function | Função a ser executada em caso de sucesso. |
| erro      | function | Função a ser executada em caso de erro.    |
| pagina    | int      | Página (quando houver muitos resultados).  |


#### form()

O método `form()` envia os dados para o preenchimento de um determinado formulário. Para utilizá-lo é necessário criar um instância do objeto `Dife`.

``` javascript
var dife = new Dife('CHAVE_PUBLICA_SITE');

dife.form(id, object, function (response) {
  // sucesso
});
```

Parâmetros:

| Parâmetro | Tipo     | Descrição                                                                                                                                                                            |
|-----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id        | int      | ID da funcionalidade.                                                                                                                                                                |
| dados     | object   | Objeto contendo os dados. Cada propriedade deve ser o slug do campo com o valor a ser enviado. Por exemplo, o campo "Nome Completo" ficaria `{nome_completo: 'João Paulo da Silva'}` |
| sucesso   | function | Função a ser executada em caso de sucesso.                                                                                                                                           |
| erro      | function | Função a ser executada em caso de erro.                                                                                                                                              |


#### template()

O método `template()` é utilizado para facilitar a renderização, caso você não utilize alguma biblioteca/framework que já possuia (como AngularJS). É um método estático, portando não deve ser chamado via intância, por não necessitar da chave.

Parâmetros:

| Parâmetro | Tipo           | Descrição                                                                                                 |
|-----------|----------------|-----------------------------------------------------------------------------------------------------------|
| id        | string         | ID do elemento HTML que possui o template. Por exemplo `<script type="text/dife" id="EXAMPLE"></script>`. |
| objeto    | object, array | Objeto que será usado no template.                                                                        |


``` javascript
var object = {
  titulo: 'Título de exemplo',
  descricao: 'Descrição de exemplo'
};

var html = Dife.template('EXAMPLE', object);
document.getElementById('local').innerHTML = html;
```


Template HTML:

``` html
<div id="local"></div>

<script type="text/dife" id="EXAMPLE">
  <div>
    <h2>{{ titulo }}</h2>
    <p>{{ descricao }}</p>
  </div>
</script>
```

O template deve estar dentro da tag `<body>`. Utilizamos a tag `<script>` com o atributo `type="text/dife"` é ignorado pelo navegador. Ao utilizar a função `Dife.template()` você deve adicionar o HTML gerado na página.
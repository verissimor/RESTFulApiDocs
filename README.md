# RESTFulApiDocs
Udemy | Entendendo e documentando REST / RESTful APIs | Jackson Pires

## Aula 3
- Resource: "Coisas" que podem ser manipuladas por id. Frequentemente um substantivo. Ex.: /usuario/ ou /venda/
- URI: Identificador unico na internet de um recurso. Ex.: meusite.com.br/usuario/
- URL: Localizador padrão de recursos. É o endereço completo. Ex.: http://meusite.com.br/usuario/
- URN: Usa URN Scheme. Ainda é uma RFC (2141). Na prática não é usado.
- IRI: Identificador de recurso internacionalizado. É uma URI com suporte a caracteres especiais.

## Aula 4 - O que é REST
Em inglês REST, significa Representational State Transfer, cujo tradução, Transferência de Estado Representacional.

Resultado de uma tese de doutorado de Roy Fielding, um dos principais autores da especificação do protocolo http. O intuito geral era a formalização de melhores práticas (contraints). Criando padrões para http e uri.

*Client/Server* <br/>
Cliente servidor: permite escalar front/back ends de forma independente.

*Stateless* <br/>
Cada requisição ao servidor não deve ter ligação com requisições anteriores ou futuras. Ou seja, não deve guardar sessão, autorizações e outros states da aplicação.

*Cache* <br/>
Permitir que as respostas sejam passíveis de cache.

*Interface Uniforme* <br/>
Exige que bastante esforço seja feito com interface semelhante. Entidade: cliente; Operações {criar, editar, deletar, pesquisar}

*Sistema em camadas* <br/>
A ideia é que possam ser adicionados novos recursos (como por exemplo um load balancer) de forma transparente para o usuário.

*Código sob demanda* <br/>
Um código que é carregado somente quando uma página é acessada. A única contraint opcional.


## Aula 5 - Diferença entre REST e RESTful
Rest é um conjunto de melhores práticas. RESTful é uma API que implementa os princípios rest. Caso uma api não implemente tais conceitos, ela torna-se apenas uma api http.

*Representações* <br/>
São as formas de retorno. Ex.:<br/>
```javascript
[cliente] => get {"/cliente/1"; "Accept: application/json"} => [servidor] => {"nome": "João da Silva"}
[cliente] => get {"/cliente/1"; "Accept: image/jpeg"} => [servidor] => {imagem}
```

*Principais representações*<br/>
- Json ```javascript {"nome": "João"}```
- Xml ```xml <?xml version="1"?><nome>João</nome>```

## Aula 6 - REST vs SOAP
 Rest | SOAP 
 -----|------
É um modelo arquitetural |  É um protocolo.
Rest requisições http simples| SOAP envolopado no HTTP para fazer RPC (Remote procedure call)
Rest suporta vários formatos (xml, json, yaml, etc)| Somente XML.

## Aula 7 cURL
https://onlinecurl.com

-H: atalho para Header. Exemplo: -H "Content-Type: application/json"
-d: atalho para data. Enviar dados para o servidor. Ex.: -d '{"name": "joao"}'
-i: ou -include. Faz o curl retornar tbm o cabeçalho da requisição 
-I: ou -head. Traz somente o cabeçalho
-X: ou -request específica qual será o verbo da requisição. Por padrão será get. Mas pode ser post, put, patch ou delete. 
-v: verboso, vai retornar todos os detalhes da requisição 

curl --help 

## aula 8 Resposta http 
1 start-line:linha de início (obrigatória) 
2 header fields: cabeçalhos de campos (0 ou mais) 
3 empty line: linha em branco obrigatório 
4 message body: corpo da mensagem opcional 

## aula 9 Métodos http (verbos) 
Na especificação original, http 1.0, eram apenas get, post e head. Na revisão 1.1, foi incluído options, put, delete, trace e connect. A rfc 5789, adiciou patch. 

Get: quando existe a necessidade de obter dados de um recurso. Idepotente, ou seja, independente de quantas requisições, o resultado deve ser o mesmo. curl - X GET

Post: usado para criar um recurso. curl - X POST

Put: serve para fazer update em um recurso. 

Delete: apaga um recurso

## Aula 10 Outros Métodos http
Head: retorna somente o cabeçalho

Patch: atualiza de forma parcial um recurso. Exemplo, atualiza somente a idade de um usuário

Options: saber quais métodos estão disponíveis para um recurso. Access-Control-Allow-Headers. 

Connect: permite a criação de um túnel
 
 #Aula 11 Safe methods 
 Métodos que não alteram dados. Ex. Get e head 
 
 É os métodos idempotentes não alteram nada após a segunda requisição. Ex. 10 requisições Get resultam de forma igual a apenas uma. São : Get, head, put, delete, options e trave. 
 
 ## Modelo de maturidade Richardson 
*Aula 12*
 
Muitas vezes precisamos de mais simplicidade ao invés de alcançar todos os níveis. 
 
Nível 0: Pox. As mensagens são em XML ou json. Mas não segue os padrões de uri proposto no rest. Ex: /salvarCliente. As respostas tbm não usam os códigos de start line. Ex. HTTP/1.1 200, {"status" : "erro"} 

*Aula 13* <br />
Nível 1: Recursos. Recursos (pessoas, clientes) são a base de modelar e organizar a API. No Nível "agora temos recursos". Utiliza verbos, mas, as respostas ainda não são com os status http corretos. Geralmente utiliza POST ou GET.
 
Nível 2: verbos HTTP. Neste nível o http deixa de exercer um papel semântico na API e os verbos passam a ser utilizados com o propósito o qual foram criados. Nesse nível, por exemplo, ao enviar um POST com dados de cliente, o sistema retorna um header HTTP 1.1 201 Created. Também é adicionado um header location ex. "Location: /cliente/1".

Status codes:
https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status

 Nível 3: HATEOAS. Significa "Hypermedia as the Engine of Application State". Segundo Roy Fielding, se não estiver nesse estado, não pode ser considerado RESTful. Na prática, um objeto retornado deve conter os links para outros possíveis estados. Ex.: 
{
  "id": "1", 
  "nome": "João", 
  "links" : [ 
    {"rel": "self", "href": "/clientes/1"}, 
    {"rel": "deletar", "href": "/clientes/1"}, 
    {"rel": "notificar", "url": "/clientes/1/notificar"} 
  ]
}

https://martinfowler.com/articles/richardsonMaturityModel.html


Em resumo

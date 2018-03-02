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


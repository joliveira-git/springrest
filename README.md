# Resumão Projeto API Spring REST
API REST escrita em Java utilizando Spring MVC

Relembrando os conceitos de REST e consolidando os conhecimentos em alguns projetos Spring

Starters do Spring Boot utilizados no projeto:
 - Spring Boot DevTools
 - Spring Data JPA
 - MySQL Driver
 - Spring Web
 - FlyWay Migration

#  Persistência de Dados, Bean Validation e Exception Handler

Tecnologias: 
 - Spring Data JPA
 - Flyway: Ferramenta de controle de versão de banco de dados.
 - Hibernate implementação Jakarta Persistence do projeto Jakarta EE (antigo JPA do JAVA EE). 
 - Jakarta Bean Validation: Validação de entrada de dados
 - modelmapper biblioteca para o mapeamento do modelo de domínio para o modelo representacional


# Spring REST

Principais tecnologias utilizadas:
Ferramentas:
    - Java 11.0
    - Spring Tool Suite: IDEs (Eclipse, Visual Studio Code, e outras) já preparadas para trabalhar com projetos Spring
    - MySql: Banco de Dados e ferramenta de administração MySql Workbench
    - Postman: Cliente REST para simular as requisições HTTP
    - Maven: Gerenciamento de dependências e automação de build
    - Lombok: Framework usado para reduzir código boilerplate
Projetos Spring:
    - Spring Boot
    - Spring MVC


# REST API

Application Programming Interface: intermediação do acesso a funcionalidades
Expor funcionalidades

  Consumidor <-> API <-> Provedor

  Web Services x API
  Web Services: Web API

# REST: Representation State Transfer
  Estilo arquitetural usado para desenvolver Web APIs

  Roy Fielding
  Melhores práticas: constraints

Por que usar REST?

  - Separação cliente e Servidor: maior flexibilidade e portabilidade
  - Escalabilidade
  - Independente de linguagem de programação

# Constraints:
  - Cliente-servidor: cliente aplicação front ou mobile que envia informações ao servidor via API. Um cliente ou servidor pode ser substituído sem interferir em nada

  - Stateless: aplicação não deve possuir um estado. A requisição deve conter tudo o que precisa para ser processado. um servidor não pode manter uma sessão

  - Cache: manter cache de dados. Ex.: lista das cidades
  Redução de hits (acessos) ao servidor.

  - Interface uniforme: conjunto de operações bem defnidas do sistema. Desacopla a arquitetura o que permite que 

cada parte evolua de forma independente.
Padronizar: 
    - Definir os recursos da aplicação
    - Definir um conjunto de operações possíveis sobre os recursos
    - Utilizar um padrão de protocolo de comunicação (HTTP)
    - resposta de uma requisição deve ser padronizada (definir o formato dos dados)
Sistema em camadas: Entre um cliente e um servidor, podem existir outros servidores para prover camada de segurança, cache, balanceamento de carga
- Código sob demanda (pouco usado)

# Protocolo HTTP

  Métodos (Verbos) HTTP:
  GET
  POST
  UPDATE
  DELETE

# Requisição / Resposta

Requisição:
  Método: Verbo (Semântica)
  URI: Caminho que identifica o recurso que queremos no servidor
  Versão
  Cabeçalho: Ex.: Content-Type (tipo de conteúdo a ser enviado), Accept (tipos de conteúdo aceitos como resposta)
  Corpo (Payload)

  JSON: 
  Javascript Object Notation
  Formato para transporte de dados

Resposta:
  Protocolo utilizado: HTTP
  Versão
  Status: 
  Cabeçalho: Location: /produtos/331, Content-Type: application/json
  Corpo:

  Singleton Resource
  Collection Resource

  URI - Uniforme Resource Identifier: substantivo (no plural). Coisas possuem propriedades e verbos não.
  URL - Uniforme Resource Locator: identifica o recurso e diz como chegar até ele.

  Recurso: URI
  Ação: métodos HTTP

  https://api.algamarket.com.br/produtos/331

Spring REST
-----------

REST API desenvolvida com um projeto Spring

Spring: ecosistema

spring.io
Projects / overview

Spring Framework: projeto de base para os demais projetos. Funcionalidades: Spring MVC, Core (base, injeção de dependência) Container de injeção de dependências. Transações e acesso a dados

Spring Data: Projeto guarda-chuva: Spring Data JPA(eliminar código Código boiler plate da camada de persistência de dados), JDBC, MongoDB, Redis, dentre outros

Spring Boot: ajuda a criar projetos fazendo as configurações iniciais.

Spring IO
- Starter adiciona um conjunto de dependências no projeto. Auto-configura o projeto para usar as dependências instaladas.
    IDEs não Spring Tool Suite: start.spring.io: permite gerar o esqueleto de projetos
- Download das dependências do maven
    Maven / Update Project / v Force Update Snapshot Releases

    pom.xml: project object model
    <parent> onde configura a herança do pom com as configurações do spring-boot.
    <artifactId>spring-boot-starter-parent</artifactId>

    versão do Java:
    <properties>
        <java.version>11</java.version>
    <properties>

    spring-boot-starter-web
        + dependencias transitivas:
        spring-boot-starter
        spring-boot-starter-json
        spring-boot-starter-tomcat
        sprint-boot-starter-validation
        spring-web (depedência Spring MVC)
            spring-beans
            spring-core
        spring-webmvc

Gerar um jar para produção:
  Run As / Maven build / Goals: clean package

  O .jar é criado na pasta target
  Na verdade é gerado um fat jar que já possui um container sevlet (por padrão TomCat na porta 8080) que é inicializado automaticamente ao rodar a aplicação.


Para executar:
    java -jar arquivo.jar

No Spring Tool Suite: 
    Boot Dashboard

end-point
serviço REST

Postman:
- Criar coleção
- Criar uma nova requisição

# Rest Controller

Criar a classe controller que vai receber as requisições HTTP:
  ```
  @RestController
  public class ClienteController{

      @GetMapping("/clientes")
      public String listar(){
          var cliente1 = new Cliente();
          ...
          var cliente2 = new Cliente();
          ...
          return Arrays.asList(cliente1, cliente2);
      }

  }
```

Criar a classe que vai representar a entidade:
```
  public class Cliente {

      private Long id;
      private String nome;
      private String email;
      private String telefone;

      getter and setters
  }
```

Para evitar código boilerplate recomenda-se o uso do framework Lombok.
Lombok: 
O Lombok é uma biblioteca Java focada em produtividade e redução de código boilerplate que por meio de anotações adicionadas ao nosso código ensinamos o compilador (maven ou gradle) durante o processo de compilação a criar código Java.

Ref.: https://medium.com/collabcode/projeto-lombok-escrevendo-menos-c%C3%B3digo-em-java-8fc87b379209

Exemplo de anotações Lombok:
  ```
  @Entity
  @NoArgsConstructor @AllArgsConstructor 
  @ToString(exclude="id")
  @EqualsAndHashCode(exclude={"firstName", "lastName", "gender"})
  public class User {

      @Id @GeneratedValue
      @Getter private Long id; 
      @Getter @Setter private String firstName;
      @Getter @Setter private String lastName;
      @Getter @Setter private String email;
      @Getter @Setter private Date age;
      @Getter @Setter private String gender;
  }
  ```

Testar a requisição no Postman:
Array ([]) de Objetos ({}) JSON: Representação de um recurso é algo que representa o estado atual do mesmo
O método HTTP possui a semântica da operação que será usada para trabalhar com o recurso, ou seja o tipo de ação que será executada com o recurso.
Requisição GET é idempotente, pois repetidas requisições não geram efeito colateral

#Códigos HTTP
Referência:
https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml
  https://httpstatuses.com/
  ```
  1×× Informational
      100 Continue
      101 Switching Protocols
      102 Processing
  2×× Success
      200 OK
      201 Created
      202 Accepted
      203 Non-authoritative Information
      204 No Content
      205 Reset Content
      206 Partial Content
      207 Multi-Status
      208 Already Reported
      226 IM Used
  3×× Redirection
      300 Multiple Choices
      301 Moved Permanently
      302 Found
      303 See Other
      304 Not Modified
      305 Use Proxy
      307 Temporary Redirect
      308 Permanent Redirect
  4×× Client Error
      400 Bad Request
      401 Unauthorized
      402 Payment Required
      403 Forbidden
      404 Not Found
      405 Method Not Allowed
      406 Not Acceptable
      407 Proxy Authentication Required
      408 Request Timeout
      409 Conflict
      410 Gone
      411 Length Required
      412 Precondition Failed
      413 Payload Too Large
      414 Request-URI Too Long
      415 Unsupported Media Type
      416 Requested Range Not Satisfiable
      417 Expectation Failed
      418 I'm a teapot
      421 Misdirected Request
      422 Unprocessable Entity
      423 Locked
      424 Failed Dependency
      426 Upgrade Required
      428 Precondition Required
      429 Too Many Requests
      431 Request Header Fields Too Large
      444 Connection Closed Without Response
      451 Unavailable For Legal Reasons
      499 Client Closed Request
  5×× Server Error
      500 Internal Server Error
      501 Not Implemented
      502 Bad Gateway
      503 Service Unavailable
      504 Gateway Timeout
      505 HTTP Version Not Supported
      506 Variant Also Negotiates
      507 Insufficient Storage
      508 Loop Detected
      510 Not Extended
      511 Network Authentication Required
      599 Network Connect Timeout Error
```

# Dev Tools
Live reload

Btn Dir / Spring / Add Dev Tools / 
 Adiciona dependencia spring-boot-devtools no pom.xml

# Content Negotiation

No cabeçalho da requisição:
Key             Value
---             -----
Accept          application/json*
                application/xml

*application contents

Para fazer content negotiation deve-se acrescentar a dependência do framework jackson no pom.xml
```
  <dependency>
      <groupId>com.fasterxml.jackson.dataformat</groupId>
      <artifactId>jackson-dataformat-xml</artifactId>
  Biblioteca utilizada para serializar e deserializar objetos
  </dependency>
```  

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>> REVISAR O TEXTO A PARTIR DAQUI

Adicionar dependência para conexão com banco de dados
Btn Dir Projeto / Spring / Add Starter / 
 - Spring Data JPA
 - MySQL Driver

Configurar a conexão em src/main/resources

application.properties:

spring.datasource.url=jdbc:mysql://localhost:3306/osworks?createDatabaseIfNotExist=true&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=masterkey

# Keep the connection alive if idle for a long time (needed in production)
spring.datasource.testWhileIdle = true
spring.datasource.validationQuery = SELECT 1

# Show or not log for each sql query
spring.jpa.show-sql = true

# Hibernate ddl auto (create, create-drop, update)
spring.jpa.hibernate.ddl-auto = update

# Naming strategy
spring.jpa.hibernate.naming-strategy = org.hibernate.cfg.ImprovedNamingStrategy

# Use spring.jpa.properties.* for Hibernate native properties (the prefix is
# stripped before adding them to the entity manager)

# The SQL dialect makes Hibernate generate better SQL for the chosen database
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5Dialect


Utilização FlyWay
-----------------
criar a pasta db/migration (osworks-api / src / main / resources / db / migration)
* se não compilar, basta cria um arquivo na pasta migration.

Criar um arquivo de script com nome V001__cria-tabela-cliente.sql
Ficar atento a regra de nome para versão: 
Version may only contain 0..9 and . (dot). Invalid version: 001.cria.tabela.cliente

O nome do arquivo tem que ser V1__QUALQUERNOME.sql.
São 2 underscore. Se seu banco mudou, você precisa ter um V2, e assim por diante

Ao rodar a aplicação o FlyWay irá criar uma tabela de controle de versão do banco:
flyway_schema_history

# Criar tabela no MySql
No Workbench 
Selecionar o banco de dados: Btn dir no Schema / Set As Default Schema
create table cliente (
    id bigint not null auto_increment,
    nome varchar(60) not null,
    email varchar(255) not null,
    telefone varchar(20) not null,
    primary key (id)
);


Verificar se o script foi aplicado com sucesso para em seguida excluir a tabela (DROP)
Copiar o script para o flyway. Ao salvar, irá obter o seguinte erro: Migration checksum mismatch for migration version 001
Um script que já foi executado não pode ser executado novamente.

No exemplo, basta excluir o registro de controle na tabela flyway_schema_history (delete rows / apply), mas na prática deve-se gerar um novo arquivo de script trocando o número da versão.

V001__cria-tabela-cliente.sql
alter table cliente change column telefone fone VARCHAR(20) not null;

JPA
 - spring-boot-starter-data-jpa
    + jakarta.persistence-api (especificaçao JPA)
    + hibernate-core (implementação JPA)

    spring-data-jpa (biblioteca para ajudar a criar repositórios, não é uma implementação JPA)

Mapeamento Objeto-Relacional

Spring Data JPA: Biblioteca que ajuda a criar repositórios com Jakarta Persistense.
Repositório é uma classe (interface) que tem método para acessar um entidade no banco de dados.

Anotação @Repository indica que a interface é um componente do Spring

Interface Repository: 

public interface ClienteRepository extends JpaRepository<Cliente, Long>{

}

* Não precisa gerar a implementação da interface pq o Spring já faz isso.

Classe Controller: 

@RestController
public class ClienteController {

	@Autowired
	private ClienteRepository clienteRepository;
	
	@PersistenceContext
	private EntityManager manager;
	
	@GetMapping("/clientes")
	public List<Cliente> listar() {
		return clienteRepository.findAll();
	}
	
}

No repository:
Query Methods do Spring Data JPA
    List<Cliente> findByNome(String nome);
Deve iniciar com o prefixo findBy / queryBy ...

List<Cliente> findByNomeContaining(String nome);

No controller:
PathVariable buscando um singleton resource (usando route param)
	@GetMapping("/clientes/{clienteId}")
	public Cliente buscar(@PathVariable Long clienteId1 ){
		return clienteRepository.findById(clienteId1).orElse(null);
	}

@DeleteMapping("/{clienteId}")
public ResponseEntity<Void> remover (@PathVariable Long clienteId){

}

ResponseEntity<Tipo de Retorno do Corpo>, nesse caso Void pq não retorna nada no delete.

# Validação
Jakarta Bean Validation

spring-boot-starter-web
    - spring-boot-starter-validation
        - jakarta.validation-api (especificação)
        - hibernate-validation  (implementação)

Incluir as anotações do bean validation na entidade

@Entity
public class Cliente{
...
    @Notblank //javax.validation.constraints
    private String nome;

}

Para ativar a validação deve-se incluir a anotação @Valid no controlador:
@PostMapping
@ResponseStatus(HttpStatus.CREATED)
public Cliente adicionar(@Valid @RequestBody Cliente cliente){
...
}


@ControllerAdvice: Indica que é componente Spring que faz tratamento das exceptions de 
todos os controllers:
ResponseEntityExceptionHandler: Classe de conveniencia para tratamento de exceptions


@ControllerAdvice
public class ApiExceptionHandler extends ResponseEntityExceptionHandler{

}

Para traduzir as mensagens: utilizar os codes (ver mensagem no console)
Criar o arquivo messages.properties na pasta src/main/resources

messages.properties:
NotBlank=é obrigatório
Size=deve ter no mínimo {2} e no máximo {1} caracteres
Email=deve ser um e-mail válido

Para carregar o arquivo com as mensagens, deve-se injetar uma instância de MessageSource na classe ApiExceptionHandler

@Autowired
private MessageSource messageSource;

Para resolver problema com acentuação, basta configurar o encoding do arquivo:
- Encoding do arquivo messages.properties: btn dir / properties / resource / opção Text file encoding
- Encoding da aplicação: Window / Preferences / General / Content Types / Text / Java Properties File / UTF-8 / Update / Apply and close


@ExceptionHandler: Caso uma exception seja lançada irá chamar o método que possui essa anotação.

@ExceptionHandler(NegocioException.class)
public ResponseEntity<Object> handleNegocio( NegocioException ex, Webrequest){}


@JsonInclude(Include.NON_NULL): Anotação do Jackson que Customiza a seralização para não serializar entidade nula


@RestController
@RequestMapping("/ordens-servico") // os end-points serão feitos para esse recurso para atender tudo que começa com esse recurso
public class OrdemServicoController{


}



@JsonProperty(access = Access.READ_ONLY): Anotar as propriedades da entidade quando não for permitida a entrada de dados.
exemplo:

@JsonProperty(acces = Access.READ_ONLY)
private LocalDateTime dataFinalizacao;


Nesse caso, o valor que for informado será ignorado.


Validação
javax.validation:
Na entidade:
@NotNull: para objetos e valores
@NotBlank: para textos
Ex: 
@NotNull
@ManyToOne
private Cliente cliente;

No controller:
@Valid
Ex: 
public OrdemServico criar(@Valid @RequestBody OrdemServio ordemServico)

Validation Group
@Valid na propriedade da entidade, indica que a validação deve ser feita em cascata. Ou seja, deve validar todos os atributos da classe tbm. O que vai causar efeitos colaterais
A solução é usar Validation Group
@ConvertGroup( from = Default, to = )

javax.validation.groups.Default: é uma interface que marca que as validações devem ser feitas por um validation group padrão.
Todas as validações são realizadas a partir de um validation group default (@NotNull, @NotBlank, etc). Se precisarmos realizar algo fora do padrão, é necessário criar um novo validation group e avisar a aplicação fazendo o mapeamento de-para:
@ConvertGroup( from = Default, to = MeuValidationGroup)

ValidationGroup é uma interface vazia que serve apenas para marcar o grupo de validação

Exemplo:
Validation Group: ValidationGroups (que pode contrar vários validations group)
public interface ValidationGroups {
	
	public interface ClienteId {}

}

Entidade OrdemServico.java:
    ...
	@Valid
	@ConvertGroup(from = Default.class, to = ValidationGroups.ClienteId.class)
	@NotNull
	@ManyToOne
	@JoinColumn(name="cliente_id")
	private Cliente cliente;

Entidade Cliente.java:
    ...
	@NotNull(groups = ValidationGroups.ClienteId.class)
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;


Controlador OrdemServicoController.java
    ...
	@PostMapping
	@ResponseStatus(HttpStatus.CREATED)
	public OrdemServico criar (@Valid @RequestBody OrdemServico ordemServico) {
		return gestaoOrdemServicoService.criar(ordemServico);
	}



Padrão para representação de data e hora : ISO 8601 com offset (dif. em horas ref. ao meridiano de greenwich. 
Um offset de 3 horas atrás de UTC, pode ser representado por -03, -0300, -03:00
Para representar UTC, usa-se a letra z ou +00:00

Utilizar tipo de dado OffsetDateTime

Domain Model x Representation Model

Domain Model: São as entidades que representam as tabelas do domínio.
domain / model

Representatios Model: São as classes que representam os dados que serão expostos.
Classe com as definições da representação do recurso da api (em angular nós usamos o mapeamento para classes .ts)
api / controller

Uma classe model pode ser usada como representation para expor os dados.
Nesse caso, podem haver informações que não queremos expor
Quando compartilhamos uma classe entre o modelo de domínio e o modelo representacional, podemos ter alguns problemas:
- ao alterar a classe de domínio, estaremos inpactando diretamente nos dados que são expostos pelo modelo repesentacional
- facilidade em quebrar os consumidores da api com uma alteração indesejada

O ideal é isolar o domain model do representation model
cria-se classe de transferência de dados usando o padrão DTO (padrão usado para a transferência de dados entre camadas de sistema)

Modelo de repesentação do recurso deve contrar apenas os atributos que precisam ser expostos pela API.

Após a criação do modelo, na classe controller, deve-se trocar as classes de modelo de domínio pelas classes do modelo de representação.

modelmapper biblioteca que ajuda a evitar a escrita de códigos boilerplate ref. a transferência de dados do modelo de domínio para o modelo representacional

Para realizar pesquisas no repositório central do maven:
search.maven.org
modelmapper

Importante: Vamos ganhar um erro ao injetar modelmapper pq ele não está sendo gerenciado pelo Spring. È necessário transformar o modelmapper em uma instância gerenciada pelo container do Spring.
Como ModelMapper é um componente de terceiros, não é possível fazer uma anotação Spring (@Service, @Repository, etc). Nesse caso, teremos que criar uma classe para expor uma instância de ModelMapper para que ela possa ser injetada.

@Configuration
public class ModelMapperConfig {
	
	@Bean
	public ModelMapper modelMapper() {
		return new ModelMapper();
	}
}

Ocorreram erros ao tentar usar ModelMapper com java 8.0.
Solução encontrada em: http://modelmapper.org/getting-started/

<dependency>
  <groupId>org.modelmapper</groupId>
  <artifactId>modelmapper</artifactId>
  <version>2.3.0</version>
</dependency>

Estratégia de correspondência de nomes


Recurso que não está representado no domain model, ou seja, faz parte da regra de negócio e não faz parte do CRUD. Ex.: Finalizar a O.S, emitir nota fiscal
Usar método HTTP: PUT
PUT é idempotente, ou seja pode ser executado diversas vezes que não haverá efeito colateral.

POST NÃO é idempotente.

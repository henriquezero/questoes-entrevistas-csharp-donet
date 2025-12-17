# Questões de Entrevista para Desenvolvedores C# .NET

## 🎯 Objetivo

O objetivo deste repositório é **auxiliar candidatos e desenvolvedores**
que desejam revisar ou praticar conceitos fundamentais de C# e .NET
antes de entrevistas técnicas.

## 🤝 Contribuições

Sinta-se à vontade para contribuir enviando novas questões, melhorias ou
correções via **Pull Request**.

## 📋 Índice
- [Boas Práticas](#boas-práticas)
- [Programação Orientada a Objetos](#programação-orientada-a-objetos)
- [Arquitetura](#arquitetura)
- [C# .NET](#c-net)
- [Banco de Dados](#banco-de-dados)
- [REST](#rest)

---

## Boas Práticas

### Princípios SOLID

#### S - Single Responsibility Principle
Este princípio estabelece que uma classe deve ter uma **única responsabilidade**.

#### O - Open-Closed Principle  
Objetos ou entidades devem estar **abertos para extensão, mas fechados para modificação**.

#### L - Liskov Substitution Principle
Uma classe derivada deve ser **substituível por sua classe base**.

#### I - Interface Segregation Principle
Uma classe **não deve ser forçada** a implementar interfaces e métodos que **não irão utilizar**.

#### D - Dependency Inversion Principle
**Dependa de abstrações** e não de implementações.

### Outros Princípios Fundamentais

#### DRY - Don't Repeat Yourself
**Evite duplicação de código**. Cada funcionalidade deve ter uma única representação no sistema.

#### YAGNI - You Ain't Gonna Need It
**Não implemente funcionalidades** até que sejam realmente necessárias. Foque no que é preciso agora.

#### KISS - Keep It Simple, Stupid
**Mantenha a simplicidade**. Soluções simples são mais fáceis de entender, manter e debugar.

## Programação Orientada a Objetos

### Principais Pilares da POO
1. **Encapsulamento** – esconder detalhes internos  
2. **Herança** – reuso e extensão de código  
3. **Polimorfismo** – múltiplas formas de comportamento  
4. **Abstração** – simplificação e contratos de alto nível

#### Encapsulamento
- Protege os dados internos da classe contra acessos indevidos
- Exposto via **getters e setters**
- Permite **ocultar detalhes de implementação**

#### Herança
- Permite criar novas classes a partir de classes existentes
- Facilita o **reuso de código**
- Pode ser simples (uma única base) ou múltipla (dependendo da linguagem)

#### Polimorfismo
- Habilidade de usar o **mesmo método de formas diferentes**
- Pode ser:
  - **Sobrecarga (overloading):** métodos com o mesmo nome, mas assinaturas diferentes
  - **Sobrescrita (overriding):** redefinição de comportamento de um método herdado

#### Abstração
- Foca em **modelar comportamentos essenciais** e ocultar detalhes complexos
- Usada em classes abstratas e interfaces
- Permite que diferentes implementações concretas respeitem o mesmo contrato
   
#### Virtual vs Abstract

**Métodos Virtual:**
- Possuem **implementação** na classe base
- **Podem** ser sobrepostos por classes derivadas

**Métodos Abstract:**
- **Não possuem implementação**
- **Devem** ser implementados na primeira classe derivada concreta

#### Interface vs Classe Abstrata

**Classes Abstratas:**
- Podem fornecer **implementações** para alguns ou todos os métodos
- Permitem construtores e campos

**Interfaces:**
- Exigem que **todos os métodos sejam implementados**
- Apenas contratos (assinaturas de métodos)

---

## Arquitetura

### Microsserviços
Consiste em construir aplicações **desmembrando-as em serviços independentes**. Estes serviços se comunicam entre si usando APIs e promovem grande agilidade em times de desenvolvimento.

**Vantagens:**
- Escalabilidade independente de cada serviço
- Permite uso de diferentes tecnologias em cada microsserviço
- Facilita deploys frequentes e independentes
- Maior resiliência: falha em um serviço não compromete toda a aplicação
- Times menores e focados em domínios específicos

**Desvantagens:**
- Maior complexidade de arquitetura
- Gestão de comunicação entre serviços (latência, falhas, versionamento de APIs)
- Monitoramento, logging e debugging mais complexos
- Exige maior maturidade de automação e DevOps
- Custos de infraestrutura podem ser mais elevados

---

### Monolito
Aplicação construída como **uma única unidade**. Todos os componentes estão interconectados e são implantados juntos.

**Vantagens:**
- Simples de desenvolver e testar
- Fácil deployment inicial
- Menos complexidade de rede

**Desvantagens:**
- Dificulta escalabilidade independente
- Tecnologia única para toda aplicação
- Deploys mais arriscados (tudo ou nada)
- Crescimento pode gerar “monólito legado” difícil de manter

### Clean Architecture / Onion Architecture
Organização em **camadas concêntricas** onde dependências apontam sempre para o centro (domínio).

**Estrutura de pastas típica:**
```
src/
├── Core/
│   ├── Domain/
│   │   ├── Entities/
│   │   ├── Interfaces/
│   │   └── ValueObjects/
│   └── Application/
│       ├── UseCases/
│       ├── DTOs/
│       └── Interfaces/
|       └── Services/
├── Infrastructure/
│   ├── Data/
│   ├── Repositories/
└── Web/
    ├── Controllers/
    ├── Models/
    └── Program.cs
```

### Vertical Slice Architecture
Organização por **funcionalidades** ao invés de camadas técnicas. Cada slice contém tudo necessário para uma feature.

**Estrutura de pastas típica:**
```
src/
├── Features/
│   ├── Users/
│   │   ├── CreateUser/
│   │   │   ├── CreateUserCommand.cs
│   │   │   ├── CreateUserHandler.cs
│   │   │   └── CreateUserValidator.cs
│   │   ├── GetUser/
│   │   └── UpdateUser/
│   ├── Products/
│   │   ├── CreateProduct/
│   │   ├── ListProducts/
│   │   └── DeleteProduct/
└── Shared/
    ├── Database/
    └── Common/
```

### CQRS (Command Query Responsibility Segregation)
Separar a **responsabilidade de escrita e leitura** de dados.
- **Command**: para escrita de dados
- **Query**: para leitura de dados

### MEDIATOR Pattern
Encapsular **como os objetos interagem**. A comunicação entre objetos é estabelecida através do Mediator.

**Exemplo:** Piloto de Avião A e Piloto B precisam se comunicar com o aeroporto - o mediator é a **torre de comando**.

### DDD (Domain-Driven Design)
Design da solução orientado pelas **regras de negócio**.

**Vantagem:** Facilita manutenção e explicação do código para pessoas que nunca viram antes.

### TDD (Test-Driven Development)
Design da solução iniciado pelos **testes**, ao invés do código.

**Fluxo:** Teste → Falha → Implementação → Refatoração → Sucesso

---

## C# .NET

### Tipos de Valor vs Tipos de Referência

#### **Tipos de Valor (Value Types)**
```csharp
int N1 = 1000; // value type
int N2 = N1;   // value type (cópia do valor)
```

**Resposta:** 
Existem **dois objetos distintos** na memória. `int` é um tipo de valor, portanto quando fazemos `int N2 = N1`, criamos uma **cópia** do valor de N1, não uma referência. Cada variável possui sua própria área de memória na stack.

#### **Tipos de Referência (Reference Types)**
```csharp
List<int> lista1 = new List<int> {1, 2, 3};
List<int> lista2 = lista1;  // REFERÊNCIA ao mesmo objeto
lista1.Add(4);              // lista2 também terá {1, 2, 3, 4}
```

**Resposta:**
Existe **apenas um objeto** na memória. Ambas variáveis **apontam para o mesmo objeto** no heap. Quando modificamos `lista1`, a `lista2` também é afetada porque ambas referenciam o mesmo local na memória.

### Diferença entre "==" e "Equals"

- **==** é usado principalmente para **tipos de valor** (comparação de valores)
- **Equals** é usado para **tipos de referência** (pode ser sobrescrito para comparação personalizada)

### Boxing e Unboxing

#### Boxing
Converter um **tipo de valor** para **tipo de referência** (implícito):

```csharp
int numero = 23;
object obj = numero; // boxing
```

#### Unboxing  
Converter um **tipo de referência** de volta para **tipo de valor** (explícito):

```csharp
int i = 123;
object o = i;        // boxing
int j = (int)o;      // unboxing
```

### Tipos de Projetos .NET

- **Class Library** → Resulta em uma **DLL**, não possui interface
- **Console Application** → Aplicação no **terminal**, pode receber input do usuário  
- **Projeto Web** → **APIs** e aplicações web
- **Projeto Testes** → Para testes unitários e integração

### Injeção de Dependência

#### O que é Injeção de Dependência (Dependency Injection) no .NET?

É um padrão de design onde as dependências são **injetadas externamente**, ao invés de serem criadas dentro da classe.

**Benefícios:**
- Código mais desacoplado  
- Maior testabilidade  
- Facilita manutenção e evolução  

#### Tipos de Ciclo de Vida:

- **AddSingleton**: Inicia com a aplicação e morre com ela
- **AddScoped**: Instancia a cada **requisição** (ideal para banco de dados)
- **AddTransient**: Nova instância a cada chamada da abstração

### O que é async / await?

Permite escrever código **assíncrono e não-bloqueante**, mantendo a leitura simples e sequencial.

**Benefícios:**
- Melhor performance
- Não bloqueia a thread principal
- Ideal para I/O (banco de dados, APIs, arquivos)

### Qual a diferença entre Task e Thread?

- **Thread** é de nível de sistema operacional
- **Task** é uma abstração de mais alto nível, gerenciada pelo **Thread Pool do .NET**

**Resumo:**  
`Task` é mais eficiente, escalável e recomendada para programação assíncrona moderna.

### O que é Middleware no ASP.NET Core?

Middleware é um componente que **processa requisições e respostas HTTP** dentro de um pipeline.

**Exemplos comuns:**
- Autenticação
- Logging
- Tratamento de exceções

**Cada middleware pode:**
- Processar a requisição
- Encerrar o pipeline
- Ou passar para o próximo middleware

### Collections e LINQ

#### IEnumerable vs IQueryable

**IEnumerable (Runtime):**
- Para consultar dados em **coleções em memória** (List, Array, etc.)
- Processamento na memória

**IQueryable (Compile-time):**
- Para consultar dados **fora da memória** (banco de dados, serviços)
- Usa **Lazy Loading** - dados carregados virtualmente

**Lazy Loading** é uma técnica onde os dados não são carregados imediatamente da fonte (banco de dados), mas apenas quando você realmente precisa deles.

```csharp
// IQueryable - Lazy Loading
IQueryable<Produto> produtos = context.Produtos.Where(p => p.Preco > 100);
// Neste momento, NENHUMA consulta foi feita ao banco ainda!

var lista = produtos.ToList(); 
// SÓ AGORA a consulta SQL é executada no banco
```
**Resumo:** É como ter uma "promessa" de dados - você monta a consulta, mas ela só é executada quando você realmente precisa dos resultados.

#### Hierarquia de Collections

- **IEnumerable**: Permite enumerar itens
- **ICollection**: Permite **contar** quantos itens  
- **IList**: Permite **inserir/remover** itens em qualquer posição e buscar por índice

---

## Banco de Dados

### Principais Diferenças

| Aspecto | SQL | NoSQL |
|---------|-----|-------|
| **Estrutura** | Tabelas com colunas fixas | Documentos flexíveis (JSON) |
| **Schema** | Rígido (deve definir antes) | Flexível (pode mudar depois) |
| **Relacionamentos** | JOINs entre tabelas | Dados aninhados ou referências |
| **Escalabilidade** | Vertical (mais poder no servidor) | Horizontal (mais servidores) |
| **Consistência** | ACID (sempre consistente) | Eventually Consistent |

### Quando Usar Cada Um?

#### **Use SQL quando:**
- ✅ **Dados estruturados** (sempre os mesmos campos)
- ✅ **Relacionamentos complexos** (clientes → pedidos → produtos)
- ✅ **Consistência crítica** (sistema bancário, e-commerce)
- ✅ **Relatórios e análises** (BI, dashboards)

**Exemplos:** Sistema bancário, ERP, CRM

#### **Use NoSQL quando:**
- ✅ **Dados flexíveis** (cada registro pode ter campos diferentes)
- ✅ **Crescimento rápido** (milhões de usuários)
- ✅ **Dados não-relacionais** (posts, comentários, logs)
- ✅ **Desenvolvimento ágil** (mudanças frequentes na estrutura)

**Exemplos:** Redes sociais, IoT, Big Data, APIs REST

### SQL vs NoSQL - Transformações

**SQL:**
- `SUM`, `COUNT`, `AVG`, `ROW_NUMBER()`

**NoSQL (MongoDB):**
- `aggregate`, `mapreduce`

### Resumo Prático

**SQL = Casa bem organizada:**
- Cada coisa no seu lugar
- Difícil de mudar a estrutura
- Fácil de encontrar tudo relacionado

**NoSQL = Mochila de viagem:**
- Flexível, cabe qualquer coisa
- Fácil de expandir
- Rápido para guardar e tirar coisas

---

## REST

### Princípios REST

**REST (Representational State Transfer)** é um estilo arquitetural para sistemas distribuídos, especialmente para web services.

#### Principais Características:

- **Stateless**: Cada requisição deve conter todas as informações necessárias
- **Client-Server**: Separação clara entre cliente e servidor
- **Cacheable**: Respostas devem ser explicitamente cacheáveis ou não-cacheáveis
- **Uniform Interface**: Interface uniforme entre componentes

### REST vs RESTful

- **REST**:  
  É o **conjunto de princípios arquiteturais** (conceito) que define como recursos devem ser modelados e acessados.  
  Exemplo: usar métodos HTTP corretamente, manter a comunicação stateless, seguir uma interface uniforme etc.

- **RESTful**:  
  Refere-se a uma **implementação prática de uma API** que **segue corretamente os princípios REST**.  
  Ou seja, uma API pode ser chamada de RESTful quando aplica, na prática, as restrições e boas práticas do estilo REST.

### Métodos HTTP

| Método | Ação | Uso |
|--------|------|-----|
| **GET** | Buscar dados | `GET /api/users/1` |
| **POST** | Criar novo recurso | `POST /api/users` |
| **PUT** | Atualizar completamente | `PUT /api/users/1` |
| **PATCH** | Atualizar parcialmente | `PATCH /api/users/1` |
| **DELETE** | Remover recurso | `DELETE /api/users/1` |

### Status Codes Importantes

- **200 OK**: Sucesso geral
- **201 Created**: Recurso criado com sucesso
- **400 Bad Request**: Erro na requisição
- **401 Unauthorized**: Não autenticado
- **403 Forbidden**: Não autorizado
- **404 Not Found**: Recurso não encontrado
- **500 Internal Server Error**: Erro no servidor

### Boas Práticas

- Use **substantivos** nas URLs: `/users` ao invés de `/getUsers`
- Use **plural**: `/users` ao invés de `/user`
- **Versionamento**: `/api/v1/users`
- **Filtros via query params**: `/users?age=25&active=true`
- **Paginação**: `/users?page=1&limit=10`

### Exemplo de API RESTful

```
GET    /api/v1/users          # Listar usuários
GET    /api/v1/users/1        # Buscar usuário específico
POST   /api/v1/users          # Criar novo usuário
PUT    /api/v1/users/1        # Atualizar usuário completo
PATCH  /api/v1/users/1        # Atualizar dados específicos
DELETE /api/v1/users/1        # Remover usuário
```

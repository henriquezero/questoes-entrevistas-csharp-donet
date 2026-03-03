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

### Threads e Concorrência

#### Thread vs Task vs ThreadPool

```csharp
// Thread - controle manual, pesado
Thread t = new Thread(() => Console.WriteLine("Thread!"));
t.Start();

// ThreadPool - pool gerenciado pelo runtime
ThreadPool.QueueUserWorkItem(_ => Console.WriteLine("Pool!"));

// Task - abstração moderna sobre ThreadPool
Task.Run(() => Console.WriteLine("Task!"));
```

**Resumo:**
- **Thread**: Cria thread do SO, caro em memória (~1MB stack cada). Use quando precisa de controle fino (prioridade, foreground/background).
- **ThreadPool**: Pool de threads reutilizáveis, gerenciado pelo CLR. Evita custo de criar/destruir threads.
- **Task**: Wrapper sobre ThreadPool com suporte a `async/await`, continuações, cancelamento e tratamento de exceções.

#### Problemas de Concorrência

**Race Condition:** duas threads acessam/modificam o mesmo recurso simultaneamente.

```csharp
// PROBLEMA - Race Condition
int contador = 0;
Parallel.For(0, 1000, _ => contador++); // resultado imprevisível!

// SOLUÇÃO 1 - lock
object lockObj = new object();
Parallel.For(0, 1000, _ => { lock(lockObj) { contador++; } });

// SOLUÇÃO 2 - Interlocked (mais performático para operações simples)
Parallel.For(0, 1000, _ => Interlocked.Increment(ref contador));
```

#### Deadlock

Acontece quando **duas threads ficam esperando uma pela outra** infinitamente.

```csharp
// EXEMPLO CLÁSSICO DE DEADLOCK
object lock1 = new(), lock2 = new();

Task.Run(() => { lock(lock1) { lock(lock2) { /* ... */ } } });
Task.Run(() => { lock(lock2) { lock(lock1) { /* ... */ } } }); // DEADLOCK!
```

**Como evitar:** sempre adquirir locks na **mesma ordem** em todas as threads.

#### CancellationToken

Mecanismo padrão do .NET para **cancelar operações assíncronas de forma cooperativa**.

```csharp
var cts = new CancellationTokenSource();
cts.CancelAfter(TimeSpan.FromSeconds(5)); // timeout de 5s

async Task ProcessarAsync(CancellationToken token)
{
    while (!token.IsCancellationRequested)
    {
        await Task.Delay(100, token);
        // trabalho...
    }
}
```

**Ponto de entrevista:** O cancelamento é **cooperativo** — o código precisa verificar o token. Não mata a thread à força.

---

### Garbage Collector (GC)

#### Como funciona?

O GC é o sistema de **gerenciamento automático de memória** do .NET. Ele libera objetos que **não têm mais referências** apontando para eles.

#### Gerações do GC

```
Gen 0 → Objetos recém-criados (coleta frequente, rápida)
Gen 1 → Sobreviveram a 1 coleta (buffer entre Gen 0 e Gen 2)
Gen 2 → Objetos de longa vida (coleta rara, cara)
```

**Lógica:** A maioria dos objetos morre jovem (Gen 0). Se sobrevive, provavelmente vai durar bastante → promove para próxima geração.

#### IDisposable e using

Para **recursos não-gerenciados** (conexões de banco, arquivos, sockets), o GC **não sabe limpar**. Você precisa fazer manualmente:

```csharp
// Padrão moderno - using declaration
using var connection = new SqlConnection(connString);
// connection.Dispose() é chamado automaticamente ao sair do escopo

// Padrão clássico - using statement
using (var reader = new StreamReader("arquivo.txt"))
{
    var conteudo = reader.ReadToEnd();
} // Dispose() chamado aqui
```

#### Finalizer vs Dispose

- **Dispose()**: Chamado explicitamente pelo dev (determinístico)
- **Finalizer (~Classe)**: Chamado pelo GC (não-determinístico, mais lento)

```csharp
public class MinhaClasse : IDisposable
{
    private bool _disposed = false;

    public void Dispose()
    {
        if (!_disposed)
        {
            // Liberar recursos não-gerenciados
            _disposed = true;
            GC.SuppressFinalize(this); // evita finalizer desnecessário
        }
    }

    ~MinhaClasse() => Dispose(); // safety net
}
```

**Ponto de entrevista:** Sempre prefira `Dispose()` com `using`. Finalizer é apenas **rede de segurança**.

#### Memory Leak em .NET — "Mas não tem GC?"

Sim, mas ainda pode ter **leaks lógicos**:
- **Event handlers** não removidos (objeto publisher mantém referência ao subscriber)
- **Objetos estáticos** que acumulam dados
- **Closures** que capturam referências sem querer
- **Cache sem política de expiração**

---

### Tratamento de Exceções

#### Hierarquia de Exceções

```
System.Exception
├── System.SystemException (exceções do runtime)
│   ├── NullReferenceException
│   ├── IndexOutOfRangeException
│   ├── InvalidOperationException
│   ├── ArgumentException
│   │   └── ArgumentNullException
│   └── StackOverflowException (não capturável!)
└── System.ApplicationException (exceções custom - evitar herdar daqui)
```

#### Try / Catch / Finally / When

```csharp
try
{
    var resultado = await httpClient.GetAsync(url);
}
catch (HttpRequestException ex) when (ex.StatusCode == HttpStatusCode.NotFound)
{
    // Filtro de exceção (when) - só entra aqui se for 404
    logger.LogWarning("Recurso não encontrado");
}
catch (HttpRequestException ex)
{
    // Outros erros HTTP
    logger.LogError(ex, "Erro HTTP");
}
catch (Exception ex)
{
    // Catch genérico - SEMPRE por último
    logger.LogError(ex, "Erro inesperado");
    throw; // re-throw mantendo stack trace original
}
finally
{
    // SEMPRE executa (com ou sem exceção)
    // Ideal para cleanup
}
```

#### throw vs throw ex

```csharp
catch (Exception ex)
{
    throw;    // ✅ Mantém o stack trace original
    throw ex; // ❌ Reseta o stack trace (perde informação de onde originou)
}
```

#### Exceções Customizadas

```csharp
public class BusinessException : Exception
{
    public string ErrorCode { get; }
    
    public BusinessException(string message, string errorCode) 
        : base(message)
    {
        ErrorCode = errorCode;
    }
}
```

**Ponto de entrevista:** Nunca use exceções para **fluxo de controle**. Exceções são para situações **excepcionais**. Para validações, prefira retornar Result/Error objects.

---

### HTTP Pipeline e Middleware (Detalhado)

#### Ordem do Pipeline

```
Requisição HTTP →
  1. ExceptionHandler (captura erros de tudo abaixo)
  2. HSTS / HTTPS Redirection
  3. Static Files
  4. Routing (resolve qual endpoint)
  5. CORS
  6. Authentication (quem é você?)
  7. Authorization (você pode?)
  8. Custom Middlewares
  9. Endpoint (Controller/MinimalAPI)
← Resposta HTTP (volta na ordem inversa)
```

**A ordem importa!** Authentication antes de Authorization. ExceptionHandler no topo para capturar tudo.

#### Criando Middleware Customizado

```csharp
public class RequestTimingMiddleware
{
    private readonly RequestDelegate _next;

    public RequestTimingMiddleware(RequestDelegate next) => _next = next;

    public async Task InvokeAsync(HttpContext context)
    {
        var sw = Stopwatch.StartNew();
        
        await _next(context); // chama o próximo middleware
        
        sw.Stop();
        context.Response.Headers.Add("X-Response-Time", $"{sw.ElapsedMilliseconds}ms");
    }
}

// Registro em Program.cs
app.UseMiddleware<RequestTimingMiddleware>();
```

#### Filtros vs Middleware

- **Middleware**: Opera no **pipeline HTTP inteiro** (antes do routing)
- **Filtros**: Operam **dentro do MVC** (após routing, mais granular)

```
Middleware → Routing → [Action Filters → Controller → Result Filters]
```

Tipos de filtros: Authorization, Resource, Action, Exception, Result.

---

### Design Patterns Comuns em Entrevista

#### Repository Pattern

Abstrai o acesso a dados. O Service não sabe se é SQL, Mongo, ou API.

```csharp
public interface IProdutoRepository
{
    Task<Produto?> GetByIdAsync(int id);
    Task<IEnumerable<Produto>> GetAllAsync();
    Task AddAsync(Produto produto);
}
```

#### Unit of Work

Garante que **múltiplas operações** no banco são commitadas (ou revertidas) **juntas**.

```csharp
public interface IUnitOfWork : IDisposable
{
    IProdutoRepository Produtos { get; }
    IPedidoRepository Pedidos { get; }
    Task<int> CommitAsync();
}
```

#### Factory Pattern

Encapsula a lógica de **criação** de objetos.

```csharp
public static class NotificacaoFactory
{
    public static INotificacao Criar(string tipo) => tipo switch
    {
        "email" => new EmailNotificacao(),
        "sms"   => new SmsNotificacao(),
        "push"  => new PushNotificacao(),
        _       => throw new ArgumentException($"Tipo desconhecido: {tipo}")
    };
}
```

---

### Structs vs Classes

| Aspecto | Struct | Class |
|---------|--------|-------|
| Tipo | Valor (stack) | Referência (heap) |
| Herança | Não suporta | Suporta |
| Default | Não pode ter construtor sem parâmetros (antes C#10) | Pode |
| Ideal para | Objetos pequenos e imutáveis (Point, Color) | Objetos complexos |
| Nullable | `int?` (Nullable<int>) | Já é nullable por padrão |

---

### Strings

#### string vs StringBuilder

```csharp
// ❌ String é IMUTÁVEL - cada concatenação cria novo objeto
string resultado = "";
for (int i = 0; i < 10000; i++)
    resultado += i.ToString(); // 10.000 objetos criados!

// ✅ StringBuilder é MUTÁVEL - modifica o mesmo buffer
var sb = new StringBuilder();
for (int i = 0; i < 10000; i++)
    sb.Append(i);
string resultado = sb.ToString(); // 1 objeto
```

#### String Interpolation e Verbatim

```csharp
var nome = "José";
var msg = $"Olá, {nome}!";              // interpolação
var path = @"C:\Users\jose\docs";        // verbatim (ignora escape)
var multi = $@"Olá {nome},
caminho: C:\Users";                      // combinados
```

---

### Records (C# 9+)

**Tipo imutável** por padrão, com igualdade por **valor** (não por referência).

```csharp
public record Pessoa(string Nome, int Idade);

var p1 = new Pessoa("José", 30);
var p2 = new Pessoa("José", 30);

Console.WriteLine(p1 == p2);       // true! (compara por valor)
Console.WriteLine(p1.Equals(p2));  // true!

// with - cria cópia com modificação
var p3 = p1 with { Idade = 31 };
```

**Quando usar:** DTOs, Value Objects, respostas de API — qualquer objeto que represente **dados imutáveis**.

---

### Generics

```csharp
// Método genérico
public T Max<T>(T a, T b) where T : IComparable<T>
    => a.CompareTo(b) >= 0 ? a : b;

// Classe genérica
public class Result<T>
{
    public bool Success { get; init; }
    public T? Data { get; init; }
    public string? Error { get; init; }

    public static Result<T> Ok(T data) => new() { Success = true, Data = data };
    public static Result<T> Fail(string error) => new() { Success = false, Error = error };
}
```

#### Constraints comuns

- `where T : class` → deve ser tipo referência
- `where T : struct` → deve ser tipo valor
- `where T : new()` → deve ter construtor sem parâmetros
- `where T : IMinhaInterface` → deve implementar interface

---

### Delegates, Events e Lambdas

#### Delegate

É um **ponteiro para função** type-safe.

```csharp
// Delegates built-in do .NET
Func<int, int, int> soma = (a, b) => a + b;     // tem retorno
Action<string> log = msg => Console.WriteLine(msg); // sem retorno
Predicate<int> ehPar = n => n % 2 == 0;           // retorna bool
```

#### Events

Implementam o padrão **Observer** (publisher/subscriber):

```csharp
public class Pedido
{
    public event EventHandler<string>? PedidoCriado;
    
    public void Criar()
    {
        // lógica...
        PedidoCriado?.Invoke(this, "Pedido #123 criado");
    }
}
```

**Ponto de entrevista:** Lembre de **remover event handlers** (`-=`) para evitar memory leaks.

---

### Nullable Reference Types (C# 8+)

```csharp
#nullable enable

string nome = null;   // ⚠️ Warning: possível null
string? nome = null;  // ✅ Explicitamente nullable

// Null-conditional e Null-coalescing
var tamanho = nome?.Length ?? 0;  // se nome for null, retorna 0

// Null-forgiving (eu sei que não é null)
var tamanho = nome!.Length;  // suprime o warning (use com cuidado!)
```

---

### Span<T> e Memory<T> (Performance)

```csharp
// Span evita alocações desnecessárias ao fatiar arrays
int[] numeros = { 1, 2, 3, 4, 5 };
Span<int> slice = numeros.AsSpan(1, 3); // {2, 3, 4} sem copiar!

// Útil para parsing de strings sem alocar
ReadOnlySpan<char> texto = "2024-01-15".AsSpan();
var ano = int.Parse(texto[..4]);   // parse sem criar substring
```

**Quando usar:** Cenários de **alta performance** onde alocações importam (parsers, processamento de dados em bulk).

---

### Testes Unitários

#### Estrutura AAA (Arrange, Act, Assert)

```csharp
[Fact]
public void Calcular_Desconto_DeveRetornar10Porcento()
{
    // Arrange
    var service = new DescontoService();
    var valorOriginal = 100m;

    // Act
    var resultado = service.Calcular(valorOriginal, percentual: 10);

    // Assert
    Assert.Equal(90m, resultado);
}
```

#### Mocking com Moq

```csharp
[Fact]
public async Task CriarPedido_DeveNotificarCliente()
{
    // Arrange
    var mockNotificacao = new Mock<INotificacaoService>();
    var service = new PedidoService(mockNotificacao.Object);

    // Act
    await service.CriarAsync(new Pedido());

    // Assert
    mockNotificacao.Verify(
        n => n.EnviarAsync(It.IsAny<string>()), 
        Times.Once);
}
```

---

### Minimal APIs vs Controllers
#### Quando usar cada um?

- **Minimal API**: Microsserviços, APIs simples, protótipos rápidos
- **Controllers**: APIs maiores, quando precisa de filtros, model binding complexo, convenções MVC

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

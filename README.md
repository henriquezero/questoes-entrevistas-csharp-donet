# Questões de Entrevista para Desenvolvedores C# .NET

## 🎯 Objetivo

O objetivo deste repositório é **auxiliar candidatos e desenvolvedores**
que desejam revisar ou praticar conceitos fundamentais de C# e .NET
antes de entrevistas técnicas.

## 🤝 Contribuições

Sinta-se à vontade para contribuir enviando novas questões, melhorias ou
correções via **Pull Request**.

## 📋 Índice
- [Conceitos Fundamentais](#conceitos-fundamentais)
  - [Tipos de Valor vs Tipos de Referência](#tipos-de-valor-vs-tipos-de-referência)
  - [Diferença entre "==" e "Equals"](#diferença-entre--e-equals)
- [Princípios SOLID](#princípios-solid)
- [Padrões de Arquitetura](#padrões-de-arquitetura)
  - [Microsserviços](#microsserviços)
  - [CQRS (Command Query Responsibility Segregation)](#cqrs-command-query-responsibility-segregation)
  - [MEDIATOR Pattern](#mediator-pattern)
  - [DDD (Domain-Driven Design)](#ddd-domain-driven-design)
  - [TDD (Test-Driven Development)](#tdd-test-driven-development)
- [Tipos de Projetos .NET](#tipos-de-projetos-net)
- [Injeção de Dependência](#injeção-de-dependência)
- [Collections e LINQ](#collections-e-linq)
  - [IEnumerable vs IQueryable](#ienumerable-vs-iqueryable)
  - [Hierarquia de Collections](#hierarquia-de-collections)
- [Programação Orientada a Objetos](#programação-orientada-a-objetos)
  - [Virtual vs Abstract](#virtual-vs-abstract)
  - [Interface vs Classe Abstrata](#interface-vs-classe-abstrata)
- [Boxing e Unboxing](#boxing-e-unboxing)
- [Banco de Dados](#banco-de-dados)
  - [Principais Diferenças](#principais-diferenças)
  - [Quando Usar Cada Um?](#quando-usar-cada-um)
  - [SQL vs NoSQL - Transformações](#sql-vs-nosql---transformações)
  - [Resumo Prático](#resumo-prático)

---

## Conceitos Fundamentais

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

---

## Princípios SOLID

### S - Single Responsibility Principle
Uma classe deve ter **um, e somente um, motivo para mudar**.

### O - Open-Closed Principle  
Objetos ou entidades devem estar **abertos para extensão, mas fechados para modificação**.

### L - Liskov Substitution Principle
Uma classe derivada deve ser **substituível por sua classe base**.

### I - Interface Segregation Principle
Uma classe não deve ser forçada a implementar interfaces e métodos que **não irão utilizar**.

### D - Dependency Inversion Principle
**Dependa de abstrações** e não de implementações.

---

## Padrões de Arquitetura

### Microsserviços
Consiste em construir aplicações **desmembrando-as em serviços independentes**. Estes serviços se comunicam entre si usando APIs e promovem grande agilidade em times de desenvolvimento.

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

## Tipos de Projetos .NET

- **Class Library** → Resulta em uma **DLL**, não possui interface
- **Console Application** → Aplicação no **terminal**, pode receber input do usuário  
- **Projeto Web** → **APIs** e aplicações web
- **Projeto Testes** → Para testes unitários e integração

---

## Injeção de Dependência

### Tipos de Ciclo de Vida:

- **AddSingleton**: Inicia com a aplicação e morre com ela
- **AddScoped**: Instancia a cada **requisição** (ideal para banco de dados)
- **AddTransient**: Nova instância a cada chamada da abstração

---

## Collections e LINQ

### IEnumerable vs IQueryable

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

### Hierarquia de Collections

- **IEnumerable**: Permite enumerar itens
- **ICollection**: Permite **contar** quantos itens  
- **IList**: Permite **inserir/remover** itens em qualquer posição e buscar por índice

---

## Programação Orientada a Objetos

### Virtual vs Abstract

**Métodos Virtual:**
- Possuem **implementação** na classe base
- **Podem** ser sobrepostos por classes derivadas

**Métodos Abstract:**
- **Não possuem implementação**
- **Devem** ser implementados na primeira classe derivada concreta

### Interface vs Classe Abstrata

**Classes Abstratas:**
- Podem fornecer **implementações** para alguns ou todos os métodos
- Permitem construtores e campos

**Interfaces:**
- Exigem que **todos os métodos sejam implementados**
- Apenas contratos (assinaturas de métodos)

---

## Boxing e Unboxing

### Boxing
Converter um **tipo de valor** para **tipo de referência** (implícito):

```csharp
int numero = 23;
object obj = numero; // boxing
```

### Unboxing  
Converter um **tipo de referência** de volta para **tipo de valor** (explícito):

```csharp
int i = 123;
object o = i;        // boxing
int j = (int)o;      // unboxing
```

---

## Banco de Dados

## Principais Diferenças

| Aspecto | SQL | NoSQL |
|---------|-----|-------|
| **Estrutura** | Tabelas com colunas fixas | Documentos flexíveis (JSON) |
| **Schema** | Rígido (deve definir antes) | Flexível (pode mudar depois) |
| **Relacionamentos** | JOINs entre tabelas | Dados aninhados ou referências |
| **Escalabilidade** | Vertical (mais poder no servidor) | Horizontal (mais servidores) |
| **Consistência** | ACID (sempre consistente) | Eventually Consistent |

## Quando Usar Cada Um?

### **Use SQL quando:**
- ✅ **Dados estruturados** (sempre os mesmos campos)
- ✅ **Relacionamentos complexos** (clientes → pedidos → produtos)
- ✅ **Consistência crítica** (sistema bancário, e-commerce)
- ✅ **Relatórios e análises** (BI, dashboards)

**Exemplos:** Sistema bancário, ERP, CRM

### **Use NoSQL quando:**
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

## Resumo Prático

**SQL = Casa bem organizada:**
- Cada coisa no seu lugar
- Difícil de mudar a estrutura
- Fácil de encontrar tudo relacionado

**NoSQL = Mochila de viagem:**
- Flexível, cabe qualquer coisa
- Fácil de expandir
- Rápido para guardar e tirar coisas

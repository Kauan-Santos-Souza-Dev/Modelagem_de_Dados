As **dependências** em modelagem de dados estabelecem as relações e regras de associação entre os atributos (campos) pertencentes a uma mesma tabela (relação). Identificar como um atributo se relaciona com outro é fundamental para reconhecer falhas de projeto, eliminar redundâncias de dados e fundamentar o processo de **normalização** no banco de dados.

Abaixo está o detalhamento de como funcionam a **Dependência Funcional** (incluindo as variações Total e Parcial), a **Dependência Transitiva** e a **Dependência Multivalorada**.

---

### **1. Dependência Funcional**

A **dependência funcional** ocorre quando o valor de um atributo em uma tabela determina de forma única o valor de outro atributo nessa mesma linha ou registro.

- **Conceito e Notação**: Considerem-se dois atributos quaisquer, \(X\) e \(Y\). Diz-se que \(Y\) é funcionalmente dependente de \(X\) (representado simbolicamente por \(X \rightarrow Y\)) se, para cada valor de \(X\), existir associado exatamente um único valor de \(Y\).
- **Atributo Determinante e Dependente**: O atributo que determina o valor (\(X\)) é chamado de **atributo determinante**, enquanto o atributo determinado (\(Y\)) é chamado de **atributo dependente**. Em geral, a chave primária de uma tabela determina funcionalmente todos os seus atributos não-chave.
- **Exemplo Prático**: Em uma tabela de `pedidos`, considerem-se os campos `número do pedido` e `prazo de entrega`. Observar isoladamente um valor como "15 dias" na coluna de prazo não tem significado completo. Esse prazo de 15 dias depende diretamente do `número do pedido` para saber a qual pedido se refere. Assim, o `número do pedido` determina funcionalmente o `prazo de entrega` (`número do pedido` \(\rightarrow\) `prazo de entrega`).

No contexto de chaves primárias compostas, a dependência funcional é classificada em duas categorias:

#### **a) Dependência Funcional Total**

- **Funcionamento**: Ocorre quando a tabela possui uma **chave primária composta** (formada por dois ou mais atributos) e um atributo não-chave depende de **todas as partes** que compõem a chave primária para existir, e não apenas de uma parte isolada.
- **Exemplo**: Em uma tabela chamada `item_pedido`, a chave primária é composta pela combinação de `número do pedido` e `código do produto`. O campo `quantidade do produto` é um atributo não-chave. Esse campo possui uma dependência funcional total, pois necessita de ambos os campos da chave primária: é preciso saber o `código do produto` para identificar o item, mas também o `número do pedido`, visto que em pedidos diferentes o mesmo produto pode ser vendido em quantidades distintas.

#### **b) Dependência Funcional Parcial**

- **Funcionamento**: Ocorre quando um atributo não-chave depende de apenas **uma parte** da chave primária composta, em vez de depender da chave em sua totalidade.
- **Exemplo**: Em uma tabela chamada `matrículas`, a chave primária é composta pelo `ID do aluno` e pelo `código da disciplina`. O campo `nome da disciplina` depende unicamente do `código da disciplina`. Ele não depende do `ID do aluno`, pois o aluno pode estar matriculado em várias disciplinas distintas. Como o `nome da disciplina` depende de apenas uma parte da chave composta, trata-se de uma **dependência funcional parcial**.

---

### **2. Dependência Funcional Transitiva**

A **dependência funcional transitiva** acontece quando um atributo não-chave não depende diretamente da chave primária da tabela, mas sim de **outro atributo que também não é chave primária**.

- **Funcionamento**: Se a chave primária \(A\) determina o atributo \(B\), e o atributo \(B\) (não-chave) determina o atributo \(C\), então \(C\) possui uma dependência transitiva em relação a \(A\) (\(A \rightarrow B \rightarrow C\)).
- **Exemplo Prático**: Em uma tabela `pedido` cuja chave primária simples é o `número do pedido`, existem os campos `prazo de entrega`, `código do vendedor` e `nome do vendedor`.
    - O `prazo de entrega` depende do `número do pedido`.
    - O `código do vendedor` (uma chave estrangeira) depende do `número do pedido`.
    - Porém, o `nome do vendedor` depende diretamente do `código do vendedor`, e não do `número do pedido`.
- **Impacto**: A existência de dependências transitivas indica que a tabela armazena dados pertencentes a outro conceito ou entidade. No processo de normalização (para atingir a **Terceira Forma Normal - 3FN**), os atributos transitivos devem ser removidos e alocados em uma nova tabela (como uma tabela própria para `vendedor`).

---

### **3. Dependência Multivalorada**

A **dependência multivalorada** ocorre quando, para um determinado valor de um atributo \(A\), existe um **conjunto de múltiplos valores** para outros atributos (\(B\) e \(C\)), sendo que os atributos \(B\) e \(C\) são independentes entre si, mas ambos dependem de \(A\).

- **Sintaxe e Representação**: Representa-se simbolicamente com uma seta de duas pontas: \(A \twoheadrightarrow B\).
- **Exemplo Prático**: Em uma tabela de `automóvel`, existem os campos `modelo`, `ano` e `cor`.
    - Os atributos `ano` e `cor` não dependem um do outro (não é possível determinar a cor a partir do ano de fabricação, nem o ano a partir da cor).
    - No entanto, tanto o `ano` quanto a `cor` dependem do `modelo` do automóvel.
    - Como um mesmo modelo de carro (como "Gol" ou "Uno") pode ser fabricado em múltiplos anos e em diversas cores, a tabela passa a acumular repetições.
- **Impacto**: A dependência multivalorada provoca redundâncias e repetições de linhas. Para corrigi-la, é necessário decompor a tabela em relações menores, isolando os conjuntos de dados repetidos.

---

### **Resumo da Aplicação na Normalização**

|Tipo de Dependência|Onde se manifesta|Solução no Projeto|
|:--|:--|:--|
|**Dependência Parcial**|Chaves primárias compostas onde um atributo depende apenas de parte da chave.|Eliminada na **Segunda Forma Normal (2FN)** movendo o atributo para uma nova tabela.|
|**Dependência Transitiva**|Atributos não-chave que dependem de outros atributos não-chave.|Eliminada na **Terceira Forma Normal (3FN)** isolando o atributo dependente e seu determinante em uma tabela separada.|
|**Dependência Multivalorada**|Atributos independentes entre si associados a um mesmo determinante gerando múltiplos valores.|Resolvida pela decomposição das tabelas para separar as combinações de dados.|

📊 Quer que eu monte um exemplo prático demonstrando o passo a passo da normalização (1FN, 2FN e 3FN) para corrigir essas dependências em uma tabela?
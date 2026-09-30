Em modelagem de bancos de dados, a **cardinalidade** é um conceito fundamental que define a quantidade ou o número de instâncias (itens) de uma entidade que podem estar associadas a instâncias de outra entidade em um relacionamento, e vice-versa.

Ela permite responder a perguntas sobre quantas ocorrências de uma entidade se conectam com a outra em um sistema de informação. A cardinalidade é dividida em dois aspectos principais: **mínima** e **máxima**.

---

### 1. Cardinalidade Mínima e Máxima

- **Cardinalidade Mínima**: Indica o número mínimo de instâncias de uma entidade que _obrigatoriamente_ devem participar do relacionamento.
    - Se a cardinalidade mínima for **0**, significa que o relacionamento é **opcional** (uma instância da entidade pode existir sem estar associada a nenhuma instância da outra).
    - Se for **1** (ou mais), a participação é **obrigatória**.
- **Cardinalidade Máxima**: Indica o número máximo de instâncias de uma entidade que _podem_ participar do relacionamento. Varia de 1 até \(N\) (muitos).

---

### 2. Classificação dos Relacionamentos pela Cardinalidade

A combinação das cardinalidades determina o tipo do relacionamento existente entre as entidades:

#### A. Um para Um (1:1)

Ocorre quando uma única instância da entidade \(A\) está associada a no máximo uma única instância da entidade \(B\), e vice-versa.

- **Exemplo**: O relacionamento entre _Professor_ e _Armário_ (em uma regra de negócio onde um professor usa apenas um armário por vez e aquele armário é de uso exclusivo de um único professor).

#### B. Um para Muitos (1:N)

Ocorre quando uma única instância da entidade \(A\) pode estar associada a múltiplas instâncias (\(N\)) da entidade \(B\), mas cada instância de \(B\) está associada a apenas uma única instância de \(A\).

- **Exemplo**: O relacionamento entre _Departamento_ e _Funcionário_ (um departamento pode ter vários funcionários trabalhando nele, mas cada funcionário pertence a apenas um departamento).

#### C. Muitos para Muitos (N:M)

Ocorre quando várias instâncias da entidade \(A\) podem estar associadas a várias instâncias da entidade \(B\).

- **Exemplo**: O relacionamento entre _Cliente_ e _Pacote de Viagem_ (um cliente pode adquirir diversos pacotes de viagem e um mesmo pacote de viagem pode ser comprado por vários clientes distintos).

---

### 3. Representação Gráfica nos Diagramas (DER)

As cardinalidades são representadas visualmente a depender da notação utilizada no Diagrama Entidade-Relacionamento (DER):

- **Notação de Peter Chen**: Exibe a cardinalidade mínima e máxima dentro de parênteses no formato `(mínimo, máximo)`. Esses valores são posicionados na linha do relacionamento, próximos à entidade correspondente. Alternativamente, pode ser representado apenas com um número ou letra de resumo (como `1` ou `N`).
- **Notação Pé de Galinha (Crow's Foot)**: Utiliza símbolos gráficos nas extremidades das linhas de conexão:
    - Uma **barra vertical** representa a cardinalidade \(1\).
    - Um **círculo** representa a cardinalidade \(0\) (opcionalidade).
    - **Traços inclinados em formato de "pé de galinha"** representam a cardinalidade **Muitos (\(N\))**.

---

### 4. Importância da Cardinalidade na Normalização e Implementação

A identificação correta da cardinalidade é indispensável durante o processo de modelagem e normalização de dados:

- **Problema do Relacionamento N:M**: Os relacionamentos do tipo **Muitos para Muitos (N:M)** são complexos e não podem ser implementados diretamente de forma eficiente em bancos de dados relacionais.
- **Criação de Tabelas/Entidades Associativas**: Quando a cardinalidade revela um relacionamento N:M, a estrutura exige a criação de uma **entidade associativa** (ou tabela intermediária/de junção). Essa entidade intermediária desmembra a relação N:M original em dois relacionamentos simples do tipo **1:N**, tornando o banco totalmente normalizado e pronto para implementação.

---

💡 Quer ver um exemplo prático de como criar uma **entidade associativa** para resolver um relacionamento Muitos para Muitos (N:M)?
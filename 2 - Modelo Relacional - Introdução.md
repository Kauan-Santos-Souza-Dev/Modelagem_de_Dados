O **Modelo Relacional** é um padrão conceitual e estrutural de banco de dados proposto pela primeira vez pelo Dr. Edgar F. Codd em um artigo publicado em junho de 1970, intitulado _"A Relational Model of Data for Large Shared Data Banks"_. Ele surgiu como uma alternativa inovadora para substituir os antigos modelos de redes e hierárquicos que eram utilizados na época.

Sua concepção prática e teórica apoia-se em conceitos matemáticos sólidos, especificamente na **lógica e na teoria de conjuntos**.

---

### **1. Estrutura de Organização dos Dados**

No modelo relacional, os dados são organizados e representados sob a forma de **tabelas bidimensionais**, que matematicamente recebem o nome de **relações** (razão pela qual o modelo é chamado de "relacional"). Embora existam distinções técnicas sobre quando utilizar cada termo, na prática cotidiana de bancos de dados, "relação" e "tabela" referem-se à mesma estrutura básica de dados.

As tabelas são compostas por dois elementos estruturais principais:

- **Tuplas (Linhas ou Registros):** Representam uma ocorrência específica de uma entidade do mundo real (como um cliente específico). A tupla agrupa todos os dados necessários que pertencem àquela ocorrência em particular, tais como o nome, endereço, CPF e telefone de um único cliente.
- **Colunas (Atributos):** São as unidades verticais que armazenam um tipo específico de dado ou valor (como a coluna de nomes ou a coluna de CPFs). Os valores em colunas comuns (não chaves) podem se repetir ao longo das linhas (por exemplo, ter vários clientes chamados "Fábio").

---

### **2. Chaves e Relacionamentos**

Para evitar a redundância (repetição desnecessária de dados), garantir que os dados não fiquem todos concentrados em um único local e permitir que as tabelas sejam cruzadas de forma íntegra, o modelo relacional utiliza **relacionamentos e chaves**:

- **Chave Primária (Primary Key):** É uma coluna (ou combinação de colunas) que serve para identificar cada registro na tabela de maneira absolutamente única. Seus valores nunca se repetem e não podem ser nulos, diferenciando de forma exclusiva ocorrências que poderiam ter nomes iguais (como distinguir dois clientes chamados "Fábio" por meio de seus CPFs ou códigos de identificação).
- **Chave Estrangeira (Foreign Key):** É uma coluna em uma tabela que é utilizada para estabelecer e definir o relacionamento com outra tabela. Ela faz isso ao apontar diretamente para a chave primária (ou para um campo de valor único) da tabela com a qual deseja se conectar.
- **Relacionamento:** É a associação lógica criada entre as tabelas por meio do emprego dessas chaves. Isso permite, por exemplo, associar a tabela de _Clientes_ à tabela de _Produtos_ e descobrir qual cliente realizou determinada compra sem a necessidade de duplicar todas as informações do cliente em cada venda.

O modelo também engloba mecanismos que garantem a **integridade, a precisão e a consistência dos dados**, assegurando que os dados inseridos permaneçam íntegros no decorrer do tempo.

---

### **3. O Processo de Criação: Da Coleta à Modelagem**

Para construir um banco de dados relacional bem-sucedido, o projetista deve seguir etapas cruciais de planejamento antes de partir diretamente para a criação física de tabelas no sistema (o que frequentemente causa erros estruturais):

#### **A. Análise de Requisitos**

Consiste na fase inicial de coleta de informações, na qual o projetista se reúne com o cliente para entender as necessidades e regras de negócio. Essa etapa é essencial para descobrir exatamente quais dados devem ser guardados e quais não devem ser registrados, prevenindo desperdício de esforço e a necessidade de refazer partes do banco no futuro.

#### **B. Modelo Entidade-Relacionamento (MER)**

A partir das regras de negócio extraídas na análise de requisitos, o projetista cria o **Modelo Entidade-Relacionamento (MER)**. Esse modelo ajuda a isolar a informação que precisa ser de fato armazenada das atividades puramente operacionais do negócio. Graficamente, ele se traduz em um **Diagrama Entidade-Relacionamento (DER)**, permitindo enxergar de forma simples como as peças do sistema se amarram.

O MER é estruturado sobre três elementos principais:

1. **Entidades:** Qualquer "coisa" ou objeto do mundo real que possua um significado especial para o negócio e sobre a qual seja necessário guardar dados (exemplos: `CLIENTE`, `PRODUTO`, `VENDEDOR`).
2. **Atributos:** Características que qualificam ou descrevem uma entidade (exemplos: `nome`, `cpf`, `endereço`). Eles podem ser marcados como obrigatórios ou opcionais.
3. **Relacionamentos:** Associações nomeadas por verbos que ligam as entidades entre si (exemplo: CLIENTE _compra_ PRODUTO).

#### **C. Convenções Comuns de Modelagem**

Durante a elaboração do modelo, o projetista costuma adotar convenções para padronizar o projeto:

- **Entidades:** São identificadas por nomes únicos, escritos sempre no **singular** e com letras **maiúsculas** (ex: `CLIENTE`).
- **Atributos:** São escritos no **singular** e com letras **minúsculas** (ex: `cpf`). Atributos obrigatórios recebem um asterisco (`*`), enquanto o atributo que atuará como identificador único da ocorrência recebe um símbolo de hash ou sustenido (`#`).
- **Cardinalidade:** Indica o grau quantitativo máximo e mínimo em que as ocorrências das entidades se associam. Ela define, por exemplo, se um cliente pode comprar um ou múltiplos produtos, ou se um produto pode ser comprado por nenhum ou vários clientes.

---

### **4. Componentes Complementares**

Além de tabelas e chaves, um banco de dados estruturado sob o modelo relacional possui outros recursos importantes para automação, performance e segurança, como:

- **Procedimentos Armazenados (Stored Procedures):** Blocos de código armazenados no banco para executar tarefas repetitivas.
- **Gatilhos (Triggers):** Ações automáticas disparadas por eventos no banco.
- **Índices:** Estruturas que aceleram a velocidade de busca de registros dentro das tabelas.
- **Normalização de Dados:** Um processo fundamental de modelagem voltado para organizar as colunas e tabelas a fim de evitar anomalias e redundâncias.

---

# diferença entre Modelo Relacional e Modelo Entidade Relacionamento. 


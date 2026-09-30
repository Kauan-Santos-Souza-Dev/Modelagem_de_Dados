Em modelagem de bancos de dados, uma **chave** consiste em uma ou mais colunas (atributos) de uma tabela cujos valores são utilizados para identificar de forma exclusiva uma linha (registro) ou um conjunto de linhas. Elas desempenham um papel fundamental na organização dos dados, na prevenção de duplicidades e na definição de relacionamentos e restrições de integridade entre as tabelas.

As chaves são classificadas em duas grandes categorias estruturais:

- **Chaves Únicas**: Identificam unicamente um único registro na tabela.
- **Chaves Não Únicas**: Identificam um conjunto de linhas ou conectam registros entre tabelas.

---

### 1. Chave Primária (Primary Key - PK)

A **Chave Primária** (frequentemente abreviada como **PK**) é a chave candidata que foi escolhida para ser a identificadora principal de uma tabela.

- **Unicidade Absoluta**: Não pode haver repetição ou duplicidade de valores na coluna definida como chave primária.
- **Ausência de Nulos**: Nunca pode aceitar valores nulos (`NOT NULL`), garantindo que todo registro tenha obrigatoriamente um identificador.
- **Representação e Boas Práticas**: Graficamente, costuma ser representada com um sublinhado no nome do atributo ou acompanhada pela sigla **PK**. Recomenda-se utilizar preferencialmente **tipos numéricos** para a chave primária, pois ocupam menos espaço em disco e aceleram o desempenho das consultas e buscas.

---

### 2. Chave Estrangeira (Foreign Key - FK)

A **Chave Estrangeira** (abreviada como **FK**) é uma coluna em uma tabela que estabelece o relacionamento com a chave primária (ou coluna de valor único) de outra tabela.

- **Ponteiro Lógico**: Funciona como uma referência entre tabelas para indicar a qual registro de outra tabela aquela linha está associada.
- **Chave Não Única**: Seus valores podem se repetir na tabela em que se encontra (por exemplo, o ID de um mesmo cliente pode aparecer várias vezes na tabela de vendas).
- **Integridade Referencial**: Para manter a consistência do banco de dados, o valor inserido em uma chave estrangeira deve obrigatoriamente corresponder a um valor existente na chave primária da tabela associada ou ser nulo (caso o relacionamento seja opcional).

---

### 3. Outros Tipos de Chaves em Modelagem de Dados

Além da Chave Primária e da Chave Estrangeira, existem outros conceitos de chaves essenciais no modelo relacional:

#### A. Chave Candidata (Candidate Key)

É qualquer atributo (ou grupo de atributos) que possui o potencial e as condições necessárias para se tornar a chave primária da tabela, por conter apenas valores exclusivos.

- _Exemplo_: Em um cadastro de alunos, tanto o **Número de Matrícula** quanto o **CPF** são chaves candidatas, pois ambos identificam cada aluno de forma única sem repetição.

#### B. Chave Alternativa (Alternative Key)

Quando uma tabela possui mais de uma chave candidata, uma delas é escolhida como a Chave Primária oficial. As chaves candidatas restantes que não foram escolhidas passam a ser chamadas de **Chaves Alternativas**.

#### C. Chave Composta (Composite Key)

É uma chave constituída pela **combinação de dois ou mais atributos** simultaneamente. É utilizada quando nenhum atributo isolado consegue garantir a unicidade do registro.

- _Exemplo_: Em uma tabela de itens de pedidos, o `Número do Pedido` sozinho se repete e o `Código do Produto` sozinho também se repete; contudo, a combinação `Número do Pedido + Código do Produto` gera um valor único para cada item do pedido.

#### D. Chave Substituta / Surrogada / Sintética (Surrogate Key)

É um valor numérico único (frequentemente um número sequencial ou autoincremento) adicionado a uma tabela para servir como chave primária.

- **Características**: Não possui nenhum significado semântico ou utilidade prática para o usuário no mundo real fora do sistema.
- **Aplicações**: É utilizada para simplificar consultas e relacionamentos quando não existe uma chave natural adequada ou quando se quer evitar o uso de uma chave primária composta complexa.

#### E. Chave Natural (Natural Key)

É uma chave baseada em atributos com valores que existem no mundo real fora do banco de dados.

- _Exemplos_: CPF, CNPJ, Placa de Automóvel, Código de Barras de um Produto ou Coordenadas Geográficas.

---

### Exemplo Prático de Associação entre Chaves

Para entender como as chaves se conectam em um banco de dados relacional:

1. **Tabela `Clientes`**: Possui o atributo `ID_Cliente` como **Chave Primária (PK)**.
2. **Tabela `Produtos`**: Possui o atributo `ID_Produto` como **Chave Primária (PK)**.
3. **Tabela `Vendas`**: Para registrar as compras, a tabela armazena a sua própria **Chave Primária** (`ID_Venda`) e inclui as colunas `ID_Cliente` e `ID_Produto` atuando como **Chaves Estrangeiras (FK)**.

Essas chaves estrangeiras conectam cada venda diretamente aos registros correspondentes nas tabelas de clientes e produtos, garantindo a integridade e permitindo consultar exatamente quem comprou o quê.

---

🔑 Quer ver um exemplo de como aplicar **Chaves Compostas** na prática durante o processo de normalização de tabelas?


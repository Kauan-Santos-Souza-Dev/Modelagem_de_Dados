A **Terceira Forma Normal (3FN)** é um dos estágios mais importantes do processo de normalização de bancos de dados relacionais. Proposta originalmente por Edgar F. Codd, a 3FN tem como objetivo principal garantir que cada tabela seja bem formada, eliminando redundâncias de dados e prevenindo anomalias de atualização.

---

### **1. Regra Fundamental da 3FN**

Uma tabela ou relação está na **Terceira Forma Normal (3FN)** quando **não existem dependências funcionais transitivas entre seus atributos não chave**.

Em termos práticos, a regra da 3FN exige que **todos os atributos não chave dependam direta, completa e exclusivamente da chave primária (PK)** da tabela, e não de outros atributos que também não sejam chave.

---

### **2. Pré-requisitos Obrigatórios**

Para que uma relação alcance a 3FN, é necessário seguir uma sequência encadeada de etapas:

1. **Estar na Primeira Forma Normal (1FN)**: Possuir uma chave primária definida e armazenar apenas valores atômicos (indivisíveis), sem conter atributos multivalorados, atributos compostos ou tabelas aninhadas.
2. **Estar na Segunda Forma Normal (2FN)**: Já estar na 1FN e garantir que todos os atributos não chave dependam de **todas** as partes da chave primária (eliminação de dependências parciais em chaves primárias compostas).

As primeira e segunda formas normais servem como um "trampolim" indispensável para que o projeto atinja a 3FN ou a Forma Normal de Boyce-Codd (FNBC).

---

### **3. O que é uma Dependência Transitiva?**

Uma **dependência funcional transitiva** ocorre quando um atributo não chave não depende diretamente da chave primária da tabela, mas sim de **outro atributo que também é não chave**.

- **Esquema conceitual**: \[\text{Chave Primária (PK)} \longrightarrow \text{Atributo Não Chave A} \longrightarrow \text{Atributo Não Chave B}\]
- Nesse cenário, o **Atributo B** possui uma dependência transitiva em relação à Chave Primária, pois ele é determinado diretamente pelo **Atributo A**.

---

### **4. Procedimento de Normalização para a 3FN**

Quando uma dependência transitiva é identificada em uma relação, aplica-se o seguinte processo de decomposição:

1. **Identificação**: Localiza-se o atributo não chave que atua como determinante de outro atributo não chave.
2. **Remoção**: Extrai-se o atributo dependente da tabela original.
3. **Criação de uma Nova Tabela**: Cria-se uma nova relação contendo o atributo removido juntamente com o seu atributo determinante. O atributo determinante é promovido a **Chave Primária (PK)** dessa nova tabela.
4. **Vínculo por Chave Estrangeira**: O atributo determinante é mantido na tabela original na condição de **Chave Estrangeira (FK)**, garantindo a integridade referencial e o relacionamento entre as duas tabelas.

---

### **5. Exemplo Prático de Aplicação**

Considere uma tabela de vendas não normalizada chamada `tbl_venda` contendo as seguintes colunas:

- `nota_fiscal` (**Chave Primária - PK**)
- `codigo_vendedor`
- `nome_vendedor`
- `codigo_produto`
- `quantidade_vendida`

#### **Análise das Dependências**:

- `codigo_produto` e `quantidade_vendida` dependem diretamente do número da `nota_fiscal`.
- `codigo_vendedor` depende diretamente da `nota_fiscal` (para registrar qual vendedor efetuou aquela venda).
- No entanto, o `nome_vendedor` **não depende da nota fiscal**, mas sim do `codigo_vendedor`.
- Como o `codigo_vendedor` não é a chave primária de `tbl_venda`, o `nome_vendedor` possui uma **dependência transitiva**.

#### **Ajuste para a 3FN**:

1. **Nova tabela `tbl_vendedor`**: Criada com as colunas `codigo_vendedor` (**PK**) e `nome_vendedor`.
2. **Tabela `tbl_venda` ajustada**: Mantém as colunas `nota_fiscal` (**PK**), `codigo_vendedor` (**Chave Estrangeira - FK**), `codigo_produto` e `quantidade_vendida`.

Dessa forma, elimina-se a repetição contínua do nome do vendedor a cada nova nota fiscal e previne-se o risco de inconsistências de cadastro.

---

### **6. Objetivos e Benefícios da 3FN**

- **Minimização da Redundância**: Evita o armazenamento repetido das mesmas informações em várias linhas.
- **Eliminação de Anomalias**: Impede problemas de inserção (ex: precisar de uma nota fiscal para cadastrar um vendedor), exclusão (ex: perder dados do vendedor ao apagar uma venda) e alteração.
- **Padrão Recomendado na Prática**: Para a grande maioria das aplicações reais de bancos de dados relacionais, normalizar até a Terceira Forma Normal é suficiente para assegurar uma estrutura limpa e performática.

---

💡 Quer explorar a **Forma Normal de Boyce-Codd (FNBC)** para entender como resolver casos específicos com múltiplas chaves candidatas compostas e sobrepostas?
A **Primeira Forma Normal (1FN)** é a regra inicial e fundamental do processo de normalização de bancos de dados relacionais, formulada originalmente por Edgar F. Codd. O seu propósito principal é garantir que a estrutura de uma relação (tabela) seja bem formada, eliminando **atributos multivalorados**, **atributos compostos** e **relações aninhadas**.

---

### **1. Requisitos para uma Tabela estar na 1FN**

Para que uma tabela seja considerada na Primeira Forma Normal, ela deve satisfazer rigorosamente aos seguintes critérios:

- **Existência de Chave Primária**: A tabela precisa possuir obrigatoriamente um identificador único (chave primária) para cada registro.
- **Valores Atômicos (Indivisíveis)**: Todos os campos em cada linha (registro/tupla) devem armazenar apenas um único valor atômico, ou seja, um dado indivisível dentro do contexto do sistema.
- **Ausência de Atributos Multivalorados**: Não pode haver colunas que armazenem múltiplos valores no mesmo campo para um único registro.
- **Ausência de Atributos Compostos**: Não pode haver colunas que reúnam diferentes subinformações em um mesmo campo.
- **Ausência de Relações Aninhadas**: A tabela não pode conter "tabelas internas" ou grupos repetitivos de colunas embutidos dentro de um mesmo registro.

---

### **2. Conceitos-Chave da 1FN**

#### **a) Dados Atômicos**

Dados atômicos representam o nível mais baixo e indivisível de detalhamento da informação. Quando um valor é armazenado de forma única e direta em sua célula na relação, ele atende ao princípio da atomicidade. Por exemplo, armazenar separadamente `nome` e `sobrenome` garante a atomicidade em comparação com armazenar o nome completo em um único campo monolítico.

#### **b) Atributos Compostos**

Um atributo é considerado composto quando pode ser desmembrado em vários subatributos menores.

- **Exemplo clássico**: O atributo `endereço`. Armazenar o endereço completo (_Rua, Número, Bairro, CEP, Cidade, Estado_) em uma única coluna é uma violação da atomicidade. Isso dificulta a realização de consultas, ordenações e pesquisas específicas (como filtrar todos os clientes de um determinado bairro ou CEP).

#### **c) Atributos Multivalorados**

Um atributo é multivalorado quando pode assumir mais de um valor para uma única ocorrência de uma entidade.

- **Exemplo clássico**: O atributo `telefone`. Um mesmo cliente ou aluno pode possuir telefone residencial, celular e comercial. Tentar registrar múltiplos números na mesma célula ou criar colunas repetitivas na mesma linha viola a 1FN.

#### **d) Relações Aninhadas**

Ocorre quando existe uma estrutura tabular embutida dentro de outra tabela. Isso acontece quando um conjunto de colunas repetitivas cria uma tabela interna dentro de um registro da tabela principal.

---

### **3. Como Resolver as Violações da 1FN**

Para conduzir uma tabela não normalizada até a Primeira Forma Normal, aplica-se o seguinte procedimento de decomposição:

1. **Tratamento de Atributos Compostos**:
    
    - **Solução**: Desmembrar a coluna composta em colunas simples/atômicas diretamente na própria tabela.
    - _Exemplo_: A coluna `endereço` é dividida nas colunas atômicas `rua`, `numero`, `bairro`, `cep`, `cidade` e `estado`.
2. **Tratamento de Atributos Multivalorados**:
    
    - **Solução**: Remover a coluna multivalorada da tabela original e criar uma **nova tabela** (relação separada) dedicada exclusivamente a armazenar esses múltiplos valores.
    - A nova tabela é associada à tabela principal através do relacionamento entre a chave primária da tabela origem (que passa a atuar como chave estrangeira na nova tabela) e o atributo extraído.
    - _Exemplo_: Remove-se o campo `telefone` da tabela de `alunos` e cria-se a tabela `telefones_aluno`, contendo o `RA_aluno` (chave estrangeira) e o número de `telefone`.

---

### **4. Papel da 1FN no Processo Global de Normalização**

A Primeira Forma Normal é o ponto de partida indispensável na modelagem relacional. Embora alinhe a tabela para conter apenas valores atômicos e elimine os grupos repetitivos, a 1FN isoladamente ainda não elimina todas as dependências parciais ou transitivas, nem todas as anomalias de atualização (inclusão, exclusão e alteração). Por essa razão, a 1FN serve como um "trampolim" obrigatório para que o projeto avance para a **Segunda Forma Normal (2FN)** e a **Terceira Forma Normal (3FN)**.

---

🛠️ Quer que eu monte um exemplo prático mostrando uma tabela antes e depois da aplicação da 1FN para ver como fica a separação dos campos na prática?
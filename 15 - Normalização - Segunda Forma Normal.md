A **Segunda Forma Normal (2FN)** é um estágio crucial no processo de normalização de bancos de dados relacionais, cujo objetivo principal é organizar as tabelas para minimizar a redundância e eliminar anomalias de atualização.

---

### **1. Pré-requisito Obrigatório**

Para que uma tabela ou relação alcance a Segunda Forma Normal, é requisito indispensável que ela **já esteja completamente ajustada à Primeira Forma Normal (1FN)**. Isso significa que a tabela já possui uma chave primária definida e que todos os seus atributos contêm apenas valores atômicos (indivisíveis), sem a presença de atributos multivalorados, compostos ou relações aninhadas.

---

### **2. Regra Fundamental da 2FN**

Uma tabela está na Segunda Forma Normal quando **todos os atributos não chave forem total e funcionalmente dependentes de todas as partes da chave primária**.

Em termos práticos, a 2FN exige a **eliminação de dependências funcionais parciais**:

- **Dependência Funcional Total**: Ocorre quando um atributo não chave precisa da chave primária em sua totalidade para ser determinado de forma única.
- **Dependência Funcional Parcial**: Ocorre quando a tabela possui uma **chave primária composta** (formada por dois ou mais atributos) e um atributo não chave depende de apenas **uma parte** dessa chave primária, e não de todas as suas partes.

> **Nota sobre Chaves Simples**: Se uma tabela já está na 1FN e possui uma chave primária simples (formada por um único atributo), ela atende automaticamente ao critério da 2FN no que tange às dependências parciais de chave composta, pois não há "partes" para fracionar a chave primária.

---

### **3. Procedimento para Normalizar uma Tabela até a 2FN**

Quando é identificada uma dependência parcial em uma relação, aplica-se o seguinte processo de decomposição:

1. **Identificação dos Atributos**: Analisa-se cada coluna não chave para identificar se ela depende da chave primária inteira ou apenas de uma parte dela.
2. **Extração das Dependências Parciais**: Remove-se o atributo que possui dependência parcial da tabela original.
3. **Criação de uma Nova Tabela**: Cria-se uma nova relação contendo o atributo removido juntamente com o atributo determinante (a parte da chave da qual ele dependia).
4. **Vínculo por Chave Estrangeira**: O atributo determinante torna-se a chave primária da nova tabela e permanece na tabela de origem atuando como chave estrangeira, garantindo a integridade referencial e o relacionamento entre ambas.

---

### **4. Exemplo Prático de Aplicação**

Imaginemos uma tabela chamada `peça` com os seguintes campos:

- **Chave Primária Composta**: (`código da peça`, `código do fornecedor`).
- **Atributos Não Chave**: `local do fornecedor`, `telefone do fornecedor` e `quantidade em estoque`.

**Análise das Dependências**:

- A `quantidade em estoque` depende da combinação completa de `código da peça` e `código do fornecedor` (dependência funcional total), pois a quantidade em estoque varia de acordo com qual peça e qual fornecedor estão associados.
- No entanto, o `local do fornecedor` e o `telefone do fornecedor` dependem **apenas** do `código do fornecedor`, não dependendo do `código da peça`. Trata-se de uma **dependência funcional parcial**.

**Ajuste para a 2FN**:

- Extraem-se os atributos `local do fornecedor` e `telefone do fornecedor` para uma nova tabela chamada `fornecedor`, onde o `código do fornecedor` atua como chave primária.
- A tabela `peça` permanece com a chave primária composta (`código da peça`, `código do fornecedor`) e o campo `quantidade em estoque`.

---

### **5. Importância da Segunda Forma Normal**

- **Prevenção de Anomalias**: Impede falhas de inserção, exclusão e alteração (por exemplo, ter que repetir o endereço de um fornecedor para cada peça que ele fornece).
- **Redução de Redundância**: Garante que os dados sejam alocados nas tabelas corretas.
- **Etapa de Transição**: A 2FN serve como um "trampolim" indispensável para conduzir o banco de dados até a **Terceira Forma Normal (3FN)** ou à **Forma Normal de Boyce-Codd (FNBC)**, onde as dependências transitivas serão eliminadas.

---

💡 Se quiser, posso te explicar como funciona o próximo passo para alcançar a **Terceira Forma Normal (3FN)** ou mostrar outro exemplo de decomposição de tabelas!
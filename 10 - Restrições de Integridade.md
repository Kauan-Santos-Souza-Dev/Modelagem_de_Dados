As **Restrições de Integridade** (frequentemente chamadas pelo termo em inglês, _constraints_) são regras e mecanismos aplicados às colunas e tabelas de um banco de dados relacional para garantir a **manutenção, consistência e precisão (acurácia) dos dados**. A função dessas restrições é impedir que dados corrompidos, inválidos ou incoerentes sejam inseridos, modificados ou mantidos no sistema.

Segundo as regras do modelo relacional, as restrições de integridade devem ser **definidas diretamente no nível do banco de dados** (armazenadas no catálogo/dicionário de dados) e gerenciadas pelo SGBD, em vez de ficarem isoladas no código das aplicações. Isso garante que a lógica de integridade seja aplicada de forma consistente, independentemente de qual aplicativo ou usuário esteja interagindo com o banco.

As restrições de integridade dividem-se em **cinco categorias principais**:

---

### 1. Integridade de Domínio

A integridade de domínio estabelece que todo valor inserido em uma coluna deve obedecer estritamente ao conjunto de valores permitidos (o **domínio**) para aquele atributo específico.

- **Como funciona**: É influenciada pelo tipo de dado (numérico, texto, data), pela representação interna, pela precisão (ex.: número de casas decimais) e pelos intervalos de valores aceitos.
- **Exemplo**: Em uma coluna destinada a armazenar o preço de uma mercadoria, a restrição de domínio garante que apenas números sejam aceitos. O sistema rejeitará entradas em texto por extenso (como `"vinte reais"`). Além disso, pode limitar o intervalo permitido, impedindo a gravação de preços negativos (ex.: `R$ -32,00`), já que não fazem sentido dentro do negócio.

---

### 2. Integridade Referencial

A integridade referencial garante a consistência das referências criadas entre tabelas distintas através de relacionamentos.

- **Como funciona**: Conecta uma **Chave Estrangeira (FK)** em uma tabela a uma **Chave Primária (PK)** em outra tabela. A regra exige que qualquer valor inserido na chave estrangeira corresponda obrigatoriamente a um valor que já existe na chave primária da tabela referenciada (ou seja nulo, caso o relacionamento seja opcional).
- **Exemplo**: Se você tentar registrar uma venda inserindo o código de um produto que não existe no cadastro da tabela de produtos, o banco de dados rejeita a operação para evitar a violação da referência.
- **Propagação em Cascata**: A integridade referencial também lida com operações de alteração ou exclusão no registro "pai". É possível configurar o banco para que, ao excluir um autor, por exemplo, os livros vinculados a ele sejam excluídos automaticamente em cascata ou a exclusão seja bloqueada para não deixar registros "órfãos" no sistema.

---

### 3. Integridade de Chave

A integridade de chave é a garantia associada diretamente à **Chave Primária (PK)** de uma tabela.

- **Como funciona**: Exige que os valores gravados na coluna definida como chave primária sejam **estritamente únicos** (sem duplicações) e **nunca nulos**.
- **Objetivo**: Garante que cada linha (registro ou tupla) de uma tabela possa ser identificada de forma exclusiva e unívoca em relação a todas as outras.

---

### 4. Integridade de Vazio (ou de Nulo)

Esta restrição dita se uma coluna tem o preenchimento obrigatório ou se pode permanecer sem nenhum valor registrado.

- **Como funciona**: No momento da modelagem, define-se se o atributo aceita ou não valores nulos:
    - **Não Nulo (`NOT NULL`)**: O preenchimento do campo é obrigatório no cadastro do registro. A chave primária é um exemplo de coluna obrigatoriamente não nula.
    - **Nulo (`NULL`)**: O campo é opcional. Em banco de dados, o termo _Nulo_ (`NULL`) significa a ausência total e completa de dados (diferente do número zero ou de uma sequência de espaços em branco).
- **Exemplo**: O nome de um aluno é um campo obrigatório (`NOT NULL`), enquanto o campo de telefone pode ser opcional (`NULL`), permitindo o cadastro caso o aluno não possua telefone no momento.

---

### 5. Integridade Definida pelo Usuário

São restrições personalizadas criadas para atender a **regras de negócio específicas** de uma organização ou aplicação, indo além das validações básicas do SGBD.

- **Como funciona**: Permite impor condições mais complexas ou específicas para validar a entrada de dados.
- **Exemplos**: Definir que o valor de uma coluna deve pertencer a um conjunto estrito de valores específicos ou que o dado só pode ser gravado se atender ao resultado de um cálculo matemático ou de uma validação condicional prévia.

---

### Boas Práticas ao Nomear Restrições (Constraints)

Ao criar as restrições no banco de dados através de comandos SQL, é uma boa prática **nomear explicitamente cada restrição** em vez de deixar que o SGBD gere nomes aleatórios ou automáticos.

Recomenda-se adotar um padrão coerente utilizando **prefixos** para indicar o tipo da restrição:

- `PK_` para Chaves Primárias (ex.: `PK_ID_AUTOR`).
- `FK_` para Chaves Estrangeiras (ex.: `FK_ID_EDITORA`).

Essa padronização simplifica a manutenção futura, o controle e a alteração da estrutura das tabelas.

💡 Quer entender como funcionam e como se comportam as atualizações e exclusões em cascata (`CASCADE`) na integridade referencial?
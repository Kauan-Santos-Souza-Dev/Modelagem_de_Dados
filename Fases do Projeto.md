 
- Levantamento de Requisitos
- Identificação de Entidades e Relacionamentos e atríbutos
- Diagram Entidade Relacionamento (ER)
- Dicionário de Dados
- Normalização 
- Implementação 
- Testes básicos


No contexto do projeto prático de modelagem de dados para o gerenciamento de uma faculdade, o desenvolvimento é estruturado em **fases sequenciais e iterativas** que orientam o projeto desde a concepção abstrata até a execução física e validação no banco de dados.

As fases principais do projeto prático dividem-se nas seguintes etapas:

---

### **1. Levantamento de Requisitos e Regras de Negócio**

- O projeto inicia-se com a coleta e a análise detalhada das **regras de negócio** passadas pelo cliente ou pela organização fictícia.
- O objetivo desta etapa é compreender quais dados precisam ser armazenados e centralizados (como informações de alunos, professores, cursos, disciplinas e histórico escolar) e quais informações não devem entrar no sistema para evitar desperdício de recursos.
- Essa documentação serve de alicerce para todas as decisões técnicas tomadas nas fases seguintes do projeto.

---

### **2. Identificação de Entidades, Atributos e Relacionamentos**

- Como parte integrante da análise inicial, examina-se o texto das regras de negócio para extrair os componentes fundamentais do modelo.
- **Entidades**: Identificam-se as categorias ou conceitos principais observando os substantivos que possuem múltiplas ocorrências ou instâncias (por exemplo: `Aluno`, `Professor`, `Disciplina`, `Curso` e `Departamento`).
- **Relacionamentos**: Analisam-se os verbos de ação que conectam as entidades para determinar como elas se associam dentro do contexto do negócio (por exemplo: `Aluno` _está matriculado em_ `Curso`, `Professor` _ministra_ `Disciplina`).
- **Atributos**: Determinam-se os campos qualificadores e descritivos pertencentes a cada entidade (como o `RA` do aluno, o `nome do professor`, a `carga horária` da disciplina e a `descrição`).

---

### **3. Elaboração do Modelo Entidade-Relacionamento (MER) e Diagrama Entidade-Relacionamento (DER)**

- A partir dos elementos identificados, constrói-se o **Modelo Entidade-Relacionamento (MER)** e a sua representação gráfica, o **Diagrama Entidade-Relacionamento (DER)**.
- O DER é construído de forma contínua e sofre modificações e refinamentos à medida que a análise avança.
- **Cálculo das Cardinalidades**: Define-se a quantidade mínima e máxima de instâncias que podem participar de cada relacionamento em ambas as direções (como 1:1, 1:N ou N:M).
- **Tratamento de Relacionamentos Muitos-para-Muitos (N:M)**: Para eliminar problemas de implementação física e redundância de dados, os relacionamentos N:M são desmembrados através da criação de **entidades associativas** intermediárias (como `Curso_Disciplina` ou `Prof_Disciplina`).

---

### **4. Criação e Atualização do Dicionário de Dados**

- O **Dicionário de Dados** (ou repositório de metadados) é elaborado como um documento formal para detalhar tecnicamente todos os objetos que compõem a modelagem.
- É mantido e atualizado constantemente ao longo do desenvolvimento do trabalho.
- Para cada tabela e atributo, o dicionário registra o **tipo de dado** (domínio), o **comprimento/tamanho em bytes**, as **restrições** (_Primary Key_, _Foreign Key_, _NOT NULL_, _UNIQUE_), os **valores padrão** e uma **descrição textual** detalhada da sua finalidade.

---

### **5. Derivação do Modelo Lógico**

- Transforma-se o diagrama conceitual (DER) em um **Modelo Lógico**, estruturando a informação na forma de tabelas relacionais compostas por linhas (tuplas) e colunas.
- Nesta etapa, especificam-se os tipos de dados e são explicitadas as **Chaves Primárias (PK)** e **Chaves Estrangeiras (FK)** necessárias para efetivar as conexões lógicas entre as tabelas.

---

### **6. Processo de Normalização do Banco de Dados**

- Aplica-se a **Normalização** sobre as tabelas do modelo lógico para eliminar anomalias de atualização (inclusão, exclusão e alteração) e minimizar a redundância de dados.
- O processo executa testes encadeados divididos em três Formas Normais (FN) principais:
    1. **Primeira Forma Normal (1FN)**: Exige a presença de chave primária e valores atômicos (indivisíveis), eliminando atributos multivalorados, compostos e tabelas aninhadas.
    2. **Segunda Forma Normal (2FN)**: Exige que a tabela já esteja na 1FN e elimina dependências funcionais parciais em chaves primárias compostas.
    3. **Terceira Forma Normal (3FN)**: Exige que a tabela já esteja na 2FN e elimina dependências funcionais transitivas entre atributos não chave.
- Como resultado da normalização, tabelas com anomalias são decompostas e novas tabelas são criadas (como tabelas separadas para os telefones ou endereços dos alunos).

---

### **7. Implementação Física do Banco de Dados (SGBD)**

- Traduz-se o modelo lógico totalmente normalizado em comandos SQL executáveis em um Sistema de Gerenciamento de Banco de Dados relacional (como o MySQL).
- São executados scripts de criação do banco de dados (`CREATE DATABASE`), criação das tabelas (`CREATE TABLE`) com suas restrições e relacionamentos (_FKs_), e realiza-se a carga inicial de dados fictícios (`INSERT INTO`) para povoar o sistema.

---

### **8. Testes Finais e Validação**

- Na última etapa do projeto, realizam-se **testes práticos** executando consultas SQL (`SELECT`, junções com `INNER JOIN`, filtros `WHERE` e ordenações `ORDER BY`) para validar se a estrutura criada atende corretamente a todas as perguntas e requisitos do negócio.
- Essa fase permite diagnosticar e corrigir eventuais inconformidades de tipos de dados ou dados ausentes antes da utilização definitiva do banco de dados.

---

💡 Se quiser, posso detalhar como funciona a transição do modelo conceitual para o modelo lógico ou explicar como desmembrar um relacionamento N:M na prática criando uma entidade associativa!
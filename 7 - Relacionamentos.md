Em modelagem de dados, um **relacionamento** é uma associação nomeada entre entidades que indica como elas se conectam ou interagem no contexto de um negócio. Sua função principal é integrar dados armazenados em tabelas distintas, permitindo responder a consultas e necessidades dos usuários (como identificar qual cliente comprou determinado produto).

---

### Principais Características dos Relacionamentos

#### 1. Representação Gráfica no DER

- **Símbolo**: No Diagrama Entidade-Relacionamento (DER), é representado por um **losango**.
- **Conexões**: Linhas conectam o losango às entidades participantes.
- **Nomeação**: Geralmente recebe o nome de um **verbo de ação** que descreve a relação (como _compra_, _trabalha_ ou _prescreve_).

#### 2. Grau do Relacionamento

Indica a quantidade de entidades envolvidas no relacionamento:

- **Unário (ou Autorrelacionamento)**: Ocorre quando uma entidade se relaciona com ela mesma (exemplo: _Pessoa_ "se casa com" _Pessoa_).
- **Binário**: Conecta duas entidades (é o tipo mais frequente, como _Funcionário_ "trabalha em" _Setor_).
- **Ternário**: Associa três entidades simultaneamente (exemplo: _Médico_ "prescreve" _Medicamento_ para _Paciente_).

#### 3. Cardinalidade

Define o número mínimo e máximo de instâncias de uma entidade que podem estar associadas a instâncias de outra entidade. Os tipos principais são:

- **Um para Um (1:1)**
- **Um para Muitos (1:N)**
- **Muitos para Muitos (N:M)**

#### 4. Implementação no Banco de Dados

Na prática, em bancos de dados relacionais, o relacionamento entre tabelas é efetuado ligando a **Chave Primária (PK)** de uma tabela à **Chave Estrangeira (FK)** localizada em outra tabela.

---

💡 Quer entender como resolver relacionamentos do tipo **Muitos para Muitos (N:M)** criando tabelas associativas, ou prefere aprofundar em **cardinalidades**?
No Modelo Entidade-Relacionamento (MER), os **atributos** são os elementos utilizados para descrever, qualificar ou caracterizar as propriedades de uma entidade. Eles representam as características ou qualidades dos dados que necessitamos armazenar no banco de dados. Por exemplo, para descrever e caracterizar a entidade `CLIENTE`, o sistema necessita de atributos específicos como `nome`, `sobrenome`, `endereço`, `telefone` e `cpf`.

Para compreender a fundo o papel e o funcionamento dos atributos no contexto de modelagem relacional de dados, é necessário analisar suas formas de representação gráfica, suas regras de nomenclatura e suas diferentes classificações técnicas:

---

### **1. Representação Gráfica e Textual**

No desenvolvimento de um Diagrama Entidade-Relacionamento (DER), existem duas formas principais de exibir os atributos:

- **Representação Gráfica (Peter Chen):** O padrão oficial estabelecido pelo criador do modelo, Dr. Peter Chen, define que os atributos devem ser desenhados utilizando **elipses** (ovais) conectadas à respectiva entidade por meio de uma linha de ligação. No entanto, como o uso de muitas elipses ao redor de uma entidade pode gerar poluição visual no diagrama, os projetistas também adotam a prática de escrever apenas o nome do atributo ligado diretamente ao retângulo da entidade por uma linha de ligação simples.
- **Representação Textual:** Na modelagem puramente textual, os atributos são expressos listando-se o nome da entidade (em caixa alta) seguido de seus respectivos atributos escritos entre parênteses (exemplo: `PRODUTO (nome_do_produto, cod_produto)`).

---

### **2. Boas Práticas e Convenções de Nomenclatura**

Para manter a consistência do projeto e garantir que a posterior implementação física em códigos (como comandos SQL) ocorra sem falhas ou erros de sintaxe nos Sistemas de Gerenciamento de Banco de Dados (SGBDs), adota-se um conjunto de convenções para os atributos:

- **Letras Minúsculas (Caixa Baixa):** Os nomes dos atributos devem ser escritos com letras minúsculas.
- **Uso no Singular:** Assim como as entidades, os atributos são nomeados no singular (exemplo: `cpf` em vez de cpfs).
- **Evitar Espaços e Caracteres Especiais:** Não devem ser utilizados espaços em branco, acentuações ou caracteres especiais ao nomear atributos. Caracteres como cifrão, sustenido ou _underline_ são aceitos em alguns SGBDs, mas a recomendação geral é evitar caracteres complexos para garantir compatibilidade.
- **Símbolos Marcadores:** No modelo conceitual, os atributos obrigatórios recebem um asterisco (`*`) antes do seu nome. Já o atributo que atua como o identificador exclusivo daquela entidade recebe um símbolo de hash ou sustenido (`#`).

---

### **3. Classificação Técnica dos Atributos**

Os atributos não são todos iguais. Dependendo de suas características físicas ou de negócio, eles são classificados em diferentes categorias, exigindo tratamentos específicos por parte do projetista na hora de planejar a estrutura final do banco de dados:

#### **A. Obrigatórios vs. Opcionais**

- **Atributos Obrigatórios:** São aqueles cujo preenchimento é estritamente essencial e indispensável para a integridade do sistema, não podendo ficar vazios (como o `cpf` em um cadastro de clientes).
- **Atributos Opcionais:** São dados que podem ou não ser registrados no sistema, caso a ocorrência não possua aquela informação (como o número de `telefone` de um cliente que não possui aparelho).

#### **B. Simples (Atômicos) vs. Compostos**

- **Atributos Compostos:** São características que podem ser logicamente subdivididas em partes menores, onde cada parte constitui um atributo simples por si só. O exemplo clássico é o `endereço`, que pode ser desmembrado em `rua`, `número`, `bairro`, `cidade` e `cep`.
- **Regra de Implementação:** Via de regra, o projetista deve desmembrar os atributos compostos em seus atributos simples (atômicos) na hora de modelar e salvar a informação para facilitar pesquisas futuras.

#### **C. Monovalorados vs. Multivalorados**

- **Atributos Multivalorados:** São aqueles que podem armazenar mais de um valor para um único registro de entidade. O exemplo mais comum é o `telefone`, visto que um mesmo cliente ou funcionário pode ter vários números associados (celular, telefone fixo, telefone de recado, etc.).
- **Identificação e Tratamento:** No diagrama, os atributos multivalorados são identificados graficamente com um **asterisco posicionado antes de seus nomes** (exemplo: `*telefone`). Por gerarem problemas de armazenamento físico de dados (como a necessidade de definir colunas vazias ou de limitar a quantidade de números inseridos), esses atributos devem ser tratados posteriormente no processo de **normalização** do banco de dados.

#### **D. Determinantes, Chaves e Identificadores**

- **Atributo Determinante:** É o atributo (ou conjunto deles) encarregado de identificar de forma absolutamente única e exclusiva cada uma das *instâncias* de uma entidade. O valor de um atributo determinante **nunca se repete** de um registro para o outro. Exemplos práticos incluem o `cnpj` em uma tabela de empresas ou um `código de produto`. No diagrama, o atributo determinante deve ter o seu nome grafado com um **sublinhado** e receber a marcação de sustenido (`#`).

Complemento: **Instância de Entidade (ou Ocorrência):** É um objeto específico, um registro real e individual que pertence àquela classe de entidade e que possui valores específicos para os atributos definidos.
    - _Exemplo:_ Um "Fiesta Azul, de placa J..." é uma **instância** (ocorrência) específica da entidade `CARRO`. Embora cada instância tenha valores de qualidades diferenciados (um carro é azul, o outro pode ser vermelho), todos seguem a mesma estrutura de dados especificada pela entidade.

- **Atributos Chaves (Chaves): Identificador Exclusivo** São usados para identificar ocorrências de entidades. Embora o conceito seja similar, existe uma distinção técnica: enquanto o atributo determinante _nunca_ se repete de uma instância para outra, o termo "chave" pode ser flexibilizado. Existem as _chaves únicas_ (que funcionam como determinantes e não se repetem) e as _chaves não únicas_ (que podem se repetir e servem para agrupar instâncias em categorias ou para conectar tabelas, como as chaves estrangeiras). As chaves também podem ser compostas pela combinação de dois ou mais atributos simples.

    - Instância: Lamborghini Huracán, **placa ABC-1234**, cor amarela, ano 2023, dono João Silva

Aqui, **placa** é o atributo identificador (chave). Por quê? Porque não existem duas placas iguais — então se você tem 1000 instâncias de carro no banco, a placa é o valor que garante que você está falando _desse_ carro específico e não de outro.

Pra fixar a diferença de raciocínio:

- ❌ "usamos a chave pra achar a instância" (como se fosse uma busca externa)
- ✅ "a chave é um atributo que já está dentro da instância, e é o que garante a unicidade dela"
---

### **A Transição para o Modelo Físico**

No ciclo de vida do projeto, quando passamos da fase conceitual (MER) para a lógica e física, **os atributos dão origem às colunas (campos) das tabelas físicas**. Caso o mapeamento dos atributos não seja realizado com cuidado — identificando corretamente quais são compostos, multivalorados ou determinantes —, o banco de dados final sofrerá com sérias anomalias, como perda de integridade de dados e graves problemas de redundância (duplicação desnecessária de informações).

---

📞 Que tal criarmos um quiz interativo rápido com 5 perguntas objetivas para você testar como esses diferentes tipos de atributos são mapeados na prática?
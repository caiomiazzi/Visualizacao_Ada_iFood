# Aula 3

## Dataset Disney

Esse dataset da disney é todo composto por arquivos CSVs. Pra gente começar nossa análise, vamos primeiro importar todos os dados pra dentro do Power BI e, a partir disso, explorar as tabelas e os dados em busca de hipóteses que seriam legais de a gente acompanhar.

O contexto desse dataset é explorar as receitas da disney de acordo com os filmes produzidos. Ou seja, basicamente informações financeiras.

Esse dataset tem a tabela de receitas dos filmes (**disney_movies_total_gross**) podemos ver algumas colunas como gênero, receita, receita ajustada pela inflação, a classificação indicativa e a data do lançamento.

Tem um segundo dataset de receitas (**disney_revenue_1991_2016**), só que esse dataset considera a Disney como um todo. Ele divide as receitas por estúdio, incluindo inclusive os parques e resorts. Um detalhe desse dataset é que a receita é anualizada, e não tem aberta ela mês a mês.

Temos também um dataset de personagens (**disney-characters**), com informações sobre o nome do filme, o principal vilão e herói, quando o filme saiu e até uma música do filme.

Temos um dataset dos diretores dos filmes (**disney-directors**), que vai nos habilitar construir filtros de acordo com o diretor.

E por fim a tabela de dubladores dos personagens (**disney-voice-actors**)

&nbsp;

### Modelagem

Antes de começar a construir o dashboard, e de formular hipóteses, vamos ver como essas tabelas se relacionam entre si. Para isso, vamos na aba de Modelagem (Aba de Exibição do modelo) e podemos ver que o Power BI já fez algumas relações entre as tabelas e os dados.

&nbsp;

#### disney-directors <-> disney_movies_total_gross

Na minha importação, ele relacionou aqui a tabela de diretores **disney-directors** com a tabela de receitas dos filmes**disney_movies_total_gross**, utilizando a coluna de índice. Será que isso faz sentido? Bom, vamos ver os dados.

Pelo que a gente consegue identificar, não parece correto esse mapeamento, já que os nomes dos filmes não parece bater com a ordem dos diretores dos filmes.

Enão vamos excluir esse relacionamento.

- Aba de Exibição do modelo
- Gerenciar Relações
- Selecionar o relacionamento e apertar em excluir

&nbsp;

#### disney-director <-> disney-characters

Explorando as tabelas, parece existir uma relação entre a tabela de diretores **disney-director** e a de personagens **disney-characters**. Apesar de não ser o melhor campo para fazer essa relação, podemos uasr a coluna de índice pra relacionar essas tabelas, já que parece estar na mesma ordem os dados.

Observem que algums dados podem divergir de uma tabela para outra. O filme 101 Dálmatas, na tabela de diretores está escrito com numeral (*101 Dalmatians*), enquanto na tabela de personagens está por extenso (*One hundred and one Dalmatians*). Então nesse ponto a coluna de índice vai ajudar a fazer a relação correta.

Vamos criar uma relação nova entre essas tabelas, caso não exista.

- Aba de Exibição do modelo
- Gerenciar Relações
- Novo
- Selecionar **disney-director.index** e **disney-characters.index**
- Cardinalidade: **Um para Um (1:1)**
- Direção do filtro cruzado: **Ambas**
- Ativar este relacionamento

&nbsp;

#### disney_movies_total_gross <-> disney-voice-actors

Na minha importação, ele relacionou aqui a tabela de receitas dos filmes **disney_movies_total_gross** com a tabela de dubladores **disney-voice-actors**, utilizando a coluna de índice. Não parece correto esse mapeamento também, já que a tabela de dubladores possui várias linhas para um mesmo filme. Então podemos exluir ele.

- Aba de Exibição do modelo
- Gerenciar Relações
- Selecionar o relacionamento e apertar em excluir

&nbsp;

#### disney_movies_total_gross <-> disney_revenue_1991-2016

Outra relação que o Power BI fez, que não parece ter sentido é a de receita de filmes **disney_movies_total_gross** com a de receita geral da Disney **disney_revenue_1991-2016**. Não tem a relação entre os índices, então vamos remover ela também.

- Aba de Exibição do modelo
- Gerenciar Relações
- Selecionar o relacionamento e apertar em excluir

&nbsp;

#### disney_movies_total_gross <-> disney-characters

Outra relação que o Power BI fez, que não parece ter sentido é a de receita de filmes **disney_movies_total_gross** com a de personagens **disney-characters**. Não tem a relação entre os índices, então vamos remover ela também.

- Aba de Exibição do modelo
- Gerenciar Relações
- Selecionar o relacionamento e apertar em excluir

&nbsp;

#### disney_revenue_1991-2016 <-> disney-characters

Outra relação que o Power BI fez, que não parece ter sentido é a de receita da Disney **disney_revenue_1991-2016** com a de dubladores **disney-voice-actors**. Não tem a relação entre os índices, então vamos remover ela também.

- Aba de Exibição do modelo
- Gerenciar Relações
- Selecionar o relacionamento e apertar em excluir

&nbsp;

#### disney-characters <-> disney-voice-actors

Podemos relacionar a tabela de personagens **disney-characters** com a tabela de dubladores **disney-voice-actors**, de acordo com o nome do filme.

Como no meu modelo já existe esse relacionamento, só que inativo, vou editar ele. Caso ele não exista, basta criar um novo.

- Aba de Exibição do modelo
- Gerenciar Relações
- Selecionar a relação e clicar em editar (ou clicar em Novo)
- Selecionar **disney-characters.movie_title** e **disney-voice-actors.movie**
- Cardinalidade: **Um para Um (1:1)**
- Direção do filtro cruzado: **Ambas**
- Ativar este relacionamento

&nbsp;

#### disney-director <-> disney_movies_total_gross

Podemos relacionar a tabela de diretores **disney-director** com a tabela de receitas dos filmes **disney_movies_total_gross** de acordo com o nome do filme, criando uma nova relação.

- Aba de Exibição do modelo
- Gerenciar Relações
- Clicar em Novo
- Selecionar **disney-director.name** e **disney_movies_total_gross.movie_title**
- Cardinalidade: **Um para Muitos (1:*)**
- Direção do filtro cruzado: **Único**
- Ativar este relacionamento

&nbsp;

#### disney-director <-> disney-voice-actors

Podemos relacionar a tabela de diretores **disney-director** com a tabela de dubladores **disney-voice-actors**, de acordo com o nome do filme.

No meu caso, já existia essa relação, então vou editar ela

- Aba de Exibição do modelo
- Gerenciar Relações
- Selecionar a relação e clicar em editar
- Selecionar **disney-director.name** e **disney-voice-characters.movie**
- Cardinalidade: **Um para Muitos (1:*)**
- Direção do filtro cruzado: **Único**

Observem que não consigo ativar esse relacionamento. Isso acontece porque já existe uma relação indireta (um caminho) entre os diretores e os dubladores, através da relação 

```
disney-voice-actors <-> disney-characters <-> disney-director
```

Se quisessemos relacionar ativamente diretores e dubladores, teria que inativar a de dubladores com personagens.

E dependendo da análise que fizermos, podemos fazer essa mudança nas relações.

&nbsp;

#### disney_revenue_1991-2016

Depois de rever a modelagem, podemos observar que a tabela de receitas da disney **disney_revenue_1991-2016** ficou sem relações. Como estamos analisando as relações entre os filmes da disney, e essa tabela mistura as outras empresas da disney, ela acaba não sendo útil na nossa análise.

Além disso, ela tem dados muito numéricos, e não categóricos, o que não agrega na nossa análise.

Ou seja, ela ta só fazendo peso no Power BI. Por isso removemos ela.

- Botão direito na tabela
- Excluir do modelo

&nbsp;

## Tratamento dos dados

Se a gente pensar no objetivo desse dataset, receitas dos filmes, podemos querer visualizar duas informações financeiras fundamentais: 

> Quanto a Disney arrecadou com filmes, no total, até hoje?

> Quanto a Disney arrecadou com filmes por ano? E se aplicarmos a correção da inflação?

Para a primeira questão, a visualização de cartão se encaixa muito bem, já que queremos um número único como resultado.

- Adicionar visualização de cartão
- Em **Campos**: disney_movies_total_gross.total_gross

No segundo caso podemos usar um gráfico de colunas agrupadas e linhas, pois além de saber quanto arrecadou por ano temos a possibilidade de ver também os anos que tiveram maior arrecadação, mostrando também o valor corrigido pela inflação.

- Adicionar visualização de colunas agrupadas e linhas
- No **Eixo X**: disney_movies_total_gross.release_date
- No **Eixo Y da coluna**: disney_movies_total_gross.total_gross (soma)
- No **Eixo Y da linha**: disney_movies_total_gross.inflation_adjusted_gross (soma)

Vamos adicionar também um segmentador de dados, para aplicar filtros de data nos nossos gráficos

- Adicionar Segmentação de Dados
- No **Campo**: disney_movies_total_gross.release_date

&nbsp;

Feito isso eu pergunto: funcionou? Conseguimos ver a soma da arrecadação, o valor arrecadado por ano?

Não. Mas por que isso acontece?

Porque a coluna **total_gross** na tabela está como texto, e não como valor numérico. Podemos ver isso pelo cifrão ($) que aparece antes de cada um dos valores do **total_gross** e do **inflation_adjusted_gross**.

A solução para esse caso é tratar os dados para que as colunas deixem de ser uma string e passem a ser valores numéricos.

O Power BI já possui ferramentas para tratamento dos dados. A gente pode fazer isso tanto com DAX quanto com Power Query.

Nesse primeiro momento, vamos fazer o tratamento visualmente com o Power Query.

Então, para acessar essa ferramenta, a gente clica em *Transformar dados**, na parte de cima do Power BI, e ele vai abrir uma janela nova para tratar os dados.

### Transformar Dados

Nessa interface, o Power BI vai exibir uma coluna com **Consultas**, que contém as tabelas do nosso modelo, a parte central com os dados tabulados para melhor visualização, e na direita um coluna com as **Etapas Aplicadas**.

A parte de etapas aplicadas nos dá um passo a passo do que foi feito automaticamente pelo Power BI até agora para tratamento dos dados, e os novos tratamentos que nós fizermos.

Vamos tratar as colunas **total_gross** e **inflation_adjusted_gross** para que elas se transformem em campos numéricos. Observem que no nome da coluna o Power BI já nos dá uma dica que a coluna é de texto, adicionando o "ABC" ao lado do nome.

Na parte central com dados tabulados:
- Clicar com botão direito na coluna **total_gross**
- Clicar em **Substituir valores**
- Em **Valor a ser localizado**, colocamos **$**
- Em **Substituir por** deixamos em branco
- Clicar em **Ok**

Depois repetimos o passo a passo acima para **inflation_adjusted_gross**.

Quando fazemos essa substituição, a coluna de **Etapas Aplicadas** é atualizada com uma nova linha. Essa nova linha possui um nome padrão de acordo com o tipo de ação que fizermos. Podemos renomear esse nome padrão, para lembrar nossas ações depois.

Na coluna **Etapas Aplicadas**:
- Clicar com botão direito em **Valor Substituído**
- Clicar em **Renomear**
- Digitar "Remoção $ total_gross"

Fazemos o mesmo para **inflation_adjusted_gross**.
&nbsp;

**Observação**
> Toda e qualquer substituição de caracteres, para tratamento de dados, pode ser feita dessa forma.

&nbsp;

Agora vamos remover as vírgulas (no meu caso) ou os pontos de separação de milhar.

Na parte central com dados tabulados:
- Clicar com botão direito na coluna **total_gross**
- Clicar em **Substituir valores**
- Em **Valor a ser localizado**, colocamos **,**
- Em **Substituir por** deixamos em branco
- Clicar em **Ok**

Depois repetimos o passo a passo acima para **inflation_adjusted_gross**.

Por fim vamos declarar que aqueles campos são numéricos.

Na parte central com dados tabulados:
- Clicar com botão direito na coluna **total_gross**
- Clicar em **Alterar Tipo**
- Clicar em **Numérico Inteiro**

Poderíamos usar números decimais, porém estamos falando de milhões de dólares. Nesse caso, desprezamos os centavos.

&nbsp;

Como removemos o cifrão, podemos no futuro não lembrar se os valores estão em milhões de reais ou de dólares. Por isso vamos renomear as colunas e adicionar o cifrão ao lado do nome.

- Na parte central com dados tabulados:
- Clicar com botão direito na coluna **total_gross**
- Clicar em **Renomear**
- Adicionar **$** ao final do nome da coluna.

Depois repetimos o passo a passo acima para **inflation_adjusted_gross**.

&nbsp;

É importante salientar que essas etapas que estamos fazendo **NÃO** são aplicadas instantameamente.

O Power BI descreve o passo a passo que vai ser aplicado mas realiza eles somente quando apertarmos no botão **Fechar e Aplicar**. Nesse momento, ele pode fazer otimizações para uma melhor performance, e o resultado final vai ser o que vimos na janela central do Power Query.

&nbsp;

Agora sim conseguimos exibir nossas informações financeiras.

Para exibir os dados da receita corrigida pela inflação, vamos adicionar um cartão para a coluna **inflation_adjusted_gross** e adicionar no Eixo X do gráfico de colunas clusterizadas a coluna **inflation_adjusted_gross**.

&nbsp;


## Dashboard de acompanhamento

### Comparando receitas por gênero

Vocês são os diretores da Disney e são responsáveis por definir quais tipos de filmes devem ser produzidos nos próximos três anos. Um fator relevante para decidir quais filmes serão produzidos de novo é a arrecadação, certo? Ou Alguém discorda disso?

Já que é a arrecadação, vamos criar um dashboard para exibir a média valores arrecadados (ajustados pela inflação) de acordo com o gênero do filme.

Primeiro vamos criar 2 cartões e personalizar eles.

- Criar visualização de cartão
- No **Campo**: Adicionar disney_movies_total_gross.inflation_adjusted_gross
- No **Campo**: Clicar na seta e depois em **Renomear para este visual**
- Digitar o nome do gênero que vamos filtrar. Ex: Ação
- Na coluna de **Filtros**, em **Filtros neste visual**, selecionar o genero de de Ação
- Na coluna de **Visualizações** ir na opção **Formatar este visual** e em **Valor do balão** clicar na função *fx* para editar a cor do valor a ser exibido.
- Definir uma regra para exibir os valores. Ex: Abaixo de 100.000.000 exibir em vermelho, e acima exibir em azul.


Escolher um segundo gênero (ex: Documentário) e realizar os mesmos passos acima.


### Receitas pré e pós Toy Story

Toy story foi um grande marco na história do cinema. Ele foi o primeiro filme da história a ter sido compilado inteiramente por ferramentas de computação gráfica, e também foi o precursor dentre os longas-metragens da Pixar e a primeira produção realizada por meio da parceria entre a própria Pixar e sua distribuidora, a Walt Disney Pictures.

Ele foi lançado em 22/11/1995, arrecadou mais de 406 milhões de dólares no circuito mundial, em comparado com o orçamento de trinta milhões. Ele entrou para a história ao ter sido uma das duas animações a ter entrado na lista dos 100 melhores filmes americanos já realizados, segundo o Instituto Americano do Cinema. Toy Story também recebeu três indicações ao Oscar de 1996 para Melhor Roteiro Original, Melhor Trilha Sonora Original e Melhor Canção Original ("You've Got a Friend in Me"), além de ter ganhado um Oscar de Contribuição Especial. Em 2005, foi introduzido no National Film Registry como sendo "cultural, histórica ou esteticamente significativo" em seu primeiro ano de elegibilidade.

Então, por causa disso tudo que falamos, é interessante comparar a média de receitas dos filmes da disney antes e depois do lançamento de toy story. Pra facilitar essas comparações, vamos criar uma coluna nova no nosso dataset.


#### Criando coluna com Power Query 

- Na parte superior do Power BI, clicar em **Transformar Dados**
- Na parte superior do Power Query, clicar na aba **Adicionar Coluna** e depois em **Coluna Condicional**
- Descrever as condições (data de lançamento maior que 22/11/1995) e clicar em **OK**

&nbsp;

Documentação do Power Query M
- https://learn.microsoft.com/pt-br/powerquery-m/

&nbsp;

#### Criando coluna com expressão DAX 

Esse processo também pode ser feito com expressão DAX, da seguinte forma:

- Na aba dos relatórios, clicar na aba de **Modelagem** e depois em **Nova Coluna**
- Vai habilitar uma linha para digitar a expressão, e iserimos a linha abaixo:

> nome_da_coluna = IF('nome_da_tabela'[nome_do_campo] > DATE(1995, 11, 22), 1, 0)

&nbsp;

Documentação do DAX
- https://learn.microsoft.com/pt-br/dax/


&nbsp;

Então com essa coluna nova, podemos criar novas visualizações e usar essa coluna como filtro, facilitando a análise.

&nbsp;

### Qual foi o filme que mais arrecadou?

&nbsp;

### Qual o gênero que mais fatura?

&nbsp;

### Média dos filmes por classificação etária

&nbsp;

## Atividade prática

Baixar o dataset **audible**, disponível no LMS, e realizar o tratamento dos dados.

Esse dataset traz informações sobre o crescimento dos audiolivros ao longo dos anos, com informações sobre o autor, data de lançamento, narrador, entre outras informações. Ele cobre um período de 1998 até 2025, porque traz lançamentos planejados.

Feito isso, pensar em insights e hipóteses para apresentar para a turma na aula seguinte.

&nbsp;

# Caixinha de sugestões

Tem alguma sugestão para melhorar o andamento das aulas? Por favor preencha o formulário abaixo.

https://forms.office.com/r/44rWB58XPs


Não deixe a sugestão de melhorias para depois! Compartilhe antes, que corrijo o mais rápido possível.

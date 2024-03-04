# Aula 2

## Visualizações

O Power BI trabalha com o que a gente chama de visualizações.

As visualizações são esses botões aqui, e são como se fossem pequenas funções (pensando em programação) que recebem algumas entradas e produzem algumas saídas.

&nbsp;

### Cartão

A visualização mais básica do Power BI é essa aqui, o Cartão.

O cartão exibe um dado único.

- Criar **cartão** com a **soma da idade dos alunos** da turma.

Vocês viram no banco de dados as agregações, sumarizações. O cartão traz os dados agregados, ou seja, posso mudar para trazer a idade média de vocês.

- Mudar cartão para **idade média dos alunos**

Mas quando o cartão é mostrado?

&nbsp;

Geralmente a gente adiciona ele no dashboard quando tem um número muito importante pra ser mostrado, que tem que estar sempre visível.

Isso tem mais a ver com um dashboard de acompanhamento. Por exemplo: número de chamados abertos no SAC. É um número importante pra gente acompanhar, então é legal ter ele no dashboard.

Uma coisa legal nesses dashboards é que o Power BI consegue monitorar alterações na base de dados, e atualiza a visualização também.


- **Manipular base de dados e inserir uma nova linha com idade de 50 anos**
- Depois clicar em **Atualizar**

&nbsp;

E como vocês podem ver, o cartão é atualizado com os novos dados.

&nbsp;

### Colunas empilhadas

Na aula passada a gente construiu um gráfico de barras clusterizado para responder o seguinte insight:

Os mineiros e nordestinos são os mais "fieis" à sua culinaria?

Nós também podemos fazer um gráfico de colunas empilhadas para fazer a mesma análise.

Diferente do cartão, esse gráfico de colunas permite relacionar duas ou mais informações diferentes, dependendo só da análise que queremos fazer.

- Selecionar **gráfico de colunas empilhadas**
    - No **Eixo Y**: Qual região do Brasil...
    - No **Eixo X**: Assinale a alternativa
    - Na **Legenda**: Qual região do Brasil...

&nbsp;

E ele vai segmentar as colunas por região.

Com essa base, conseguimos tentar buscar a relação entre a região e outras informações, como por exemplo o tipo de hobbie

- No **Eixo X**: Assinale o hobbie...

&nbsp;

ou o time que as pessoas torcem

- No **Eixo X**: Escolha o time

&nbsp;

E por ai vai, dependendo das informações que queremos analisar.

&nbsp;

### Hipótese da aula passada

Nessa mesma pegada da visualização de colunas empilhadas, podemos usar um primo das colunas, que é a visualização de barras empilhadas.

Uma das hipóteses que foi enviada na aula passada era:

- Pessoas com menos de 30 anos tendem a gostar de videogame.

Para ver se isso realmente está certo, vamos criar uma nova visualização

- Selecionar **gráfico de barras empilhadas**
- No **Eixo Y**: Assinale o hobbie.....
- No **Eixo X**: contagem de IDs
- Na **Legenda**: Qual sua idade?

&nbsp;

Mas aqui temos um quesito de idade. Queremos saber das pessoas menores de 30 anos.

E ai, o que podemos fazer? Ficar olhando e separando mentalmente quem tem menos de 30 não é uma opção. Então, a gente pode adicionar um filtro na própria visualização e definir um range de idade para filtrar os dados.

- Nos **Filtros neste visual**: menor que 30

Ai a gente consegue ver se de fato pessoas com menos de 30 anos tendem a gostar de videogame.

&nbsp;

### Hipótese da aula passada

Outra hipótese que foi enviada na aula passada era:

- As pessoas mais velhas do curso estão na região sudeste.

A gente pode usar o gráfico de colunas empilhadas, como vimos antes

- Selecionar **gráfico de colunas empilhadas**
- No **Eixo Y**: **Contagem** de qual sua idade
- No **Eixo X**: Qual regiãodo Brasil ...
- Na **Legenda**: Qual sua idade?
E aplicar um filtro de idade

&nbsp;

Ou podemos também usar um gráfico de pizza que, apesar de não ser o mais indicado para essa situação, a gente pode adicionar uma visualização de segmentação de dados e complementar a informação.

- Selecionar **gráfico de Pizza**
- Na **Legenda**: Qual a região do Brasil você está?
- Nos **Valores**: Contagem de IDs

&nbsp;

### Segmentação de dados (Slicer)
A visualização de segmentação de dados é uma ferramenta que permite filtrar e segmentar dados em um relatório de maneira interativa.

Diferente do filtro que vimos antes, que adicionamos direto na visualização (mas pode ser por página ou todas as páginas também) a segmentação de dados normalmente se aplica a todas as visualizações da página, permitindo uma interação mais dinâmica com o dashboard pra ver segmentos específicos de informações.

- Para realizar o filtro de forma mais simples, adicionar **Slicer**.
    - No campo adicionar **Qual sua Idade?**
    - Na aba **Visual** mostrar em **configuração da segmentação** outros estilos para filtragem.

&nbsp;

## Carregar dados do Banco de Dados

Antes usamos um arquivo do excel como fonte de dados, e agora vamos conectar o Power BI no Postgres e puxar a base de dados de lá

- Rodar o script sql que está no LMS para criar a base Northwind
- Conectar no PowerBI através do BD
    - **Servidor**: localhost:5432
    - **Banco de dados**: northwind
    - Selecionar todas as tabelas

&nbsp;

### Comando SQL na importação do Power BI

Quando a gente faz isso, o Power BI já importa todas as tabelas e, mais importante, as relações entre as tabelas.

Então ele já vai saber que elas estão relacionadas entre si.

Mas como eu falei segunda, pra ele fazer isso, o custo é o consumo alto de memória.

Então, um caso recorrente no mercado de trabalho é a gente deixar algumas informações de fora do Power BI e trabalhar somente com o que queremos.

Vamos supor que a gente queria trazer somente os dados desse ano, pois os anos anteriores não fazem sentido na nossa análise.

Vamos voltar na importação do banco de dados
- Conectar no PowerBI através do BD
    - **Servidor**: localhost:5432
    - **Banco de dados**: northwind

E vocês podem ver nessas **opções avançadas** que a gente pode executar uma query **antes** de importar os dados pro Power BI.

- e fazer a query usando o comando
```
SELECT * FROM orders
WHERE order_date >= '2024-01-01'
```

Agora, quando a gente atualizar o Power BI, naquele botão de atualização, ele vai trazer todas as tabelas que já importamos do jeito normal e as tabelas que tiverem o comando SQL aplicado na importação, o comando vai executar **antes** de virem os dados pra cá, trazendo menos informações e deixando o Power BI um pouco mais leve.

Eu não vou incluir nenhum comando SQL aqui, é só pra que vocês tenham em mente que existe essa funcionalidade.

&nbsp;

### Modelagem

Quando importamos, e olhamos a aba de **Modelagem**, podemos ver todas as relações feitas pelo Power BI. Mas por que isso é importante?

Eu quero ver, por exemplo, a quantidade de unidades que tenho no estoque por produto, e pra isso vou criar esse gráfico de rosca aqui:

- Criar gráfico de rosca
- Na **Legenda**: product_name
- Nos **Valores**: units_in_stock

Mas eu quero ver somente de uma cidade. Só que a informação de cidade não ta na tabela de produtos, ta na de supplier.

Como esse dado não é da mesma tabela, a gente deveria imaginar que ia dar algum erro. Mas não.

Se eu adicionar o segmentador de dados, e colocar os dados de cidades pra filtrar, ele consegue separar quantas unidades eu tenho em estoque de acordo com o filtro.

- Segmentador de dados
- No **Campo**: [supplier].city

Mas por que ele sabe fazer isso?

Porque ele já mapeou que a tabela suppliers e a tabela products se relacionam. Então quando eu jogo um filtro em uma, ele já aplica no relacionamento.

&nbsp;

### Criando relacionamentos novos

Caso tenha alguma relação errada ou faltando, a gente pode fazer ela na mão também.

Primeiro vamos excluir a relação entre as tabelas **territories** e **region**

Então, pra gente excluir e depois reconstruir essa relação na mão a gente vai na aba de modelagem, deleta a relação, clica no botão Gerenciar relações e depois em Novo, e depois seleciona as tabelas e os campos e o power BI vai tentar inferir uma relação entre elas.

- Modelagem
- Remover relação
- Gerenciar relações
- Novo
- Seleciona as tabelas e colunas **territories.region_id** primeiro, depois **region.region_id**
- e da um ok.

A opção **ativar relacionamento** faz com que o filtro seja aplicado na relação, Ou seja, se eu selecionar o território em uma visualização que esteja exibindo os dados da região, ele vai aplicar o filtro na visualização. Caso essa opção esteja desmarcada (linha pontilhada) ele ainda exibe a relação, mas não vai aplicar ela na visualização.

Para demonstrar essa opção, vamos desativar a relação entre suppliers e products e fazer o filtro na tela.

A opção de **direção de filtro cruzado** faz com que o filtro seja aplicado de uma tabela para outra ou nos dois sentidos.

&nbsp;

### Modelagem BD <-> Power BI

Se removermos uma coluna de chave estrangeira do banco de dados, ou seja, removermos a relação entre elas no BD e atualizarmos o Power BI, ele vai manter a relação.
Porém, se importarmos o banco de dados novamente, e deixar o Power BI construir as relações do zero, ele não vai mais reconhecer a relação entre as tabelas.

&nbsp;

## Prática em aula

Baixar o dataset 
https://www.kaggle.com/datasets/thedevastator/disney-character-success-a-comprehensive-analysi

que também tem no LMS, se preferirem, 

E explorar um pouco ele.

- Ver se as relações estão adequadas
- Criar visualizações de cartão, segmentador de dados, gráficos de barras e colunas
- fazer um dashboard de acompanhamento periódico (acompanhar vendas, metas, receitas, etc)

&nbsp;

**Um ponto importante**

Vocês tem que olhar os dados mas não seguiar por eles. Na atividade passada, por coincidência ou não, a gente acabou criando hipóteses amarradas nos resultados, e todos deram 100% de acerto. Bem improvável, por isso me deixou com a pulga atrás da orelha.

Nesse caso, deixem a imaginação fluir pra criar as hipóteses.


## Exercício em casa
- https://www.kaggle.com/datasets/arianazmoudeh/airbnbopendata
		Objetivo do exercício: 	
			explorar a base
			tentar tirar insights (levantar hipóteses e validar com os gráficos)
			tentar identificar o que é importante para o Airbnb, para deixar em um dashboard fixo com indicadores e outras coisas


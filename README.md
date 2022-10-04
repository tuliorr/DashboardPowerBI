# DashboardPowerBI


## Introdução


Esse projeto foi desenvolvido como forma de avaliação na disciplina **Dashboard com foco BI** do MBA de Ciência de Dados da Universidade de Fortaleza - UNIFOR


## Objetivo


O objetivo geral desse projeto é conhecer a ferramenta Microsoft Power BI para visualização de dados disponibilizados em planilhas excel, além de desenvolver um dashboard para esses dados


## Parte 1


* Inicialmente, vamos obter os dados através da planilha Excel ```Dados_exercicio_DA100.xlsx```, a qual será utilizada como base para construção dos seguintes gráficos:
	* Gráfico de Área
	* Gráfico de Rosca
	* Gráfico de Barras Clusterizado

* Todas as abas da planilha devem ser carregadas, exceto a "Gerar_Datas"

  1. Clicar na opção ``Obter dados`` no menu superior
  2. Selecionar a opção ``Pasta de Trabalho do Excel`` -> ``Conectar``
  3. Selecionar o arquivo ```Dados_exercicio_DA100.xlsx```
  4. Selecionar todas as tabelas, exceto a ``Gerar_datas``


### 1.1 Gráfico de Área - Valor total de venda por mês


* Entrar na aba ``Modelo`` no menu lateral esquerdo
* Inserir o relacionamento entre as tabelas de [Vendas] e de [Datas] utilizando o campo ``DATA``

NOTA 1: Sempre será necessário inserir o relacionamento entre as tabelas quando for gerar gráficos que utilizem o cruzamento de dados de diferentes tabelas

NOTA 2: Os campos que são utilizados para o relacionamento precisam ser iguais nas duas tabelas.

![1](/images/relacionamento_vendas_datas.png)

* Selecionar o visual ``Gráfico de Área`` e os campos Venda ``VALOR_TOTAL_VENDA`` e Datas ``DATA -> Mês``

![2](/images/grafico1.png) 

* Observação: Você pode customizar o visual do seu gráfico na segunda aba do menu ``Visualizações`` (marcado de azul)


### 1.2 Gráfico de Rosca - Quantidade de Vendas por Categoria de Produto


* Entrar na aba ``Modelo`` no menu lateral esquerdo e inserir o relacionamento entre as tabelas de [Vendas] e de [Produto] utilizando o campo ``CODIGO_PRODUTO`` e ``ID_PRODUTO``

![3](/images/relacionamento_vendas_produto.png)

* Selecionar o visual ``Gráfico de Rosca`` e os campos Produto ``CATEGORIA_PRODUTO`` e Vendas ``ID_PEDIDO``

![4](/images/grafico2.png) 

* Selecionar ``contagem`` como forma de agregação do campo ``ID_PEDIDO``

![5](/images/contagem.png)


### 1.3 Gráfico de Barras Clusterizado


* Entrar na aba ``Modelo`` no menu lateral esquerdo e inserir o relacionamento entre as tabelas de [Vendas] e de [Cliente] utilizando o campo ``CODIGO_CLIENTE`` e ``ID_CLIENTE``

![6](/images/relacionamento_vendas_cliente.png)

* Selecionar o visual ``Gráfico de Barras Clusterizado`` e os campos Cliente ``Nome`` e Vendas ``VALOR_TOTAL_VENDA``

![7](/images/grafico3.1.png) 

* Para inserir o filtro, abra a aba de filtros do visual e faça essas modificações no campo Nome:
    * Tipo de filtro = N superior
    * Mostrar itens = Superior - 5
    * Por valor = ``VALOR_TOTAL_VENDA``
    * Clique em ``Aplicar filtro``

![8](/images/filtros.png)  

* Dessa forma, o gráfico irá exibir os TOP 5 clientes por valor total da venda


### 1.4 Catálogo de Clientes


* Crie uma nova página

* Selecione o visual ``Tabela`` e adicione todos os campos da tabela ``Cliente``

![9](/images/tabela_clientes.png)  

* Adicione um botão para voltar para a página 1: Menu superior -> Inserir -> Botôes -> Voltar

* Clique no ícone do botão e na aba ``Formato`` clique em ``Ação``. O tipo da ação será ``Navegação por página`` e o destino será a ``Página 1``

![10](/images/botao1.png)  

* Precisamos criar um botão na primeira página também para direcionar para a página 2, a qual será o nosso catálogo de clientes

* O processo é praticamente igual ao do primeiro botão, contudo, o segundo botão será do tipo ``Em branco``

* O formato do botão 2 será similiar ao do botão 1 também, porém, o destino agora será a ``Página 2``

* Na guia ``Estilo`` o texto será ``Catálogo de Clientes`` de forma centralizada

![11](/images/botao2.png)


## Parte 2


* Na segunda parte serão desenvolvidos os gráficos de indicador e dispersão para compor o dashboard, além do gráfico Word Cloud para análise dos comentários realizados pelos clientes

* A planilha com os comentários ``Comentarios_pesquisa.xlsx`` deve ser carregada, conforme explicado na parte 1

### 2.1 Word Cloud

* Esse gráfico não está configuração padrão dos visuais, portanto deve ser obtido através do marketplace do Power BI (não tem custo)

* Clique na última opção dos visuais (reticências) na aba ``Visualizações`` e depois em obter mais visuais

![12](/images/obter_visuais.png)   

* Pesquise por Word Cloud e adicione ao seu Power BI. Após a adição, o visual irá aparecer na aba ``Visualizações``

![13](/images/wc.png) 

* Adicione o visual ``WordCloud`` e selecione a tabela ``Comentários``

![14](/images/wordcloud.png)

* Agora precisamos filtrar a palavras irrelevantes dos comentários, essa opção está na seção ``Formatar seu visual`` e precisa estar ativada. Além disso, é preciso determinar quais palavras são irrelevantes, conforme o exemplo em seguida:

**PALAVRAS IRRELEVANTES:** da de do a e o com para é muito são tudo que foi as os na no atendimento Loja produto Empresa em produtos

![15](/images/palavras.png)


### 2.2 Gráfico Indicador


* Para a construção desse gráfico será necessárioa a criação de medidas, as quais representam cálculos realizados entre os dados de diferentes tabelas (ou da mesma)

* As medidas são utilizadas em análises de dados mais comuns, tais como: somas, médias, mínimo, máximo, contagens, etc

* Os resultados dos cálculos das medidas estão sempre se modificando em resposta à sua interação com seus relatórios, permitindo uma exploração de dados ad hoc, rápida e dinâmica

* A boa prática na construção de dashboards orienta criar uma tabela para armanezar todas as medidas criadas, essa tabela pode ser criada por meio do seguinte caminho:
Menu superior -> Guia Modelagem -> Nova Tabela

* O nome dessa tabela geralmente é iniciado por "00" para ela ficar no topo da aba ``Campos``

* Para o nosso gráfico devem ser criadas as seguintes medidas dentro da tabela ``00_Medidas``:
	* Valor_total_Compra = Multiplicação entre tudo o que foi comprado e a quantidade de produtos.
	* Lucro = Subtração do valor total de venda e o Valor total de compra
	* Margem_Lucro = ((Lucro/Valor total Vendido)/Quantidade de Pedidos)/100

* Uma nova medida pode ser criada por meio do seguinte caminho:
Menu superior -> Guia Modelagem -> Nova Medida (observar que a tabela ``00_Medidas`` deve estar selecionada)

* Seguem abaixo as fórmulas que devem ser utilizadas em cada medida:
	* Valor_total_Compra = sumx(Vendas,Vendas[VALOR_UNITARIO_COMPRA])*sumx(Vendas,Vendas[QUANTIDADE])
	* Lucro = sumx(Vendas,[Valor_total_Venda]-[Valor_total_Compra])
	* Margem_Lucro = (sumx(Vendas,[Lucro]/[Valor_total_Venda])/countx(Vendas,Vendas[ID_PEDIDO]))/100

![16](/images/medida.png) 

* Agora com as medidas adicionadas podemos seguir com os gráficos

* Lembrar de alterar o formato da medida ``Margem_lucro`` para porcentagem

![17](/images/margem_lucro.png)  

* Selecione o visual ``Indicador`` e adicione a medida ``Margem_lucro``

![18](/images/indicador.png)   

* Na guia ``Formatar seu visual`` alterar os Eixos do medidor:
	* Máx = 0,1
	* Destino = 0,05

![19](/images/limites_indicador.png)


### 2.3 Gráfico de Dispersão


* Selecione o visual ``Gráfico de Dispersão`` e adicione todos os seguintes campos:
	* Tabela Datas ``DATA -> MÊS`` -> EIXO DE REPRODUÇÃO
	* Tabela Produto ``CATEGORIA_PRODUTO`` -> LEGENDA
	* Tabela Vendas ``ID_PEDIDO`` -> EIXO Y
	* Tabela Vendas ``VALOR_TOTAL_VENDA`` -> EIXO X

* Lembrar de alterar a agregação campo ``ID_PEDIDO`` para CONTAGEM

![20](/images/dispersao.png)

* Para analisar o comportamento através do tempo aperte o botão PLAY no gráfico


## Conclusão


* Por fim, já com todos os gráficos construídos agora podemos organizar o dashboard. Cada gráfico se comporta como uma caixa que pode ter suas dimensões alteradas

* Na guia Exibição no menu superior é possível fazer a alteração dos estilos, cores e outras formatações

* A boa prática na construção de dashboards orienta a deixar um espaço entre os gráficos para não ficarem colados um no outro e para a visualização ficar melhor

* O resultado final do dashboard ficará parecido com as imagens abaixo:

![21](/images/dashboard.png)

![22](/images/catalogo.png)

* Lembrando que existe o botão para acessar a página de catálogo de clientes, bem como o botão para retornar ao dashboard

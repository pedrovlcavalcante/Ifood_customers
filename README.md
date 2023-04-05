# Projeto de classificação

## Problema de Negócio
Desenvolver um modelo preditivo que irá auxiliar o time de marketing a selecionar melhor os clientes alvo da próxima campanha, maximizando o lucro.

## Etapas
1. Importação de bibliotecas iniciais
2. Importação do dataset, limpeza de dados e criação de features
3. Análise exploratória de dados
4. Proposta de segmentação
5. Importação de bibliotecas para preparação dos modelos de classificação
6. Modelagem e avaliação de métricas
7. Avaliação do retorno financeiro dos modelos.

## Objetivos
1. Propor uma segmentação de perfil baseado no comportamento dos consumidores
2. Criar um modelo preditivo visando maximizar os lucros das próximas campanhas de marketing.

## Os dados
O dataset é constituído por 29 colunas representando uma característica dos clientes e 2240 linhas, cada uma representando um cliente.

As informações tratam de:
-  Grau de Instrução
-  Ano de nascimento
-  Estado civil
-  Renda
-  Número de filhos crianças
-  Número de filhos adolescentes
-  Data em que se tornou cliente
-  Recência
-  Montante consumido em vinhos
-  Montante consumido em carnes
-  Montante consumido em frutas
-  Montante consumido em peixes
-  Montante consumido em doces
-  Montante consumido em produtos "Gold"
-  Número de compras feitas com desconto
-  Número de compras feitas usando o catálogo
-  Número de compras feitas diretamente na loja
-  Número de compras feitas no website
-  Se o cliente fez alguma reclamação nos últimos 2 anos
-  Se o cliente aceitou alguma das campanhas anteriores (1 coluna para cada campanha)
-  Variável resposta (última campanha)

## Procedimentos de limpeza dos dados e criação de features
Os dados não aprensentaram grandes problemas, a única coluna apresentando inconsistências foi `Income` (Renda), com alguns dados faltantes.
O procedimento realizado para sanar esse problema foi substituir os dados faltantes pela média de renda de acordo com o grau de instrução do cliente.
Por exemplo, se o dado faltante for de um cliente com grau de instrução de graduação, esse dado será preenchido pela renda média dos clientes com esse mesmo grau de instrução. Isso se deve ao fato de que foi observado no dataset que a renda média aumenta com graus de instrução maiores.

Foram criadas features para auxiliar na modelagem, são elas:
-  TotalCmp: O total de campanhas aceitas dentre as 5 anteriores
-  CustomerDays: O número de dias passados desde a data que o cliente se inscreveu na companhia
-  Age: Idade do cliente, derivado da coluna Year_Birth
-  Children: Soma dos filhos crianças e adolescentes de cada cliente

Foram identificados outliers em `Income` e `Age` pelos limites superiores dos boxplots de cada uma das features. Os outliers foram removidos.

## Insights da análise exploratória
-  Idade: Em sua maioria, os clientes tem entre 30 e 60 anos de idade
-  Educação: Em sua maioria, possuem nível superior
-  Estado Civil: Em sua maioria, os clientes são casados ou vivem juntos com algum companheiro
-  Renda: Poucos clientes possuem renda acima de $100.000,00 anual

Observou-se uma correlação positiva entre a renda dos clientes e os valores consumidos por eles, principalmente em vinhos e carnes, que foram também os produtos identificados como os mais consumidos pelos clientes.

É importante frisar que os valores apresentados no consumo desses produtos dizem respeito à quantia total gasta pelo cliente nos últimos 2 anos.

Foi também indentificado que o perfil de renda dos clientes que aceitaram as ofertas das campanhas é consideravelmente maior que o dos que não aceitaram.

Quanto às variáveis de idade, grau de instrução, estado civil, idade e número de filhos, o pefil dos aceitantes foi semelhante ao dos que recusaram, em outras palavras, mesmo no grupo de pessoas que aceitaram as campanhas (que giram em torno de 7% da amostra para cada campanha), o perfil seguiu o da amostra. Em resumo, a única discrepância significativa encontrada foi na renda.

Foi também identificado que os clientes que aceitaram a campanha alvo do estudo também aceitaram bem as outras campanhas, com exceção da 2.

## Segmentação
Foi proposta a seguinte segmentação:
-  Clientes com grau superior de instrução, casados ou juntos, com um filho, tem preferencia por vinhos

## Classificadores
Foram escolhidos 3 modelos de classificação bastante conhecidos:
-  Regressão Logística
-  KNN
-  Decision Tree

## Métricas
As métricas escolhidas foram:
-  Acuracy
-  Precision
-  Recall
-  Score F1
-  Curva ROC

## Preparação dos dados e modelagem
Para que os modelos pudessem ser treinados de forma adequada, foi necessário aplicar algumas tranformações nos dados.

Os dados categóricos como grau de instrução e estado civil por exemplo, foram transformados em categorias numéricas de acordo com os valores encontrados na coluna, por meio do método `One-Hot`.

Já os dados numéricos como renda e idade por exemlo, foram padronizados de forma que a média torna-se 0 e a variância torna-se 1, reduzindo o impacto que valores originais muito altos como os de renda teriam frente ao impacto que valores menores como idade tem.

O treino dos modelos foi realizado após a separação dos dados em grupos de treino, utilizados para ensinar o modelo, e de teste, utilizado para validar o modelo.
Todo esse processo foi realizado com o auxílio do `Pipeline` do Scikit Learn.

## Métricas
Para verificar as quantidades de erros e acertos dos modelos nos dados de treinamento e de teste, foram criadas matrizes de confusão, que mostram as quantidades de vezes em que o modelo previu corretamente o valor de aceitantes da oferta (1) e de não aceitantes (0), bem como todas a vezes em que as previsões foram erradas, ou seja, onde se previu 1 onde na realidade foi 0 e vice-versa.

Cada métrica foi calculada tanto para os dados de treino quanto para o de teste para avaliar a possibiliade de overfitting, em outras palavras, a capacidade do modelo em acertar previsões em dados desconhecidos, se as métricas divergirem muito entre esses grupos de dados, por exemplo, performar muito bem nos dados de treino e muito mal nos dados de teste, há grande possibilidade de haver overfitting no modelo e medidas precisam ser aplicadas para reverter essa situação.

Para os dados de treino, as métricas foram:

-  Logistic Regression <br/>
  Accuracy:  0.9012899607403253 <br/>
  Precision:  0.7604790419161677 <br/>
  Recall:  0.4828897338403042 <br/>
  F1 Score:  0.5906976744186048 <br/>
  
-  KNN <br/>
  Accuracy:  0.9052159282108806 <br/>
  Precision:  0.7865853658536586 <br/>
  Recall:  0.49049429657794674 <br/>
  F1 Score:  0.6042154566744731 <br/>
  
-  Decision Tree <br/>
  Accuracy:  0.9921480650588895 <br/>
  Precision:  1.0 <br/>
  Recall:  0.9467680608365019 <br/>
  F1 Score:  0.97265625 <br/>
  
Para os dados de teste, as métricas foram:
  
-  Logistic Regression <br/>
Accuracy:  0.8856502242152466 <br/>
Precision:  0.6785714285714286 <br/>
Recall:  0.5352112676056338 <br/>
F1 Score:  0.5984251968503937 <br/>

-  KNN <br/>
Accuracy:  0.8430493273542601 <br/>
Precision:  0.5098039215686274 <br/>
Recall:  0.36619718309859156 <br/>
F1 Score:  0.42622950819672134 <br/>

-  Decision Tree <br/>
Accuracy:  0.8587443946188341 <br/>
Precision:  0.5526315789473685 <br/>
Recall:  0.5915492957746479 <br/>
F1 Score:  0.5714285714285715 <br/>

Podemos notar que o modelo de regressão logística manteve uma performance semelhante nos dados de teste e de treino, apesar da precisão ter variado mais. É importante destacar que os modelos foram treinados com as configurações padrão em que são importados do Scikit Learn.

## Retorno financeiro
Os calculos do retorno financeiro do modelo foi realizado utilizando as informações do desafio, um pdf que se encontra nesse repositório, onde o custo de contato com o cliente foi calculado em 3 unidades monetárias ($3) e a receita gerada caso o cliente aceitasse a oferta foi de 11 unidades monetárias ($11).

Com isso, utilizando dos valores encontrados nas matrizes de confusão de cada modelo, realizamos o seguinte cálculo, com as seguintes nomenclaturas:
-  acertos dos aceitantes (tp)
-  erro dos aceitantes (fp)

Cálculo:

(tp * 11) - (tp * 3) - (fp * 3) = lucro ou prejuízo

(Quantidade de acertos x receita gerada) menos (quantidade de acertos x custo) menos (quantidade de erros vezes custo) = lucro ou prejuízo

Retorno positivo Logistic Regression <br/>
$250 <br/>
Retorno financeiro possível <br/>
$568 <br/>
Taxa de retorno: 44.01% <br/>

Retorno positivo KNN <br/>
$133 <br/>
Retorno financeiro possível <br/>
$568 <br/>
Taxa de retorno: 23.42% <br/>

Retorno positivo Decision Tree <br/>
$234 <br/>
Retorno financeiro possível <br/>
$568 <br/>
Taxa de retorno: 41.20% <br/>

O retorno finaceiro possível é o valor que poderia ser gerado caso os modelos acertassem todas as previsões nos dados de teste, onde havia 71 usuários que aceitaram a oferta, o que geraria um retorno de $568, a partir disso, calculamos a porcentagem do total que o modelo nos trouxe, onde, mais uma vez, a regressão logística obteve um aproveitamento maior que o dos outros modelos, com 44.01%.

## Conclusão
O modelo escolhido até o momento para solucionar o problema de nogócio foi a `Regressão Logística`, que apresentou bons resultados em suas configurações padrão, porém ainda há possibilidades de melhorar esses resultados aplicando algumas medidas como:

-  Aplicar transformações nos dados
-  Redução de dimensionalidade (retirar features que não influenciam no treino do modelo)
-  Diferentes thresholds (Regressão Logística)
-  Diferentes números de vizinhos (KNN)
-  Diferentes números de nós (Decision Tree)
-  Treinamento em dados balanceados (há muito mais clientes que recusaram que clientes que aceitaram, o que compromete o desempenho do modelo)
-  Cross Validation (validar os modelos em diferentes dados de treino e de teste)

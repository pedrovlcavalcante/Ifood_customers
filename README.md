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

## Procedimentos de limpeza dos dados
Os dados não aprensentaram grandes problemas, a única coluna apresentando inconsistências foi `Income` (Renda), com alguns dados faltantes.
O procedimento realizado para sanar esse problema foi substituir os dados faltantes pela média de renda de acordo com o grau de instrução do cliente.
Por exemplo, se o dado faltante for de um cliente com grau de instrução de graduação, esse dado será preenchido pela renda média dos clientes com esse mesmo grau de instrução. Isso se deve ao fato de que foi observado no dataset que a renda média aumenta com graus de instrução maiores.

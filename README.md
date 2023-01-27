# tcc-bi

<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->
# Título do Trabalho

#### Aluno: [André de Oliveira Salles](https://github.com/link_do_github)
#### Orientador: [Felipe Borges](https://github.com/FelipeBorgesC).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código](https://github.com/link_do_repositorio). <!-- caso não aplicável, remover esta linha -->

---

### Resumo

<!-- trocar o texto abaixo pelo resumo do trabalho, em português -->

O projeto teve como objetivo utilizar uma rede neural para prever o valor futuro da produção de biodiesel a partir dos dados de produção de anos anteriores para cada região do Brasil. 
Os dados foram obtidos na plataforma de dados abertos do governo federal (link). 
O modelo foi gerado a partir de uma combinação de uma camada de rede lstm e de outra camada de rede bidirecional.
O resultado foi capaz de captar a tendência das séries de cada região, porém as nuâncias da rede não foram determinadas.

### 1. Introdução

Comentário sobre produção de biodiesel: Os dados de produção de biodiesel têm como fonte a página de dados abertos do governo federal do Brasil. Os dados são mensais do período de 2005 até 2020 e podem ser classificados de acordo com a região do Brasil. 

Explicação sobre rede neurais (lstm e bidirecional): Para realizar a predição de um valor futuro da série temporal, foram utilizadas redes neurais para cada região do Brasil. Devido a sua capacidade de lembrar dos parâmetros de entrada seguindo uma sequência de dados, o tipo de rede utilizada foi a LSTM desenvolvida para o Tensorflow. Além disso, com o objetivo de tentar melhorar o treinamento da rede, uma rede bidirecional, também desenvolvida para o Tensorflow foi utilizada.

COmentário sobre o Colab: O projeto foi totalmente desenvolvido no ambiente em cloud da Google, o Google Colab, devido a praticidade para fazer o upload dos dados históricos da produção de biodiesel e para instalar as bibliotecas necessárias. Todas esão listadas abaixo:

- numpy as np
- matplotlib.pyplot as plt
- pandas as pd
- os
- datetime import datetime
- keras.models import Sequential
- keras.layers import LSTM
- keras.layers import Dense
- keras.layers import Bidirectional
- keras.layers import Dropout
- datetime import datetime
- sklearn.preprocessing import MinMaxScaler
- sklearn.model_selection import train_test_split
- tensorflow.python.keras.preprocessing.sequence import TimeseriesGenerator
- keras.callbacks import EarlyStopping, ReduceLROnPlateau, ModelCheckpoint
- math
- sklearn.metrics import mean_squared_error
- tensorflow import keras


### 2. Modelagem

O primeiro passo do trabalho consistiu em fazer o upload do arquivo '.csv' para a pasta de armazenamento do Google Colar. Uma vez com os dados da produção de biodiesel no ambiente, o comando 'read_me' da biblioteca pandas foi utilizado para importar os dados para um dataframe. Uma avaliação inicial indicou que não havia dados nulos ou em formatos incorretos na planilha original, logo, não foi necessário fazer um tratamento na qualidade dos dados.

Antes de treinar o modelo, foram necessárias diversas etapas para prepará-los. A primeira foi uma manipulação do dataframe para armazenar os dados agregados e categorizados por ano, mês e região do Brasil. 

Em seguida, houve uma manipulação do formato das datas para que eles ficassem igualmente distribuídos ao longo do período com dados válidos. Neste momento, também foi possível plotar os gráficos para cada região utilizando a biblioteca matplotlib.

Na etapa de preparação para o treinamento, os dados foram separados em treino e teste, foi utilizada a função 'train_test_split' da biblioteca Sklearn. Após algumas heurísticas para determinar a melhor proporção entre os dois grupos, foi definido que dois terços dos dados seriam utilizados para treino e o outro um terço para validação. Além disso, como a ordenação dos dados é importante para séries temporais, o parâmetro shuffle foi configurado como falso para não alterar a ordem do datafram original.

Ainda na etapa de preparação para o treinamento, foi utilizada a função 'fit_transform' da biblioteca MinMaxScaler do Scikit Learn para normalizar os dados entre 0 e 1.

Como último passo na etapa de preparação, foi utilizada a função TimeseriesGenerator para determinar o formato de entrada dos dados no modelo de redes neurais e os valores que a rede deve tentar prever. Testes indicaram uma janela de entrada de 4 valores sequenciais de produção de biodiesel.

Uma vez que os dados estavam prontos para o treinamento, restou apenas configurar as redes neurais para cada região. As redes foram configuradas em três camadas LSTM Bidirecional e uma de saída:

- LSTM Bidirecional com um dropout de 0.1 com tamanho 100.
- LSTM Bidirecional com um dropout de 0.1 com tamanho 80.
- LSTM Bidirecional com um dropout de 0.1 com tamanho 50.
- Saída (Dense) de tamanho 1.

Para compilar a rede, utilizou-se o otimizador SGD (Gradiente Otimizador Estocástico) e, além disso, o método do erro médio quadrático para o cálculo do erro geral de previsão da rede.

O treinamento foi configurado para 100 épocas, um batch size igual a 8, um percentual de validação de 20% e, por fim, um early stopping com paciência de 100.


### 3. Resultados

Os resultados variaram muito para cada região. Embora o RMSE de todos tenha ficado entre 0.05 e 0.2, valores considerados baixos, foi possível observar, de maneira gráfica, que os resultados poderiam ser melhores. De maneira resumida, o modelo foi capaz de prever bem a tendência das séries temporais. Entretanto, as oscilações previstas pelo modelo são muito maiores do que a dos dados fornecidos. 

### 4. Conclusões

Embora o modelo seja capaz de detectar a tendência das curvas de cada região, apenas a própria série temporal para prever o seu comportamento futuro não foi suficiente para fazer a previsão. Uma análise com mais variáveis é recomendado tentar obter resultados melhores.

---

Matrícula: 191.671.006

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*



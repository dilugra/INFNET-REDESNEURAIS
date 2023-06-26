# COMPREENSÃO DO NEGÓCIO

Visando criar um modelo que pudesse classificar pacientes diabéticos e não diabéticos de uma base de pacientes, assim poderemos prever e iniciar medidas prévias antes que esses pacientes possam desenvolver efetivamente a doença ou mesmo inciar um tratamento , mesmo com a doença em fase assintomática.
Para isso selecionamos uma base de dados do Kaggle.
Para os dados pré-processados da etapa anterior você irá:

# COMPREENSÃO DOS DADOS
gender = Gênero, variável categórica , foi transformada com o onehotencoder em binário. para poder distribuir seu peso de forma mais eficiênte.
age = idade , variável contínua. realizado um standart scaler.
hypertension = Se o paciente é hipertenso ou não, variável categórica , foi transformada com o onehotencoder em binário. para poder distribuir seu peso de forma mais eficiênte.
heart_disease = Se o paciente tem doença cardiaca ou não, variável categórica , foi transformada com o onehotencoder em binário. para poder distribuir seu peso de forma mais eficiênte.
smoking_history = Se o paciente fuma ou não , variável categórica,  foi feito um reshape pois assim as categorias puderam ser distribuidas dentro dos pesos atribuidos.
bmi = Indice de massa corpotal ( IMC ) , variável contínua.  realizado um standart scaler.
HbA1c_level = nivel de hemoglobina no sangue , variável contínua. realizado um standart scaler.
blood_glucose_level = nível de glucose no sangue, variável contínua. realizado um standart scaler.
diabetes = target.

# PREPARAÇÃO DOS DADOS

Foram realizadas as transformações nas variáveis categóricas para que fique entre -1 a 1 e 0 a 1 ( para as que eram sim ou não).
Variáveis contínuas receberam um standartscaler.
Como foi visto na matriz de correlação , os dados eram bem descorrelacionados, logo não vi necessidade de aplicar uma PCA.

# MODELAGEM

Quantas camadas?
Faremos com 3 camadas, 1 de entrada, uma intermediária e uma de saída.
Quantos neurônios na camada de entrada?
A camada de entrada receberá 8 neurônios de acordo com o número de features da tabela.
Quantos neurônios na camada de saída? Justifique.
A camada de saída receberá 2 neurônios, pois estou querendo saber sim ou não para diabetes, e usarei a função loss de categorical_crossentropy.
Quantos números de neurônios na camada intermediária? Como esse número foi escolhido?
A camada intermediária receberá 8 neurônios, pois quero que todo o mapeamento das possibilidades seja feito. Em leituras de Pappers eram constantemente citadas como uma forma de escolha da quantidade de neuronios
da camada intermediária ( para um classificador binomial) um número que fosse intermediário a camada de entrada e saída. assim correria menor risco de overfit.
Qual será o algoritmo utilizado no treinamento?
No treinamento utilizaremos o keras , com uma validação cruzada feito pelo sklearn , usando o StratifiedKFold , com o parametro stratify  = o target e o shuffle = True, para garantir que teremos presença de todas as classes no treino.
Qual a função de ativação será utilizada em cada camada? Justifique.
camada intermediária = Relu , O uso da Relu foi feito , pois ela consegue resolver bem essa classificação sem sobrepeso computacional. 
camada de saída = softmax, o Uso da Softmax foi feito, pois a saída da softmax é um intervalo de 0 a 1 logo em 2 classes ela conseguirá me retornar 0 ou 1.
Qual a função de otimização será utilizada neste treinamento?
Usarei a função cathegorical crossentropy, pois me da uma boa saída para 2 ou mais classes, nosso caso são 2.
Quais serão as figuras de mérito que serão usadas na avaliação do modelo. Justifique.
recall, pois quero maximizar o número de doentes tratados , mesmo que os não doentes fiquem sobre uma avaliação. 


# AVALIAÇÃO DO MODELO

temos um problerma onde nossa base é relacionada a doença, logo acurácia não deve ser o medidor principal. Temos que analisar a sencibilidade e a especificidade do modelo, visto isso o ajuste do trheshold para 0,1 ,
assim pegando basicamente todos os doentes em detrimento de alguns não doentes. O modelo conseguiu classificar bem , porém temos 2 variáveis que são muito importantes para o modelo, indice de glucose e hemoglobina.
Com essas 2 variáveis sendo o peso maior de todo o sistema o que poderia causar algum tipo de viés do modelo, talvês se tivessemos mais variáveis que fossem relevantes a ponto de dividir um pouco o protagonismo,
teríamos como separar os casos onde temos pacientes doentes e não doentes com as mesmas indicações.


# Trabalho-MVP-ML-PUC
MVP de Machine Learning – Previsão de NPS em C+6
Contexto

Este projeto faz parte da disciplina de Machine Learning da PUC, mas foi inspirado em um desafio que vivencio na prática. Trabalho como Coordenador de Experiência do Cliente (CX) e CRM em uma construtora, e um dos maiores pontos de atenção na área é identificar clientes que podem ficar insatisfeitos antes da pesquisa final de NPS, que acontece seis meses após a entrega das chaves.

A ideia aqui foi trazer esse problema real para dentro do curso e construir um MVP preditivo, testando diferentes modelos de aprendizado de máquina para verificar se conseguimos antecipar a percepção do cliente e atuar de forma preventiva.

Objetivo

O objetivo é prever se um cliente será:

Detrator (nota 0–6),

Neutro (nota 7–8) ou

Promotor (nota 9–10)

na pesquisa de NPS C+6.

As variáveis consideradas incluem:

Nota dada no NPS da vistoria

Perfil socioeconômico: renda, idade, filhos, estado civil, escolaridade

Dados operacionais: meses para entrega, status e acionamentos da assistência técnica

Região e safra de obras

Etapas do Trabalho

Carga e preparação dos dados

Leitura da base em CSV

Criação da variável alvo nps_6m_target

Ajuste de tipos e tratamento de valores ausentes

Exploração e pré-processamento

Análise da distribuição das classes (Detratores 48%, Promotores 32%, Neutros 20%)

Tratamento de missing values (mediana/moda)

Padronização e codificação via pipeline

Divisão treino/teste estratificada

Modelagem

Baseline: Dummy Classifier

Modelos lineares e probabilísticos (Regressão Logística, Naive Bayes)

Árvores e ensembles (Decision Tree, Random Forest, Bagging, Extra Trees, Voting)

Boosting (AdaBoost, Gradient Boosting, XGBoost)

Avaliação

Validação cruzada estratificada (k=5)

Métricas: accuracy, f1-macro, precision, recall

Comparação e ranking de modelos

Otimização de hiperparâmetros

GridSearchCV no AdaBoost

Melhor configuração: n_estimators=100, learning_rate=0.5, max_depth=3

f1-macro em CV: ~0,49

Aplicação prática

Simulação de clientes fictícios

Previsão da classe (Detrator, Neutro ou Promotor)

Discussão sobre uso real no negócio

Resultados
Modelo	Accuracy	f1-macro	Observações
Dummy (Baseline)	0,48	0,21	Sempre prevê Detrator
Logistic Regression	0,56	0,43	Melhor que baseline, mas fraco em Neutros
Random Forest	0,54	0,43	Estável, mas sem destaque
Gradient Boosting	0,57	~0,45	Bom equilíbrio
AdaBoost (default)	0,58	~0,46	Melhor desempenho geral
AdaBoost (tuning)	0,53	0,45	Refinou Detratores e Promotores, mas Neutros seguem críticos

📌 Insight: os algoritmos de boosting foram os que mais se destacaram, mas a classe Neutro continua sendo difícil de prever devido ao desbalanceamento.

Próximos Passos

Testar técnicas de balanceamento (SMOTE, class_weight)

Explorar variantes modernas como LightGBM e CatBoost

Analisar importância das variáveis para entender os fatores que mais pesam no NPS

Integrar o modelo em um painel de CX para apoiar ações preventivas

Como Executar
Clonar o repositório
git clone https://github.com/frasilva82/Trabalho-MVP-ML-PUC.git
cd Trabalho-MVP-ML-PUC

Rodar no Google Colab

Abra o notebook diretamente pelo link:
👉 Abrir no Colab

Rodar localmente

Instale as dependências principais:

pip install pandas numpy scikit-learn xgboost matplotlib


Depois, abra o notebook MVP_NPS.ipynb no Jupyter Notebook ou VSCode.

Autor

Francisco Almeida da Silva
Coordenador de Experiência do Cliente (CX) e CRM – Construtora Tenda

Projeto desenvolvido no curso de Machine Learning da PUC, inspirado em desafios reais de gestão de NPS.

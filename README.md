## MVP de Machine Learning – Previsão de NPS em C+6

Contexto

Esse projeto nasceu dentro da disciplina de Machine Learning da PUC, mas foi inspirado em um desafio que eu enfrento no dia a dia como Coordenador de Experiência do Cliente (CX) em uma construtora.

O problema é que a pesquisa de NPS seis meses após a entrega das chaves (C+6) muitas vezes chega tarde: quando o cliente já está insatisfeito, sobra pouco espaço para ação. A proposta aqui foi criar um MVP preditivo que consiga antecipar quem tem mais chance de ser Detrator, Neutro ou Promotor, para que a equipe de CX possa agir antes da pesquisa final.

Objetivo

Treinar modelos de classificação para prever o NPS C+6 com base em variáveis já conhecidas durante a jornada do cliente:

Nota no NPS da vistoria

Perfil socioeconômico (idade, filhos, renda, escolaridade, estado civil)

Dados operacionais (meses para entrega, acionamentos da assistência técnica, status do chamado)

Região e safra de obras

Com isso, a área de CX pode antecipar riscos, priorizar clientes críticos e potencializar ações de fidelização.

O que foi feito

Preparação da base (tratamento de nulos, criação do target nps_6m_target).

Análise inicial (48% Detratores, 32% Promotores, 20% Neutros).

Pipelines de pré-processamento (padronização + one-hot).

Teste de diferentes modelos:

Baseline: Dummy Classifier

Modelos simples: Regressão Logística, SVM, KNN, Naive Bayes, Árvore

Ensembles: Random Forest, Bagging, Extra Trees, Voting

Boosting: AdaBoost, Gradient Boosting, XGBoost

Validação cruzada e comparação de métricas.

Tuning no AdaBoost com GridSearchCV.

Simulação prática com clientes fictícios.

Resultados

Baseline (Dummy): 48% (só prevê Detrator).

Modelos lineares: 53–56%.

Random Forest / Ensembles: ~54%.

Boosting: AdaBoost (58%) e Gradient Boosting (57%) tiveram o melhor desempenho.

AdaBoost otimizado: ~53% no teste, com maior equilíbrio entre Detrator e Promotor.

📌 Ponto crítico: o modelo ainda tem dificuldade em classificar os Neutros (20% da base).

Se um Neutro é previsto como Detrator, podemos agir antes para evitar uma resposta negativa.

Se um Neutro é previsto como Promotor, podemos ativar campanhas de indicação (MGM) e fidelização.

Ou seja, mesmo errando nos Neutros, o modelo já gera valor prático: permite decidir estratégias de retenção e engajamento com antecedência.

Exemplo prático
Cliente	NPS Vistoria	Renda	Acionamentos	Previsão C+6
SP (40 anos, baixa renda, 3 acionamentos)	Detrator	FAIXA 1	3	Detrator
BA (32 anos, renda média, sem acionamentos)	Neutro	FAIXA 2	0	Detrator
CE (27 anos, renda alta, 5 acionamentos)	Promotor	FAIXA 3	5	Promotor

O modelo já consegue:
✅ Identificar bem Detratores e Promotores
⚠️ Nos Neutros, traz alertas úteis que podem direcionar a atuação da equipe de CX

Antecipar clientes insatisfeitos (Detratores)

O modelo consegue identificar clientes com alto risco de se tornarem Detratores no C+6.

Isso permite acionar equipes de relacionamento, assistência técnica e renegociação antes da pesquisa final.

Na prática, significa reduzir surpresas negativas e evitar quedas no NPS que só apareceriam no fim da jornada.

Aproveitar Promotores

Os clientes que o modelo indica como Promotores podem ser rapidamente direcionados para programas de indicação (MGM), campanhas de fidelização e geração de leads.

Com isso, a empresa consegue transformar satisfação em resultado de negócio (mais vendas, menor CAC) ainda durante a jornada.

Trabalhar os Neutros de forma proativa

Apesar de ser a classe mais difícil, justamente aí está o maior potencial: um Neutro pode migrar para Detrator (impacto negativo no NPS) ou ser convertido em Promotor (impacto positivo direto).

O modelo funciona como um radar de atenção, permitindo criar planos específicos de encantamento, acompanhamento e reforço da percepção de valor.

Ou seja, cada Neutro bem trabalhado significa pontos a mais no NPS consolidado.
Próximos passos

Balanceamento de classes (SMOTE, class_weight).

Testar LightGBM e CatBoost.

Explorar feature importance para entender fatores-chave.

Avaliar uso em painel de CX em tempo real.

Como rodar
git clone https://github.com/frasilva82/Trabalho-MVP-ML-PUC.git
cd Trabalho-MVP-ML-PUC


👉 Abrir direto no Colab

Dependências principais:

pip install pandas numpy scikit-learn xgboost matplotlib

Autor

Francisco Almeida da Silva
Coordenador de Experiência do Cliente (CX) e CRM – Construtora Tenda

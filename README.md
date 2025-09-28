##MVP – Predição de NPS no Pós-Ocupação

Contexto

Este projeto foi desenvolvido como parte do MVP da disciplina de Machine Learning da PUC no cusrso de especialização em ciência de dados e analytics.
O desafio trazido é real e busca identificar, de forma antecipada, clientes com potencial de insatisfação no período de pós ocupação de seu apartamento.

Hoje, a pesquisa NPS (Net Promoter Score) é aplicada 6 meses após a entrega das chaves. O objetivo do projeto foi treinar um modelo capaz de prever esse resultado futuro (NPS Chaves+6 ou C+6) com base em dados coletados no momento da vistoria e em atributos do cliente.

O Net Promoter Score (NPS) é uma métrica de lealdade e satisfação de clientes criada por Fred Reichheld (2003). É amplamente utilizada em diversos setores, inclusive no mercado imobiliário, para medir a experiência do cliente após interações importantes, como a entrega do imóvel.

O cálculo parte de uma única pergunta:
“Em uma escala de 0 a 10, qual a probabilidade de você recomendar a empresa/produto/serviço a um amigo ou colega?”

0 a 6: Detratores (clientes insatisfeitos, risco de churn e críticas negativas).

7 e 8: Neutros (clientes indiferentes, pouco engajados).

9 e 10: Promotores (clientes engajados, com alto potencial de recomendação).


Objetivo

Construir um modelo de Machine Learning supervisionado que classifique clientes como:

Detrator (avaliações NPS entre 0 a 6)

Neutro (avaliações NPS entre 7 e 8)

Promotor (avaliações NPS entre 9 e 10)

A ideia é que esse modelo seja usado de forma prática pela área de CX para atuar antes da pesquisa final — prevenindo riscos, engajando clientes e aumentando o impacto positivo no NPS.


Base de Dados

Registros: 2.539 clientes.

Variáveis:

Numéricas: idade, filhos, sexo, meses_para_entrega, acionamentos_assistencia.

Categóricas: regional, safra_inicio_obras, nps_vistoria, faixa_renda, estado_civil, escolaridade, status_assistencia.

Variável alvo: NPS 6 meses após as chaves, transformado em três classes (Detrator=0, Neutro=1, Promotor=2).

Desbalanceamento: 48% Detratores, 32% Promotores e 20% Neutros.


Metodologia

Exploração da base: análise de distribuições, categorias e valores ausentes (~0,5%).

Pré-processamento: imputação de faltantes (mediana/moda), padronização numérica e one-hot encoding para variáveis categóricas.

Divisão treino/teste: 80/20, preservando proporção das classes (stratify).

Baseline: DummyClassifier (acurácia ~48%, equivalente à classe majoritária Detrator).

Modelagem inicial: Regressão Logística e Random Forest.

Comparação ampliada: KNN, SVM, Naive Bayes, Decision Tree, Bagging, Extra Trees, Voting, Gradient Boosting e AdaBoost, todos com validação cruzada (k=5).

Otimização: tuning de hiperparâmetros no AdaBoost (n_estimators, learning_rate, max_depth).


Resultados

Modelos lineares (Regressão Logística): superaram o baseline, mas com baixa sensibilidade para a classe Neutro.

Random Forest: maior robustez, mas ainda limitada nos Neutros.

Boosting (AdaBoost e Gradient Boosting): melhores desempenhos médios em validação cruzada.



Modelo final escolhido:

AdaBoost

Acurácia média (CV): ~58%

f1_macro: ~0,46



Aplicabilidade prática em CX

O modelo já pode ser usado como piloto, mesmo com limitações nos clientes Neutros. Ele apoia decisões estratégicas da área de Experiência do Cliente:

Detratores: antecipar riscos de insatisfação e agir antes do NPS final.

Promotores: engajar clientes e fortalecer programas de indicação e fidelização.

Neutros: trabalhar de forma proativa, aumentando as chances de reversão positiva e impacto direto no NPS.



Conclusão

Este MVP conecta teoria e prática: mostra como o uso de Machine Learning pode fortalecer a gestão da experiência do cliente no setor da construção civil.

Mesmo sendo uma primeira versão, o modelo já apoia decisões reais da operação de CX, oferecendo valor imediato e abrindo espaço para evoluções futuras, como balanceamento de classes, uso de métricas adicionais e exploração de novos algoritmos.

# Domínio 4: Diretrizes para IA Responsável (14% do exame)

Resumo técnico baseado no guia oficial AWS Certified AI Practitioner (AIF-C01) v1.2, focado em práticas de desenvolvimento ético, transparência, mitigação de riscos e ferramentas da AWS para IA Responsável.

---

## Tarefa 4.1: Características de Sistemas de IA Responsáveis

A AWS define seis dimensões principais para o desenvolvimento e operação de IA Responsável:

1. **Justiça (Fairness):** Garantir que o modelo não discrimine grupos demográficos ou perpetue preconceitos históricos nos dados.
2. **Explicabilidade (Explainability):** Capacidade de entender e explicar como os parâmetros e atributos (features) do modelo levam a uma determinada decisão ou saída.
3. **Privacidade e Segurança (Privacy and Security):** Proteger dados sensíveis (PII) contra vazamentos, acessos não autorizados e inferências maliciosas.
4. **Robustez (Robustness):** Garantir que o sistema mantenha saídas confiáveis mesmo diante de entradas inesperadas, ruídos ou tentativas de manipulação (como prompt injection).
5. **Governança (Governance):** Processos organizacionais para documentar, auditar e controlar o ciclo de vida completo dos modelos.
6. **Transparência (Transparency):** Disponibilizar informações claras aos usuários e partes interessadas sobre as capacidades, limitações e dados usados no modelo.

### Riscos Comuns em Modelos de IA e IA Generativa

* **Viés (Bias):** Distorção sistemática nos resultados causada por dados de treinamento desbalanceados, amostragem incorreta ou premissas humanas durante a rotulagem.
* **Alucinações (Hallucinations):** Quando um Foundation Model gera informações falsas, inventadas ou desconectadas da realidade, mas apresentadas com alta confiança gramatical.
* **Plágio e Violação de Propriedade Intelectual:** Geração de código, texto ou imagem que reproduz diretamente material protegido por direitos autorais presente no conjunto de treinamento.
* **Overfitting e Underfitting:**
  * *Overfitting (Sobreajuste):* O modelo decora os dados de treino e falha ao generalizar para novos dados.
  * *Underfitting (Subajuste):* O modelo é simples demais para capturar os padrões dos dados, apresentando baixo desempenho já no treino.

---

## Tarefa 4.2: Práticas e Ferramentas para IA Transparente e Explicável

### Ferramentas AWS para IA Responsável

* **Amazon Bedrock Guardrails:**
  Implementa camadas de proteção customizáveis sobre os Foundation Models (independente do modelo escolhido). Permite configurar:
  * Filtros de conteúdo (ódio, insultos, violência, conteúdo sexual).
  * Tópicos negados (bloquear assuntos específicos, como aconselhamento financeiro ou médico não autorizado).
  * Filtros de palavras (palavrões, termos de concorrentes).
  * Redação de informações sensíveis (mascarar ou bloquear PII como CPF, cartões de crédito e e-mails na entrada ou na resposta).
  * Verificação de contextualização (Contextual Grounding Check) para detectar e bloquear alucinações em respostas baseadas em RAG.

* **Amazon SageMaker Clarify:**
  Ferramenta focada em detectar viés (bias) em conjuntos de dados (pré-treinamento) e em modelos treinados (pós-treinamento). Também fornece relatórios de explicabilidade (usando valores SHAP) para mostrar quais variáveis mais influenciaram uma previsão específica.

* **AWS AI Service Cards e Amazon SageMaker Model Cards:**
  Documentação centralizada que registra a finalidade pretendida de um modelo, métricas de desempenho, limitações conhecidas, dados de avaliação e considerações éticas. Essencial para transparência e auditoria.

* **Amazon SageMaker Model Monitor:**
  Monitora continuamente a qualidade dos modelos em produção, detectando desvios nos dados (*data drift*) ou desvios no conceito (*concept drift*) que possam degradar a precisão ou introduzir novos vieses ao longo do tempo.

* **Amazon Augmented AI (Amazon A2I):**
  Permite construir fluxos de trabalho com revisão humana (*Human-in-the-loop*) para previsões de baixa confiança, garantindo supervisão humana em decisões críticas.

---

## Resumo Rápido para Prova (Pegadinhas Comuns)

* **Precisa bloquear tópicos proibidos, ocultar PII ou evitar alucinações no Bedrock?** -> **Amazon Bedrock Guardrails**.
* **Precisa identificar viés nos dados ou explicar o peso de cada variável (feature attribution) na decisão do modelo?** -> **Amazon SageMaker Clarify**.
* **Precisa documentar formalmente o propósito, limitações e métricas de um modelo para transparência?** -> **SageMaker Model Cards** (ou AWS AI Service Cards).
* **Precisa adicionar validação humana quando a confiança da inferência for baixa?** -> **Amazon A2I**.
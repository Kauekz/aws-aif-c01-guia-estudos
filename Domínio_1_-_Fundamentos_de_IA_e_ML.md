# 🧠 DOMÍNIO 1 — Fundamentos de IA e ML (20%)

> **Task Statements oficiais:** 1.1 Explicar conceitos básicos | 1.2 Identificar casos de uso | 1.3 Descrever o ciclo de vida de ML

---

## 1.1 Hierarquia e Terminologia Fundamental

```text
┌─────────────────────────────────────────────────────┐
│  AI — Artificial Intelligence (Inteligência Artificial) │
│  ┌────────────────────────────────────────────────┐  │
│  │  ML — Machine Learning (Aprendizado de Máquina)  │  │
│  │  ┌─────────────────────────────────────────┐   │  │
│  │  │  Deep Learning (Aprendizado Profundo)     │   │  │
│  │  │  ┌──────────────────────────────────┐   │   │  │
│  │  │  │  Generative AI (IA Generativa)    │   │   │  │
│  │  │  │  ┌───────────────────────────┐   │   │   │  │
│  │  │  │  │  Agentic AI (IA Agêntica) │   │   │   │  │
│  │  │  │  └───────────────────────────┘   │   │   │  │
│  │  │  └──────────────────────────────────┘   │   │  │
│  │  └─────────────────────────────────────────┘   │  │
│  └────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────┘
```

| Termo (EN) | Termo (PT-BR) | Definição |
|------------|--------------|-----------|
| **Artificial Intelligence (AI)** | Inteligência Artificial (IA) | Campo amplo: sistemas que simulam inteligência humana |
| **Machine Learning (ML)** | Aprendizado de Máquina | Subárea da IA: aprende padrões de dados sem programação explícita |
| **Deep Learning (DL)** | Aprendizado Profundo | Subárea do ML: redes neurais com múltiplas camadas para padrões complexos |
| **Generative AI (GenAI)** | IA Generativa | Especialização de DL: **gera** novo conteúdo (texto, imagem, código, áudio) |
| **Agentic AI** | IA Agêntica | GenAI que **planeja e executa tarefas** autonomamente usando ferramentas |
| **Large Language Model (LLM)** | Modelo de Linguagem de Grande Escala | FM especializado em texto, baseado em arquitetura Transformer |
| **Foundation Model (FM)** | Modelo de Fundação | Modelo grande e genérico, pré-treinado em enormes volumes de dados |
| **Model** | Modelo | Artefato treinado que mapeia entradas em saídas (previsão, geração) |
| **Algorithm** | Algoritmo | Método matemático usado no treinamento (ex: regressão, rede neural) |
| **Training** | Treinamento | Fase onde o modelo aprende padrões dos dados |
| **Inferencing** | Inferência | Fase onde o modelo usa o que aprendeu para fazer previsões |
| **Bias** | Viés | Erro sistemático que distorce resultados de forma injusta |
| **Fairness** | Equidade | Resultados justos e equitativos para todos os grupos |
| **Fit** | Ajuste | Overfitting (sobreajuste) ou Underfitting (subajuste) |

> **Regra de ouro:** Programação tradicional = regras + dados $\rightarrow$ respostas. ML = dados + respostas $\rightarrow$ regras (o modelo).

### Diferenças entre AI, ML, GenAI, Deep Learning e Agentic AI

| Característica | AI | ML | Deep Learning | GenAI | Agentic AI |
|---------------|----|----|--------------|-------|-----------|
| Aprende de dados? | Pode | Sim | Sim | Sim | Sim |
| Gera novo conteúdo? | Não necessariamente | Não | Pode | **Sim** | **Sim** |
| Age autonomamente? | Não | Não | Não | Não | **Sim** |
| Usa ferramentas externas? | Não | Não | Não | Não | **Sim** |
| Exemplos | Regras, busca | Regressão, floresta | CNN, Transformer | Claude, GPT | Bedrock Agents |

---

## 1.2 Tipos de Aprendizado de Máquina

| Tipo (EN) | Tipo (PT-BR) | Dados | Objetivo | Exemplos de uso |
|-----------|-------------|-------|----------|----------------|
| **Supervised Learning** | Aprendizado Supervisionado | **Rotulados** (entrada + resposta correta) | Prever alvo conhecido | Detecção de fraude, previsão de preço |
| └ Classification | Classificação | Rotulados | Prever **categoria discreta** | Spam/não-spam, diagnóstico |
| └ Regression | Regressão | Rotulados | Prever **número contínuo** | Preço de imóvel, temperatura |
| **Unsupervised Learning** | Aprendizado Não-Supervisionado | **Sem rótulo** | Descobrir estrutura | Segmentação de clientes |
| └ Clustering | Agrupamento | Sem rótulo | Agrupar por similaridade | Perfis de clientes, k-Means |
| └ Dimensionality Reduction | Redução de Dimensionalidade | Sem rótulo | Compactar features | PCA, visualização |
| └ Anomaly Detection | Detecção de Anomalias | Sem rótulo | Identificar outliers | Fraude sem histórico, intrusão |
| **Reinforcement Learning (RL)** | Aprendizado por Reforço | Sinal de recompensa | Maximizar recompensa | Robótica, jogos, AWS DeepRacer |
| **Self-supervised Learning** | Aprendizado Auto-supervisionado | Sem rótulo (gera próprios rótulos) | Pré-treinar FMs | Como os LLMs são treinados |

---

## 1.3 Tipos de Dados em IA

| Tipo (EN) | Tipo (PT-BR) | Exemplos |
|-----------|-------------|---------|
| **Labeled data** | Dados rotulados | E-mails com tag spam/não-spam, imagens com anotações |
| **Unlabeled data** | Dados não-rotulados | Texto bruto, imagens sem anotação |
| **Structured data** | Dados estruturados | Tabelas, CSVs, bancos relacionais |
| **Semi-structured data** | Dados semi-estruturados | JSON, XML, logs com metadados |
| **Unstructured data** | Dados não-estruturados | Texto livre, imagens, áudio, vídeo |
| **Tabular data** | Dados tabulares | Planilhas, bancos de dados |
| **Time-series data** | Dados de séries temporais | Preços de ações, sensores IoT |
| **Image data** | Dados de imagem | Fotos, radiografias, capturas de tela |
| **Text data** | Dados de texto | Artigos, e-mails, documentos |

---

## 1.4 Tipos de Inferência

| Tipo (EN) | Tipo (PT-BR) | Quando usar |
|-----------|-------------|------------|
| **Real-time inference** | Inferência em tempo real | Latência baixa, resposta imediata (ex: chatbot) |
| **Batch inference** | Inferência em lote | Alto volume, sem urgência, menor custo (ex: relatório noturno) |
| **Asynchronous inference** | Inferência assíncrona | Payloads grandes (até 1 GB), processamento longo, requisições em fila |
| **Serverless inference** | Inferência serverless | Tráfego intermitente, sem servidor para gerenciar, cold starts aceitáveis |

---

## 1.5 Quando Usar (e NÃO Usar) IA/ML

**✅ Use AI/ML quando:**
- Auxiliar decisões humanas com dados complexos (*Assist human decision making*)
- Escalar soluções que não cabem em regras manuais (*Solution scalability*)
- Automatizar tarefas repetitivas (*Automation*)
- Regras mudam com frequência ou são difíceis de codificar

**❌ NÃO use AI/ML quando:**
- Solução determinística simples resolve (`if/else`, fórmula) — *specific outcome needed*
- Custo-benefício desfavorável (*cost-benefit analysis*)
- Área altamente regulada exige explicabilidade total
- Dados insuficientes para treinar um modelo útil

### ML Tradicional vs Foundation Models (Task 1.2.6 — V1.1)

| Situação | ML Tradicional | Foundation Model |
|----------|---------------|-----------------|
| Tipo de dado | **Dados tabulares** | Texto, imagem, áudio, multimodal |
| Explainability | **Alta** (árvore de decisão) | Baixa (caixa preta) |
| Regulação estrita | **Preferível** | Risco de conformidade |
| Latência/custo fixo | **Previsível** | Variável por token |
| Volume de dados | Funciona com poucos dados rotulados | Aproveita dados não-rotulados |

---

## 1.6 Algoritmos de ML Clássico

### Supervisionado

| Algoritmo (EN) | Algoritmo (PT-BR) | Tipo | Uso |
|---------------|------------------|------|-----|
| **Linear Regression** | Regressão Linear | Regressão | Prever valores numéricos com relação linear |
| **Logistic Regression** | Regressão Logística | Classificação | Classificação binária (probabilidade) |
| **Decision Tree** | Árvore de Decisão | Class./Reg. | Regras interpretáveis, ramos sim/não |
| **Random Forest** | Floresta Aleatória | Class./Reg. | **Ensemble** paralelo de árvores — cada árvore vota |
| **Gradient Boosting / XGBoost** | Gradient Boosting | Class./Reg. | **Ensemble** sequencial — cada árvore corrige erros da anterior |
| **Support Vector Machine (SVM)** | Máquina de Vetores de Suporte | Classificação | Hiperplano que separa classes em alta dimensão |
| **k-Nearest Neighbors (k-NN)** | k-Vizinhos Mais Próximos | Class./Reg. | Classifica pelos $K$ vizinhos mais próximos |
| **Naive Bayes** | Naive Bayes | Classificação | Probabilidade bayesiana — ótimo para texto |
| **Neural Networks** | Redes Neurais | Class./Reg. | Múltiplas camadas aprendem padrões complexos |

### Não-Supervisionado

| Algoritmo (EN) | Algoritmo (PT-BR) | O que faz |
|---------------|------------------|-----------|
| **k-Means Clustering** | Agrupamento k-Means | Agrupa em $K$ clusters por similaridade |
| **DBSCAN** | DBSCAN | Agrupa por densidade, detecta outliers |
| **PCA** (Principal Component Analysis) | Análise de Componentes Principais | Reduz dimensionalidade preservando variância |
| **Isolation Forest** | Floresta de Isolamento | Detecta anomalias isolando pontos atípicos |
| **Autoencoder** | Autocodificador | Rede neural que aprende representação compacta |

> **🎯 Bizu "Conjunto de Árvores":** Random Forest = árvores em **paralelo**, votação por maioria. Gradient Boosting/XGBoost = árvores em **sequência**, cada uma corrige o erro da anterior.

---

## 1.7 Redes Neurais e Deep Learning

### Estrutura de uma Rede Neural

| Componente (EN) | Componente (PT-BR) | O que é |
|-----------------|-------------------|---------|
| **Input Layer** | Camada de Entrada | Recebe os dados brutos (features) |
| **Hidden Layers** | Camadas Ocultas | Aprendem padrões e representações intermediárias |
| **Output Layer** | Camada de Saída | Produz a previsão/classificação final |
| **Weight** | Peso | Força da conexão entre neurônios — aprendido no treino |
| **Bias** | Viés (arquitetural) | Deslocamento da função de ativação |
| **Activation Function** | Função de Ativação | Não-linearidade: ReLU, sigmoid, softmax |
| **Forward Propagation** | Propagação Direta | Dado percorre da entrada à saída para gerar previsão |
| **Loss Function** | Função de Perda | Mede o erro entre previsão e valor real |
| **Backpropagation** | Retropropagação | Ajusta pesos baseado no erro calculado |
| **Gradient Descent** | Descida de Gradiente | Otimização que atualiza pesos na direção que reduz o erro |
| **Epoch** | Época | Uma passagem completa pelo dataset de treino |
| **Batch Size** | Tamanho do Lote | Quantidade de exemplos por atualização de pesos |
| **Learning Rate** | Taxa de Aprendizado | Tamanho do passo na atualização (hiperparâmetro) |

### Arquiteturas de Redes Neurais

| Arquitetura (EN) | Arquitetura (PT-BR) | Especialidade | Uso |
|-----------------|-------------------|--------------|-----|
| **CNN** (Convolutional Neural Network) | Rede Neural Convolucional | Imagens em grade | Visão computacional |
| **RNN / LSTM** | Rede Neural Recorrente | Dados sequenciais | Séries temporais, texto |
| **Transformer** | Transformer | Atenção em sequências longas | LLMs, NLP, GenAI |
| **GAN** (Generative Adversarial Network) | Rede Adversarial Gerativa | Geração realista (generator vs discriminator) | Imagens sintéticas |
| **Autoencoder** | Autocodificador | Compressão e reconstrução | Anomalias, dimensionalidade |
| **Diffusion Model** | Modelo de Difusão | Reversão de ruído | Geração de imagens (Stable Diffusion) |

---

## 1.8 Computer Vision (Visão Computacional)

### Tarefas de Computer Vision

| Tarefa (EN) | Tarefa (PT-BR) | O que faz | AWS Service |
|------------|---------------|-----------|------------|
| **Image Classification** | Classificação de Imagem | 1 label para a imagem inteira | Amazon Rekognition |
| **Object Detection** | Detecção de Objetos | Detecta múltiplos objetos com **bounding boxes** | Amazon Rekognition |
| **Image Segmentation** | Segmentação de Imagem | Classifica cada pixel individualmente | SageMaker (custom) |
| **Facial Recognition** | Reconhecimento Facial | Detecta e identifica rostos | Amazon Rekognition |
| **OCR** (Optical Character Recognition) | Reconhecimento Óptico de Caracteres | Extrai texto de imagens/documentos | Amazon Textract |
| **Activity Recognition** | Reconhecimento de Atividade | Identifica ações em vídeos | Amazon Rekognition |

> **Bounding Box (Caixa Delimitadora):** Retângulo $(x, y, \text{largura}, \text{altura})$ que delimita a posição de um objeto detectado na imagem. Conceito central em **Object Detection**.

### CNN — Componentes

| Camada (EN) | Camada (PT-BR) | Função |
|------------|---------------|--------|
| **Convolutional Layer** | Camada Convolucional | Aplica filtros para detectar bordas, texturas, formas |
| **Pooling Layer** (Max Pooling) | Camada de Pooling | Reduz dimensões (downsampling) |
| **Fully Connected Layer** | Camada Totalmente Conectada | Combina features para classificação final |
| **Feature Map** | Mapa de Features | Output de uma camada convolucional |
| **Kernel / Filter** | Filtro | Matriz de parâmetros aprendíveis da convolução |

### Métricas Específicas de Computer Vision

| Métrica (EN) | Métrica (PT-BR) | Uso |
|-------------|----------------|-----|
| **IoU** (Intersection over Union) | Interseção sobre União | Qualidade das bounding boxes em object detection |
| **mAP** (mean Average Precision) | Precisão Média | Métrica principal de object detection |

### AWS Services de Computer Vision

| Serviço | Função | Cue de Prova |
|---------|--------|-------------|
| **Amazon Rekognition** | Imagem/vídeo: objetos, faces, moderação, PPE, texto | Qualquer análise de imagem sem ML customizado |
| **Amazon Textract** | OCR: extrai texto, formulários, tabelas de documentos | "Extrair campos de formulário", "digitalizar notas fiscais" |
| **Amazon Lookout for Vision** | Detecta **defeitos visuais** em inspeção industrial | "Controle de qualidade na fábrica", "defeito em produto" |
| **AWS Panorama** | Leva CV para câmeras **on-premises** (edge) | "Análise de vídeo na fábrica sem enviar à cloud" |
| **AWS DeepLens** | Câmera com deep learning para aprendizado/experimentos | Mencionado em contexto educacional |

---

## 1.9 NLP — Natural Language Processing

| Tarefa (EN) | Tarefa (PT-BR) | AWS Service |
|------------|---------------|------------|
| **Sentiment Analysis** | Análise de Sentimento | Amazon Comprehend |
| **Named Entity Recognition (NER)** | Reconhecimento de Entidades | Amazon Comprehend |
| **Text Classification** | Classificação de Texto | Amazon Comprehend |
| **Machine Translation** | Tradução Automática | Amazon Translate |
| **Speech-to-Text (ASR)** | Fala para Texto | Amazon Transcribe |
| **Text-to-Speech (TTS)** | Texto para Fala | Amazon Polly |
| **Question Answering** | Perguntas e Respostas | Amazon Bedrock + RAG |
| **Text Summarization** | Sumarização de Texto | Amazon Bedrock |

---

## 1.10 Ciclo de Vida de ML (Pipeline)

```text
1. Business Problem Definition (Definir problema de negócio)
       ↓
2. Data Collection (Coletar dados) → Amazon S3
       ↓
3. EDA + Data Preparation / Feature Engineering → SageMaker Data Wrangler, AWS Glue
       ↓
4. Model Training (Treinar modelo) → SageMaker Training Jobs
       ↓
5. Hyperparameter Tuning (Ajuste de hiperparâmetros) → SageMaker Automatic Model Tuning
       ↓
6. Model Evaluation (Avaliar modelo) → Métricas
       ↓
7. Deployment (Deploy) → SageMaker Endpoints, Bedrock, API
       ↓
8. Monitoring (Monitorar) → SageMaker Model Monitor
       ↓
   ← Iterate (Iterar — voltar a qualquer etapa) ←
```

**Conceitos críticos do ciclo:**

| Conceito (EN) | Conceito (PT-BR) | O que é |
|--------------|-----------------|---------|
| **Feature Engineering** | Engenharia de Features | Transformar dados brutos em variáveis úteis para o modelo |
| **Hyperparameters** | Hiperparâmetros | Configurações do treinamento (ex: learning rate) — definidos antes do treino |
| **Hyperparameter Tuning** | Ajuste de Hiperparâmetros | Testar combinações para encontrar a melhor configuração |
| **Model Drift** | Deriva do Modelo | Degradação quando dados reais divergem dos dados de treino |
| **Retraining** | Retreinamento | Retreinar com dados atualizados para corrigir drift |
| **MLOps** | MLOps | Práticas de CI/CD, versionamento e governança para ML em produção |

### MLOps — Conceitos Fundamentais

| Conceito (EN) | Conceito (PT-BR) | Descrição |
|--------------|-----------------|-----------|
| **Experimentation** | Experimentação | Testar diferentes abordagens e hiperparâmetros |
| **Repeatable processes** | Processos reproduzíveis | Pipelines auditáveis e reexecutáveis |
| **Scalable systems** | Sistemas escaláveis | Infraestrutura que cresce com a demanda |
| **Technical debt management** | Gestão de dívida técnica | Manter qualidade do código e pipeline |
| **Production readiness** | Prontidão para produção | Validação antes do deploy |
| **Model monitoring** | Monitoramento do modelo | Detectar drift e degradação |
| **Model re-training** | Retreinamento | Atualizar o modelo com dados novos |

### Métodos de Deploy em Produção

| Método (EN) | Método (PT-BR) | Descrição |
|------------|---------------|-----------|
| **Managed API service** | Serviço de API gerenciado | AWS gerencia infra, escalabilidade e disponibilidade (ex: Bedrock, SageMaker Endpoint) |
| **Self-hosted API** | API auto-hospedada | Você gerencia a infraestrutura (ex: EC2 com modelo próprio) |

---

## 1.11 Métricas de Avaliação

### Classificação

| Métrica (EN) | Métrica (PT-BR) | O que mede | Quando priorizar |
|-------------|----------------|-----------|-----------------|
| **Accuracy** | Acurácia | % de previsões corretas no total | Classes balanceadas |
| **Precision** | Precisão | Dos positivos previstos, quantos eram reais | FP caro (spam bloqueando e-mail legítimo) |
| **Recall** | Revocação / Sensibilidade | Dos positivos reais, quantos foram detectados | FN perigoso (fraude, doença) |
| **F1 Score** | F1 Score | Média harmônica de Precision e Recall | Classes desbalanceadas |
| **AUC-ROC** | Área sob a Curva ROC | Capacidade de separar classes | Comparar modelos |

**Matriz de Confusão (Confusion Matrix):**
- **TP** (True Positive / Verdadeiro Positivo): previu positivo, era positivo ✅
- **TN** (True Negative / Verdadeiro Negativo): previu negativo, era negativo ✅
- **FP** (False Positive / Falso Positivo): previu positivo, era negativo ❌ (alarme falso)
- **FN** (False Negative / Falso Negativo): previu negativo, era positivo ❌ (perda)

### Regressão

| Métrica (EN) | Métrica (PT-BR) | Detalhe |
|-------------|----------------|---------|
| **MAE** (Mean Absolute Error) | Erro Médio Absoluto | Fácil de interpretar |
| **MSE** (Mean Squared Error) | Erro Quadrático Médio | Penaliza erros grandes |
| **RMSE** (Root MSE) | Raiz do Erro Quadrático Médio | Mesma unidade do dado original |
| **$R^2$** (R-squared) | Coeficiente de Determinação | Proporção da variância explicada ($0$ a $1$, maior = melhor) |

### Métricas de Negócio (Business Metrics — Task 1.3.6)

| Métrica (EN) | Métrica (PT-BR) | O que mede |
|-------------|----------------|-----------|
| **ROI** (Return on Investment) | Retorno sobre Investimento | Retorno financeiro do projeto de IA |
| **Cost per user** | Custo por usuário | Custo operacional por usuário atendido |
| **Development costs** | Custos de desenvolvimento | Custo total de construção e manutenção |
| **Customer feedback** | Feedback de clientes | Avaliação qualitativa do impacto |

### Overfitting vs Underfitting

| Problema (EN) | Problema (PT-BR) | Causa | Consequência | Solução |
|--------------|-----------------|-------|-------------|---------|
| **Overfitting** | Sobreajuste (alta variância) | Modelo complexo demais, "decorou" os dados | Ótimo no treino, ruim em produção | Mais dados, regularização, early stopping |
| **Underfitting** | Subajuste (alto viés) | Modelo simples demais | Performance ruim em treino e produção | Modelo mais complexo, mais features, mais épocas |

---

## 1.12 Stack de IA/ML da AWS (3 Camadas)

| Camada (EN) | Camada (PT-BR) | Para quem | Exemplos |
|------------|---------------|----------|---------|
| **AI Services** (topo) | Serviços de IA | Devs sem ML | Rekognition, Comprehend, Textract, Transcribe, Polly, Translate, Lex |
| **ML Platform** (meio) | Plataforma de ML | Data scientists | Amazon SageMaker AI |
| **Frameworks & Infra** (base) | Frameworks e Infra | Pesquisadores | EC2 GPU, TensorFlow, PyTorch |
| **GenAI** (ala separada) | IA Generativa | Devs, analistas | Amazon Bedrock, Amazon Q |

---

## 1.13 Amazon SageMaker AI — Mapa Completo

| Ferramenta | Etapa | O que faz | Cue de Prova |
|-----------|-------|-----------|-------------|
| **SageMaker Studio** | Todo o ciclo | IDE web para o workflow completo de ML | "Ambiente unificado para data scientists" |
| **SageMaker Canvas** | Build | ML **sem código** para analistas de negócio | "Sem código", "analista de negócio", "previsão de tabela" |
| **SageMaker Ground Truth** | Rotulagem | Rotular dados com humanos + automação | "Rotular dados de treino", "anotação humana", "bounding boxes" |
| **SageMaker Data Wrangler** | Preparação | Importar, limpar, transformar dados visualmente | "Preparar dados com pouco código" |
| **SageMaker Feature Store** | Preparação | Repositório centralizado e reutilizável de features | "Reutilizar features entre modelos" |
| **SageMaker Autopilot** | Treinamento | **AutoML** — explora e treina candidatos automaticamente | "AutoML", "testar múltiplos modelos automaticamente" |
| **SageMaker JumpStart** | Build/Fine-tuning | Hub de modelos pré-treinados e FMs (hospedados no SageMaker) | "Modelo pré-treinado no SageMaker", "fine-tune FM no SageMaker" |
| **SageMaker Training** | Treinamento | Jobs de treinamento gerenciados | "Treinar modelo customizado" |
| **SageMaker Automatic Model Tuning** | Treinamento | Otimização automática de hiperparâmetros | "Hyperparameter tuning" |
| **SageMaker Clarify** | Avaliação | Detectar viés + explicar previsões (SHAP) | "Detectar bias", "explicar previsão", "fairness" |
| **SageMaker Endpoints** | Deploy | Hospeda o modelo para inferência | "Deploy do modelo", "endpoint de inferência" |
| **Batch Transform** | Deploy | Inferência em lote sem endpoint permanente | "Pontuar dataset inteiro offline" |
| **SageMaker Model Monitor** | Monitoramento | Detecta **drift** em produção | "Drift", "modelo degradou em produção" |
| **SageMaker Pipelines** | MLOps | CI/CD para ML | "Automatizar workflow ML", "pipeline reproduzível" |
| **SageMaker Model Registry** | MLOps | Versiona e aprova modelos | "Versionar modelos", "aprovação antes de produção" |
| **SageMaker Model Cards** | Governança | Documenta propósito, limites e métricas | "Documentar modelo", "transparência" |
| **SageMaker Model Dashboard** | Governança | Visão centralizada de todos os modelos em produção | "Visão centralizada de modelos deployados" |
| **SageMaker Role Manager** | Governança | Cria roles IAM para personas ML | "Roles IAM para equipe de ML" |

### Opções de Inferência no SageMaker

| Opção (EN) | Opção (PT-BR) | Quando usar |
|-----------|-------------|------------|
| **Real-time Endpoint** | Endpoint em Tempo Real | Latência baixa, tráfego constante |
| **Serverless Inference** | Inferência Serverless | Tráfego intermitente/imprevisível |
| **Asynchronous Inference** | Inferência Assíncrona | Payloads grandes, processamento longo |
| **Batch Transform** | Transformação em Lote | Pontuação de dataset inteiro offline, sem endpoint |

---

## 1.14 AI Services — Mapa Completo

| Serviço | Função (EN) | Função (PT-BR) | Status |
|---------|------------|---------------|--------|
| **Amazon Rekognition** | Image/video analysis | Análise de imagem/vídeo | ✅ In-scope |
| **Amazon Textract** | Document text extraction (OCR) | Extração de texto de documentos | ✅ In-scope |
| **Amazon Comprehend** | NLP: sentiment, entities, PII | NLP: sentimento, entidades, PII | ✅ In-scope |
| **Amazon Transcribe** | Speech-to-text | Fala $\rightarrow$ texto | ✅ In-scope |
| **Amazon Polly** | Text-to-speech | Texto $\rightarrow$ fala | ✅ In-scope |
| **Amazon Translate** | Machine translation | Tradução automática | ✅ In-scope |
| **Amazon Lex** | Chatbots and voice bots | Chatbots e bots de voz | ✅ In-scope |
| **Amazon Personalize** | Real-time recommendations | Recomendações em tempo real | ✅ In-scope |
| **Amazon Lookout for Vision** | Industrial defect detection | Detecção de defeitos industriais | ✅ In-scope |
| ~~Amazon Forecast~~ | Time series forecasting | Séries temporais | ⛔ Fechado jul/2024 $\rightarrow$ use SageMaker Canvas |
| ~~Amazon Kendra~~ | Intelligent search | Busca inteligente | ⛔ Fora do escopo V1.1 |
| ~~Amazon Fraud Detector~~ | Fraud detection | Detecção de fraude | ⛔ Fechado nov/2025 |

---
> 📂 **Navegar:** [🏠 Início (README)](README.md) | **[D1 IA-ML](AIF-C01-D1-Fundamentos-IA-ML.md)** | [D2 GenAI](AIF-C01-D2-Fundamentos-GenAI.md) | [D3 FMs](AIF-C01-D3-Aplicacoes-FM.md) | [D4 Responsável](AIF-C01-D4-IA-Responsavel.md) | [D5 Segurança](AIF-C01-D5-Seguranca-Governanca.md) | [D6 Referência](AIF-C01-D6-Referencia-Estrategia.md)
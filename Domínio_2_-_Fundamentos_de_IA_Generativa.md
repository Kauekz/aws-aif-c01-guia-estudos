# ✨ DOMÍNIO 2 — Fundamentos de IA Generativa (24%)

> **Task Statements oficiais:** 2.1 Explicar conceitos básicos | 2.2 Capacidades e limitações | 2.3 Infraestrutura e tecnologias AWS

---

## 2.1 Vocabulário Fundamental de GenAI

| Termo (EN) | Termo (PT-BR) | Definição |
|------------|--------------|-----------|
| **Token** | Token | Unidade básica que o modelo lê/escreve. $\approx 3/4$ de palavra. **Custo e limites = tokens** |
| **Context Window** | Janela de Contexto | Máximo de tokens que o modelo processa de uma vez (entrada + saída). Se cheia, "esquece" |
| **Chunking** | Chunking (Segmentação) | Dividir textos longos em pedaços menores — fundamental para RAG |
| **Embedding** | Embedding (Incorporação) | Representação **numérica do significado** em vetor. Base da busca semântica |
| **Vector** | Vetor | Array de números representando um embedding. Usado para similaridade |
| **Prompt** | Prompt | Entrada de texto que guia a resposta do modelo |
| **Prompt Engineering** | Engenharia de Prompt | Arte de projetar instruções/contexto para guiar saídas do modelo |
| **Foundation Model (FM)** | Modelo de Fundação | Modelo grande e genérico, pré-treinado em enormes volumes de dados |
| **Transformer** | Transformer | Arquitetura baseada em **atenção** que alimenta os LLMs modernos |
| **LLM** (Large Language Model) | Modelo de Linguagem de Grande Escala | FM especializado em texto |
| **Multimodal Model** | Modelo Multimodal | Processa múltiplas modalidades: texto + imagem + áudio + vídeo |
| **Diffusion Model** | Modelo de Difusão | Arquitetura para **geração de imagens** (reverte processo de adição de ruído) |
| **Hallucination** | Alucinação | Modelo gera informação **plausível mas falsa** com alta confiança |
| **Grounding** | Fundamentação | Ancorar respostas em fontes verificáveis para reduzir alucinação |
| **Nondeterminism** | Não-determinismo | Mesma entrada pode gerar saídas diferentes |
| **Training cutoff** | Corte de treinamento | Data limite do conhecimento do modelo — não conhece eventos posteriores |

### Tipos de Foundation Models

| Tipo (EN) | Tipo (PT-BR) | O que faz | Quando a prova menciona |
|-----------|-------------|-----------|------------------------|
| **LLM** | Modelo de Linguagem | Gera e processa texto token a token | "gerar texto", "chatbot", "sumarizar" |
| **Embedding Model** | Modelo de Embedding | Converte texto em vetor — **NÃO gera resposta** | "busca semântica", "similaridade" |
| **Diffusion Model** | Modelo de Difusão | Gera imagens | "gerar imagens" $\rightarrow$ diffusion, não LLM |
| **Multimodal Model** | Modelo Multimodal | Texto + imagem + áudio juntos | "analisar imagem e texto juntos" |
| **Instruction-tuned Model** | Modelo Ajustado por Instrução | Treinado com RLHF para seguir instruções — melhor para chatbots | "chatbot que segue instruções" |
| **Base/Completion Model** | Modelo Base | Completa texto sem seguir instruções diretamente | Pré-treino, não ideal para uso direto |

> **Bizu:** Embedding model $\neq$ LLM. Embedding **converte** texto em número para busca. LLM **gera** texto novo.

---

## 2.2 Tipos de Alucinação

| Tipo (EN) | Tipo (PT-BR) | O que é |
|-----------|-------------|---------|
| **Factual Hallucination** | Alucinação Factual | Informação factualmente incorreta apresentada com alta confiança |
| **Attribution Hallucination** | Alucinação de Atribuição | Atribui informação a uma fonte incorreta |
| **Context Hallucination** | Alucinação de Contexto | Contradiz informações presentes no próprio contexto fornecido |
| **Confabulation** | Confabulação | Inventa detalhes plausíveis para preencher lacunas de conhecimento |

---

## 2.3 Vantagens e Limitações da GenAI

### Vantagens (Advantages)

| Vantagem (EN) | Vantagem (PT-BR) |
|--------------|-----------------|
| **Adaptability** | Adaptabilidade — um modelo faz múltiplas tarefas |
| **Responsiveness** | Responsividade — latência adequada para interações |
| **Conversational capabilities** | Capacidades conversacionais — diálogo natural |
| **Content generation** | Geração de conteúdo — texto, imagem, código em escala |

### Limitações (Disadvantages)

| Limitação (EN) | Limitação (PT-BR) | Detalhe |
|---------------|-----------------|---------|
| **Hallucinations** | Alucinações | Gera fatos errados com alta confiança — principal risco |
| **Interpretability / Black box** | Interpretabilidade | Difícil explicar por que chegou a determinada resposta |
| **Inaccuracy** | Imprecisão | Pode estar errado mesmo parecendo certo |
| **Nondeterminism** | Não-determinismo | Mesma entrada $\rightarrow$ saídas diferentes |
| **Bias** | Viés | Reproduz preconceitos dos dados de treino |
| **Cost** | Custo | Alto custo de tokens em escala |
| **Training cutoff** | Corte de treinamento | Não conhece eventos após a data de corte |
| **Toxicity** | Toxicidade | Pode produzir conteúdo ofensivo ou prejudicial |

---

## 2.4 Ciclo de Vida de um Foundation Model

```text
Data Selection → Model Selection → Pre-training → Fine-tuning → Evaluation → Deployment → Feedback
(Seleção de Dados) → (Seleção do Modelo) → (Pré-treinamento) → (Ajuste Fino) → (Avaliação) → (Deploy) → (Feedback)
                                                                           ↑___________________________|
```

---

## 2.5 Token-Based Pricing (Precificação por Token — Task 2.1.4)

| Conceito (EN) | Conceito (PT-BR) | Detalhe |
|--------------|-----------------|---------|
| **Input tokens** | Tokens de entrada | Tokens do prompt enviado ao modelo |
| **Output tokens** | Tokens de saída | Tokens da resposta gerada — **geralmente custam mais** |
| **On-demand pricing** | Precificação sob demanda | Paga por token usado, flexível |
| **Provisioned Throughput** | Throughput Provisionado | Reserva capacidade dedicada, custo por hora — melhor para alto volume constante |
| **Prompt Caching** | Cache de Prompt | Cache da parte estática do prompt para reduzir custo e latência |

### Estratégias para Reduzir Custo de Tokens

| Estratégia (EN) | Estratégia (PT-BR) | Como reduz custo |
|----------------|------------------|-----------------|
| Shorter prompts | Prompts mais curtos | Menos tokens de entrada |
| Smaller model | Modelo menor | Menor custo por token |
| Prompt Caching | Cache de Prompt | Prefixos repetidos não são cobrados novamente |
| Batch inference | Inferência em lote | Menor custo por request |
| Distillation | Destilação | Modelo pequeno com qualidade similar ao grande |
| Provisioned Throughput | Throughput Provisionado | Volume alto constante $\rightarrow$ custo menor por token |
| AWS Budgets | AWS Budgets | Definir alertas de orçamento para gastos com Bedrock/SageMaker |
| AWS Cost Explorer | AWS Cost Explorer | Analisar e visualizar custos de IA/ML por serviço e período |

---

## 2.6 Context Engineering (Engenharia de Contexto — Task 2.1.5)

Prática de gerenciar **estrategicamente** o que entra na context window — não apenas como instruir, mas **o que incluir no contexto**:

- Selecionar apenas chunks relevantes do RAG
- Comprimir histórico de conversa preservando informação
- Usar prompt caching para prefixos repetidos
- Gerenciar memória de conversa longa
- Balancear qualidade vs custo de tokens

> **Prompt Engineering = COMO instruir o modelo.** **Context Engineering = O QUE colocar na janela de contexto.**

---

## 2.7 Agentic AI — Conceitos Fundamentais (Task 2.1.6 — V1.1)

| Conceito (EN) | Conceito (PT-BR) | Definição |
|--------------|-----------------|-----------|
| **Agentic AI** | IA Agêntica | GenAI que planeja e executa tarefas multi-etapa usando ferramentas |
| **Agent** | Agente | FM + ferramentas + memória + loop de raciocínio-ação-observação |
| **Tool use** | Uso de ferramentas | Agente chama APIs, bancos de dados, funções externas |
| **Memory management** | Gestão de memória | Short-term (sessão atual) vs Long-term (entre sessões) |
| **Workflow orchestration** | Orquestração de workflow | Coordenar múltiplas etapas e agentes |
| **MCP** (Model Context Protocol) | Protocolo de Contexto de Modelo | Protocolo **aberto** para conectar agentes a ferramentas externas |

### Padrões Multi-agente (Multi-agent Patterns)

| Padrão (EN) | Padrão (PT-BR) | Como funciona |
|------------|---------------|--------------|
| **Supervisor + Specialists** | Supervisor + Especialistas | Um agente orquestrador delega sub-tarefas a agentes especialistas |
| **Sequential** | Sequencial | Agentes executam em sequência, passando resultado ao próximo |
| **Parallel** | Paralelo | Agentes executam tarefas independentes em paralelo |

### Tipos de Memória de Agentes

| Tipo (EN) | Tipo (PT-BR) | Duração |
|-----------|-------------|---------|
| **Short-term memory** | Memória de curto prazo | Dura apenas a sessão atual (context window) |
| **Long-term memory** | Memória de longo prazo | Persiste entre sessões (armazenada externamente) |

---

## 2.8 Fatores para Seleção de Modelos GenAI

| Fator (EN) | Fator (PT-BR) | Por que importa |
|-----------|-------------|----------------|
| **Cost** | Custo | Preço por token (entrada + saída) |
| **Latency** | Latência | Tempo de resposta — real-time exige baixa latência |
| **Throughput** | Throughput | Requisições simultâneas suportadas |
| **Model size / complexity** | Tamanho/complexidade | Equilíbrio entre qualidade e eficiência |
| **Multilingual** | Multilíngue | Suporte aos idiomas necessários |
| **Modality** | Modalidade | Texto, imagem, áudio, multimodal |
| **Context length** | Tamanho do contexto | Limite de tokens por requisição |
| **Customization** | Customização | Fine-tuning, flexibilidade de prompts |
| **Compliance** | Conformidade | Requisitos regulatórios e de privacidade |
| **Prompt Caching** | Cache de Prompt | Eficiência para prefixos repetidos |

### Métricas de Valor de Negócio para GenAI (Task 2.2.4)

| Métrica (EN) | Métrica (PT-BR) | O que mede |
|-------------|----------------|-----------|
| **ROI** (Return on Investment) | Retorno sobre Investimento | Ganho financeiro do projeto de GenAI |
| **Efficiency** | Eficiência | Ganho de produtividade com automação |
| **Conversion rate** | Taxa de conversão | % de usuários que convertem após interação com IA |
| **ARPU** (Average Revenue Per User) | Receita média por usuário | Impacto da IA na receita por usuário |
| **Accuracy** | Acurácia | Precisão das respostas geradas |
| **CLV** (Customer Lifetime Value) | Valor do ciclo de vida do cliente | Impacto da IA na retenção de clientes |
| **Cross-domain performance** | Desempenho multi-domínio | Eficácia do modelo em diferentes contextos |

---

## 2.9 FMs Disponíveis no Amazon Bedrock

| Provedor | Modelos | Especialidade |
|---------|---------|--------------|
| **Anthropic** | Claude 3/3.5 (Haiku, Sonnet, Opus) | Texto, raciocínio, segurança (Constitutional AI) |
| **Meta** | Llama 3, Llama 3.1 | Open-source, texto |
| **Mistral AI** | Mistral, Mixtral | Texto eficiente |
| **Amazon Nova** | Nova Micro/Lite/Pro (texto), Nova Canvas (imagens), Nova Reel (vídeo), Nova Sonic (voz) | Família atual da Amazon no Bedrock |
| **Stability AI** | Stable Diffusion (SDXL) | Geração de imagens (diffusion) |
| **Cohere** | Command (texto), Embed (embeddings) | Texto e embeddings corporativos |

> **Constitutional AI (IA Constitucional):** Abordagem da **Anthropic** para treinar modelos Claude com princípios que guiam autoavaliação. **Não é serviço AWS** — é técnica de treinamento.

---

## 2.10 AWS Services de GenAI

| Serviço | Função (EN) | Função (PT-BR) | Cue de Prova |
|---------|------------|---------------|-------------|
| **Amazon Bedrock** | Serverless FM API | API serverless para acessar FMs de múltiplos provedores | "sem infra", "sem gerenciar modelo" |
| **Bedrock Playground** | Visual FM testing in console | Testar FMs no console sem código | "testar FMs no console sem código" |
| **PartyRock** | External Bedrock playground | Playground externo sem conta AWS | "prototipar sem conta AWS" |
| **Bedrock Studio** | Team collaboration for GenAI apps | Interface colaborativa para equipes | "colaboração de equipe para app GenAI" |
| **Amazon SageMaker AI** | Custom ML/FM platform | Plataforma para ML/FM customizado | "treinar modelo próprio" |
| **SageMaker JumpStart** | Pre-trained model hub in SageMaker | Hub de modelos pré-treinados no SageMaker | "FM no SageMaker com controle total" |
| **Amazon Quick** | Agentic BI workspace for analysts | Workspace agêntico de BI para analistas | "analista + BI + dados + chat" |
| **Kiro** | Spec-driven agentic IDE | IDE agêntica spec-driven | "IDE com IA para desenvolvimento" |
| **Strands Agents** | Open-source agent SDK | SDK open-source para construir agentes | "SDK open-source para agentes" |
| **Bedrock AgentCore** | Production agent platform | Plataforma de produção para agentes | "agentes em produção, escala, qualquer framework" |
| **Amazon Q Developer** | AI coding assistant | Assistente de código na IDE | "assistente de código na IDE" |
| **Amazon Q Business** | Enterprise knowledge Q&A | Q&A sobre documentos internos da empresa | "Q&A sobre docs internos corporativos" |
| **AWS Transform** | Workload modernization agents | Agentes para modernizar mainframe/.NET/VMware | "modernizar mainframe com IA" |

---
> 📂 **Navegar:** [🏠 Início (README)](README.md) | [D1 IA-ML](AIF-C01-D1-Fundamentos-IA-ML.md) | **[D2 GenAI](AIF-C01-D2-Fundamentos-GenAI.md)** | [D3 FMs](AIF-C01-D3-Aplicacoes-FM.md) | [D4 Responsável](AIF-C01-D4-IA-Responsavel.md) | [D5 Segurança](AIF-C01-D5-Seguranca-Governanca.md) | [D6 Referência](AIF-C01-D6-Referencia-Estrategia.md)
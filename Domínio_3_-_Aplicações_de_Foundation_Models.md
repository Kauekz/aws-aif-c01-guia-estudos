# 🔧 DOMÍNIO 3 — Aplicações de Foundation Models (28%)

> **Task Statements oficiais:** 3.1 Considerações de design | 3.2 Prompt engineering | 3.3 Treinamento e fine-tuning | 3.4 Métodos de avaliação

---

## 3.1 Critérios de Seleção de FM

| Fator (EN) | Fator (PT-BR) | Por que importa |
|-----------|-------------|----------------|
| **Cost** | Custo | Preço por token (entrada + saída) |
| **Modality** | Modalidade | Texto, imagem, áudio, multimodal |
| **Latency** | Latência | Tempo de resposta (real-time exige baixa) |
| **Multi-lingual** | Multilíngue | Idiomas suportados |
| **Model size / complexity** | Tamanho/complexidade | Equilíbrio qualidade vs eficiência |
| **Customization** | Customização | Fine-tuning, flexibilidade de prompts |
| **Input/output length** | Comprimento entrada/saída | Context window máximo |
| **Prompt caching** | Cache de prompt | Eficiência para prefixos repetidos |

---

## 3.2 Parâmetros de Inferência

| Parâmetro (EN) | Parâmetro (PT-BR) | Efeito |
|---------------|-----------------|--------|
| **Temperature** | Temperatura | **Alto** = criativo/aleatório · **Baixo** = determinístico/focado |
| **Top-P** (nucleus sampling) | Top-P | Considera tokens até acumular $P$ de probabilidade |
| **Top-K** | Top-K | Considera apenas os $K$ tokens mais prováveis |
| **Max output tokens** | Máximo de tokens de saída | Limita o tamanho máximo da resposta |
| **Stop sequences** | Sequências de parada | Tokens que encerram a geração |

> **Temperature baixa $\rightarrow$ FAQ, respostas factuais. Temperature alta $\rightarrow$ brainstorm, nomes criativos.**

---

## 3.3 RAG — Retrieval Augmented Generation (Geração Aumentada por Recuperação)

**Definição:** Recupera documentos relevantes de base de conhecimento externa e fornece como contexto ao FM para gerar respostas fundamentadas.

```text
Pergunta do usuário
      ↓
Gerar embedding da pergunta (Query Embedding)
      ↓
Busca vetorial na base de conhecimento (Vector Search)
      ↓
Recuperar chunks relevantes (Chunk Retrieval)
      ↓
FM gera resposta fundamentada no contexto (Grounded Response)
      ↓
Resposta com citação de fonte (Cited Answer)
```

**Por que usar RAG:**
- Reduz **alucinações** — resposta baseada em fonte verificável
- Mantém respostas **atualizadas** sem retreinar o modelo
- Acessa **conhecimento privado/interno** sem expor ao FM
- Mais barato que fine-tuning para atualizar conhecimento

**AWS:** Amazon Bedrock Knowledge Bases (RAG gerenciado)

### Chunking Strategies (Estratégias de Segmentação)

| Estratégia (EN) | Estratégia (PT-BR) | O que faz | Quando usar |
|----------------|------------------|-----------|------------|
| **Fixed-size chunking** | Segmentação por tamanho fixo | Chunks de $N$ tokens com sobreposição configurável | Documentos uniformes |
| **Default chunking** | Segmentação padrão | Bedrock escolhe automaticamente (~300 tokens, 20% overlap) | Sem requisito específico |
| **Semantic chunking** | Segmentação semântica | Agrupa sentenças semanticamente relacionadas (tamanho variável) | "Chunks que respeitam o significado" |
| **Hierarchical chunking** | Segmentação hierárquica | Parent (contexto amplo) + Child (precisão) — recupera child, retorna parent | "Manter contexto ao redor do trecho" |
| **No chunking** | Sem segmentação | Arquivo = 1 chunk, pré-processamento externo | Documentos já segmentados |

> ⚠️ **Chunking strategy NÃO pode ser alterada após criar a data source no Bedrock Knowledge Bases.**

### Técnicas Avançadas de RAG

| Técnica (EN) | Técnica (PT-BR) | O que faz | Cue |
|-------------|----------------|-----------|-----|
| **Reranking** | Reranqueamento | Após recuperar $N$ chunks, modelo reordena pelos mais relevantes | "retrieval traz chunks irrelevantes" |
| **Hybrid search** | Busca híbrida | Combina busca vetorial (semântica) + keyword (BM25) | "busca semântica não acha termos técnicos" |
| **Metadata filtering** | Filtragem de metadados | Filtra por metadados (data, autor, categoria) antes do ranking | "responder só com docs de 2024" |
| **GraphRAG** | RAG com grafo | RAG usando grafo de conhecimento (Neptune Analytics) | "relacionamentos entre entidades importam" |

### Bancos Vetoriais na AWS (Vector Databases)

| Serviço | Uso |
|---------|-----|
| **Amazon OpenSearch Service** | Busca + similaridade vetorial (mais comum para RAG) |
| **Amazon Aurora PostgreSQL** | BD relacional com extensão pgvector |
| **Amazon RDS for PostgreSQL** | Idem acima |
| **Amazon Neptune** | Grafos + recuperação relacional (GraphRAG) |
| **Amazon DocumentDB** | Compatível com MongoDB |
| **Amazon ElastiCache** | Cache in-memory — embeddings de baixa latência (in-scope V1.2) |

---

## 3.4 Estratégias de Customização de FM (do mais barato ao mais caro)

| Abordagem (EN) | Abordagem (PT-BR) | Muda pesos? | Custo | Melhor para |
|---------------|-----------------|------------|-------|------------|
| **Prompt engineering / In-context learning** | Engenharia de prompt | ❌ Não | 💰 Baixo | Iterações rápidas, tarefas gerais |
| **RAG** | RAG | ❌ Não | 💰💰 Médio | Conhecimento privado/atualizado, citações |
| **Fine-tuning / Instruction tuning** | Ajuste fino | ✅ Sim | 💰💰💰 Alto | Estilo consistente, domínio específico, comportamento |
| **Continued pre-training** | Pré-treinamento contínuo | ✅ Sim | 💰💰💰 Alto | Vocabulário de domínio sem labels |
| **Model distillation** | Destilação de modelo | ✅ Sim (novo modelo) | 💰💰 Médio | Reduzir custo/latência mantendo qualidade |
| **Pre-training from scratch** | Pré-treinamento do zero | ✅ Sim | 💰💰💰💰 Altíssimo | Raramente justificado |

> **RAG $\rightarrow$ dados que mudam. Fine-tuning $\rightarrow$ comportamento/estilo que não muda.**

### Fine-tuning — Métodos

| Método (EN) | Método (PT-BR) | Dados | O que aprende |
|------------|---------------|-------|--------------|
| **Instruction tuning** | Ajuste por instrução | Pares instrução$\rightarrow$resposta (**rotulados**) | Seguir instruções, comportamento |
| **Domain adaptation / Continued pre-training** | Adaptação de domínio | Textos do domínio (**não-rotulados**) | Vocabulário especializado |
| **Transfer learning** | Transferência de aprendizado | Reutiliza modelo pré-treinado para nova tarefa | Reduz dados e tempo necessários |
| **RLHF** (Reinforcement Learning from Human Feedback) | RL com Feedback Humano | Ranking de respostas por humanos | Preferências humanas, alinhamento de valores |

### Fine-tuning — Técnicas Eficientes (PEFT)

| Técnica (EN) | Técnica (PT-BR) | O que faz | Quando usar |
|-------------|----------------|-----------|------------|
| **LoRA** (Low-Rank Adaptation) | Adaptação de Baixo Rank | Treina apenas matrizes de baixo rank inseridas — drasticamente menos GPU | "Fine-tuning com recursos limitados" |
| **QLoRA** (Quantized LoRA) | LoRA Quantizado | LoRA + quantização 4-bit do modelo base — fine-tuning de modelos grandes em 1 GPU | "Fine-tuning de modelo 13B+ em GPU única" |

### Destilação de Modelos (Model Distillation)

| Conceito (EN) | Conceito (PT-BR) | Descrição |
|--------------|-----------------|-----------|
| **Teacher model** | Modelo professor | FM maior e mais capaz que gera dados de alta qualidade |
| **Student model** | Modelo aluno | Modelo menor treinado para imitar o teacher |
| **Distillation** | Destilação | Teacher gera dados sintéticos $\rightarrow$ student aprende com eles |

> **Distillation $\neq$ Fine-tuning:** Distillation usa dados sintéticos do teacher. Fine-tuning usa dados reais rotulados.

### Preparação de Dados para Fine-tuning (Task 3.3)

| Aspecto (EN) | Aspecto (PT-BR) | Detalhe |
|-------------|----------------|---------|
| **Data curation** | Curadoria de dados | Selecionar dados de qualidade, remover noise |
| **Data governance** | Governança de dados | Controle de origem, uso e conformidade |
| **Size** | Tamanho | Dados suficientes para generalização |
| **Labeling** | Rotulagem | Dados rotulados de alta qualidade (instruction tuning) |
| **Representativeness** | Representatividade | Cobrir variações do domínio |
| **RLHF** | RLHF | Feedback humano para alinhamento |

---

## 3.5 Bedrock — Features Detalhadas

| Feature (EN) | Feature (PT-BR) | O que faz | Cue de Prova |
|-------------|----------------|-----------|-------------|
| **Knowledge Bases** | Bases de Conhecimento | RAG gerenciado | "RAG sem gerenciar infra" |
| **Agents** | Agentes | Agentes multi-etapa com ferramentas e APIs | "agente autônomo, chamar APIs" |
| **AgentCore** | AgentCore | Produção de agentes: Runtime, Memory, Gateway, Identity, Policy, Observability | "agentes em produção, escala" |
| **AgentCore Identity** | Identidade do Agente | Gerencia identidades de agentes para acesso seguro a ferramentas | "agente com credenciais próprias" |
| **AgentCore Policy** | Política do Agente | Define e restringe quais ferramentas o agente pode chamar | "controlar o que o agente pode acessar" |
| **Guardrails** | Guardrails | Filtros de segurança, conteúdo, PII, grounding | "filtrar conteúdo", "bloquear tópico" |
| **Prompt Management** | Gerenciamento de Prompts | Versionamento e templates de prompts | "versionar prompts como código" |
| **Model Evaluation** | Avaliação de Modelos | Compara FMs com métricas automáticas, humanas ou LLM-as-a-judge | "comparar múltiplos modelos" |
| **Flows** | Fluxos | Builder visual para workflows: Prompts + KB + Lambda + Condition | "workflow GenAI visual sem código" |
| **Cross-Region Inference** | Inferência Multi-Região | Roteia para regiões alternativas quando sobrecarregado | "alta disponibilidade inferência" |

### Bedrock Guardrails — Features Detalhadas

| Feature (EN) | Feature (PT-BR) | O que faz | Cue |
|-------------|----------------|-----------|-----|
| **Content filtering** | Filtro de conteúdo | 6 categorias (ódio, violência, sexual, automutilação, insultos, ilícito), 4 níveis cada | "bloquear hate speech" |
| **Denied topics** | Tópicos negados | Tópicos customizados que o modelo recusa | "chatbot não pode discutir X" |
| **PII redaction** | Redação de PII | Detecta e mascara dados pessoais em inputs e outputs | "prevenir vazamento de dados pessoais" |
| **Word filters** | Filtros de palavras | Bloqueia palavras/frases específicas | "bloquear nome de concorrentes" |
| **Contextual grounding check** | Verificação de fundamentação contextual | Verifica se resposta é suportada pelo contexto (grounding score) e relevante (relevance score) | "detectar alucinação em RAG" |
| **Grounding score** | Score de fundamentação | Score $0\text{--}1$ — abaixo do threshold $\rightarrow$ resposta bloqueada | Cliente define o threshold |
| **Relevance score** | Score de relevância | Mede se a resposta responde à pergunta do usuário | "resposta correta mas não relevante" |
| **Automated reasoning checks** | Verificações de raciocínio automatizado | Verifica respostas contra regras formais/políticas | "verificar resposta contra política de compliance" |

---

## 3.6 Prompt Engineering (Engenharia de Prompt)

### Conceitos e Construções de Prompt

| Elemento (EN) | Elemento (PT-BR) | O que é |
|--------------|-----------------|---------|
| **Instruction** | Instrução | O que o modelo deve fazer |
| **Context** | Contexto | Informações de fundo para o modelo usar |
| **Input data** | Dados de entrada | Os dados específicos para processar |
| **Output format** | Formato de saída | Como a resposta deve ser estruturada |
| **System prompt** | Prompt de sistema | Instrução de contexto/papel antes da conversa |
| **Negative prompts** | Prompts negativos | Instrui o que o modelo NÃO deve fazer/incluir |

### Técnicas de Prompt Engineering

| Técnica (EN) | Técnica (PT-BR) | Como funciona | Quando usar |
|-------------|----------------|--------------|------------|
| **Zero-shot** | Zero-shot | Só instrução, sem exemplos | Tarefas genéricas/óbvias |
| **One-shot** | Um exemplo | 1 exemplo no prompt | Quando há 1 exemplo perfeito |
| **Few-shot** | Poucos exemplos | 3-5 exemplos no prompt | Comportamento específico não-óbvio |
| **Chain-of-thought** | Cadeia de pensamento | "Pense passo a passo antes de responder" | Matemática, lógica, múltiplas etapas |
| **Prompt templates** | Templates de prompt | Templates reutilizáveis com variáveis | Aplicações em escala |
| **ReAct** (Reason + Act) | Raciocinar + Agir | Alterna Thought $\rightarrow$ Action $\rightarrow$ Observation em loop | Base dos Bedrock Agents |
| **Self-consistency** | Auto-consistência | Gera múltiplas respostas, seleciona a mais frequente | Aumentar confiabilidade em raciocínio |
| **Meta-prompting** | Meta-prompting | O LLM gera/otimiza seus próprios prompts | Otimizar prompts automaticamente |

### Riscos de Prompt

| Risco (EN) | Risco (PT-BR) | O que é | Mitigação |
|-----------|-------------|---------|-----------|
| **Prompt injection / hijacking** | Injeção / sequestro de prompt | Instrução maliciosa embebida para desviar o modelo | Guardrails, validação de entrada |
| **Jailbreaking** | Jailbreak | Contornar restrições de segurança do modelo | Guardrails, RLHF |
| **Exposure / Leakage** | Exposição | Vazar system prompt ou dados sensíveis via resposta | Guardrails, não expor system prompt |
| **Data poisoning** | Envenenamento de dados | Dados maliciosos na base RAG contaminam respostas | Curar fontes, validar base |

### Prompt Management (Gerenciamento de Prompts — Task 3.2.5)

- **Versionamento de prompts** (*Prompt versioning*): controlar versões como código — Bedrock Prompt Management
- **Templates parametrizados** (*Parametrized templates*): prompts reutilizáveis com variáveis
- **Avaliação A/B de prompts**: testar qual prompt produz melhores resultados

### Melhores Práticas de Prompt Engineering

- Ser específico e conciso
- Definir formato de saída (JSON, lista, tabela)
- Usar exemplos quando o comportamento é não-óbvio
- Versionar e testar prompts
- Adicionar guardrails nos prompts

---

## 3.7 Avaliação de Foundation Models (Task 3.4)

### Abordagens de Avaliação

| Abordagem (EN) | Abordagem (PT-BR) | Detalhe |
|---------------|-----------------|---------|
| **Human evaluation** | Avaliação humana | Padrão-ouro, mas cara e lenta |
| **Benchmark datasets** | Datasets de benchmark | GLUE, SuperGLUE — comparação padronizada entre modelos |
| **Amazon Bedrock Model Evaluation** | Avaliação de Modelos Bedrock | Avaliação gerenciada: automática, humana ou LLM-as-a-judge |
| **LLM-as-a-judge** | LLM como avaliador | Usar um FM para avaliar saídas de outro FM — escalável |

### Métricas de Qualidade de Saída

| Métrica (EN) | Métrica (PT-BR) | Uso principal |
|-------------|----------------|--------------|
| **ROUGE** (Recall-Oriented Understudy for Gisting Evaluation) | ROUGE | **Sumarização** — sobreposição de n-gramas com referência |
| **BLEU** (Bilingual Evaluation Understudy) | BLEU | **Tradução** — sobreposição de n-gramas (precision-oriented) |
| **BERTScore** | BERTScore | **Similaridade semântica** — usa embeddings BERT, captura paráfrases |
| **Perplexity** | Perplexidade | Fluência do modelo — menor = melhor |
| **F1 Score** | F1 Score | Classificação (precision + recall) |

### Métricas de Avaliação RAG (Bedrock Model Evaluation)

| Métrica (EN) | Métrica (PT-BR) | O que mede |
|-------------|----------------|-----------|
| **Faithfulness** | Fidelidade | Resposta é suportada pelos chunks recuperados — mede alucinação no RAG |
| **Answer Relevancy** | Relevância da Resposta | Resposta responde à pergunta do usuário |
| **Context Relevance** | Relevância do Contexto | Chunks recuperados são relevantes à pergunta |
| **Context Coverage** | Cobertura do Contexto | Chunks cobrem todas as informações necessárias |
| **Correctness** | Correção | Resposta é factualmente correta vs ground truth |

### Métricas de Alinhamento com Negócio (Task 3.4.5 — V1.1)

| Métrica (EN) | Métrica (PT-BR) | O que mede |
|-------------|----------------|-----------|
| **Task completion rate** | Taxa de conclusão de tarefas | % de tarefas que o agente/modelo conclui com sucesso |
| **User satisfaction** | Satisfação do usuário | NPS, CSAT, avaliação qualitativa |
| **Cost per interaction** | Custo por interação | Custo médio por chamada/sessão |
| **Productivity** | Produtividade | Ganho de produtividade com uso da IA |
| **User engagement** | Engajamento do usuário | Frequência e qualidade das interações |

---

## 3.8 Bedrock Flows vs Agents

| Característica | Bedrock Flows | Bedrock Agents |
|----------------|--------------|---------------|
| Tipo de workflow | **Determinístico** (graph estático) | **Autônomo** (modelo decide os passos) |
| Quem define os passos | Você (visual builder) | O próprio LLM |
| Quando usar | Processo conhecido e fixo | Processo aberto, variável |
| Componentes | Prompt, KB, Agent, Guardrail, Lambda, Condition, Iterator | FM + Tools + Memory + Observation |
| Cue de prova | "workflow GenAI com lógica fixa" | "agente autônomo que decide ações" |

---
> 📂 **Navegar:** [🏠 Início (README)](README.md) | [D1 IA-ML](AIF-C01-D1-Fundamentos-IA-ML.md) | [D2 GenAI](AIF-C01-D2-Fundamentos-GenAI.md) | **[D3 FMs](AIF-C01-D3-Aplicacoes-FM.md)** | [D4 Responsável](AIF-C01-D4-IA-Responsavel.md) | [D5 Segurança](AIF-C01-D5-Seguranca-Governanca.md) | [D6 Referência](AIF-C01-D6-Referencia-Estrategia.md)
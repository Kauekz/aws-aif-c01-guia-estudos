# Domínio 5: Segurança, Conformidade e Governança para Soluções de IA (14% do exame)

Resumo técnico baseado no guia oficial AWS Certified AI Practitioner (AIF-C01) v1.2, focado em proteção de dados, controle de acesso, responsabilidade compartilhada, auditoria e governança na nuvem AWS.

---

## Tarefa 5.1: Segurança e Privacidade em Sistemas de IA

### Modelo de Responsabilidade Compartilhada na IA

* **Responsabilidade da AWS (Segurança DA Nuvem):**
  Proteger a infraestrutura física global, hardware, rede base, virtualização e garantir o isolamento dos serviços gerenciados (como a infraestrutura subjacente do Amazon Bedrock e SageMaker).
* **Responsabilidade do Cliente (Segurança NA Nuvem):**
  Qualidade e legalidade dos dados de treinamento e inferência, configuração de políticas de acesso (IAM), criptografia de dados em repouso (chaves KMS), configuração de rede privada (VPC, PrivateLink), engenharia de prompt segura e aplicação de Guardrails.

### Privacidade de Dados no Amazon Bedrock

* **Isolamento de Dados:** O Amazon Bedrock **não** usa seus prompts, respostas ou dados de customização (fine-tuning) para treinar os modelos base nem os compartilha com os provedores terceiros dos modelos (como Anthropic ou Meta).
* **Criptografia:** Dados são criptografados em trânsito (TLS) e em repouso (por padrão com chaves gerenciadas pela AWS ou chaves gerenciadas pelo cliente via **AWS KMS**).

### Principais Serviços de Segurança Aplicados a IA

* **AWS IAM (Identity and Access Management):** Controle granular de autenticação e autorização (princípio do privilégio mínimo) para definir quem ou qual serviço pode invocar modelos (`bedrock:InvokeModel`) ou acessar buckets S3 de treinamento.
* **Amazon Macie:** Utiliza Machine Learning para descobrir, classificar e proteger automaticamente dados sensíveis (PII, dados financeiros) armazenados no Amazon S3 antes que sejam enviados para treinamento ou bases de conhecimento (RAG).
* **Amazon Comprehend (PII Detection):** Identifica e mascara entidades de dados pessoais diretamente em textos em tempo real ou em lote.
* **AWS PrivateLink (VPC Endpoints):** Permite conectar sua VPC diretamente ao Amazon Bedrock ou Amazon SageMaker sem que o tráfego de dados passe pela internet pública.
* **AWS KMS (Key Management Service):** Criação e controle de chaves criptográficas para proteger volumes de armazenamento do SageMaker, buckets S3 e trabalhos de customização no Bedrock.

### Ameaças Específicas a Sistemas de IA

* **Prompt Injection (Injeção de Prompt):** Manipulação da entrada pelo usuário para tentar ignorar as instruções originais do sistema (*jailbreak*) ou extrair informações confidenciais.
* **Data Poisoning (Envenenamento de Dados):** Inserção maliciosa de dados adulterados ou tendenciosos no conjunto de treinamento ou na base do RAG para comprometer o comportamento futuro do modelo.
* **Data Exfiltration / Model Inversion:** Tentativas de reconstruir dados confidenciais de treinamento a partir das respostas do modelo.

---

## Tarefa 5.2: Governança e Conformidade para Sistemas de IA

### Auditoria, Rastreabilidade e Monitoramento

* **AWS CloudTrail:** Registra todas as chamadas de API feitas na conta AWS (quem chamou qual API, quando e de onde). Fundamental para auditoria de segurança e conformidade.
* **Amazon CloudWatch:** Monitora métricas de performance e logs operacionais (como latência de invocação de modelos, quantidade de tokens consumidos e erros de execução no Bedrock/SageMaker).
* **Model Invocation Logging (Amazon Bedrock):** Recurso que permite registrar os metadados, prompts de entrada e respostas geradas pelos modelos diretamente no Amazon S3 ou CloudWatch Logs para fins de auditoria (desativado por padrão por questões de privacidade).

### Serviços de Conformidade e Governança

* **AWS Artifact:** Portal sob demanda que fornece acesso a relatórios de conformidade e certificações da AWS (ISO, PCI DSS, SOC) para validação por auditores.
* **AWS Audit Manager:** Ajuda a auditar continuamente o uso da AWS e automatizar a coleta de evidências para avaliar riscos e conformidade com regulamentos e políticas internas.
* **AWS Config:** Avalia, audita e monitora continuamente as configurações dos recursos da AWS (ex.: verificar se um bucket S3 usado para IA está público ou sem criptografia).
* **Amazon SageMaker Model Registry:** Catálogo central para gerenciar versões de modelos em produção, rastrear metadados de linhagem, aprovar ou rejeitar modelos para deploy e manter governança sobre o ciclo de vida de ML.
* **Amazon SageMaker Lineage Tracking:** Cria e armazena informações sobre as etapas de um fluxo de trabalho de ML (dados usados, parâmetros, artefatos), permitindo reproduzir modelos e realizar auditorias de rastreabilidade.

---

## Resumo Rápido para Prova (Pegadinhas Comuns)

* **Descobrir PII automaticamente em buckets do Amazon S3 antes de treinar um modelo?** -> **Amazon Macie**.
* **Garantir que o tráfego entre sua aplicação e o Amazon Bedrock não passe pela internet pública?** -> **AWS PrivateLink** (Interface VPC Endpoint).
* **Auditar quem fez uma chamada de API no Bedrock ou SageMaker?** -> **AWS CloudTrail**.
* **Baixar relatórios de conformidade (ISO, SOC, PCI) da própria AWS?** -> **AWS Artifact**.
* **Automatizar coleta de evidências para auditorias internas ou regulatórias?** -> **AWS Audit Manager**.
* **Controlar versão e aprovação de modelos antes de irem para produção?** -> **SageMaker Model Registry**.
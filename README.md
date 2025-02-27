# Engenheiro-MLOps-GCP

# Objetivo  
Avaliar o conhecimento e a experiência do candidato em MLOps com foco na Google Cloud Platform (GCP), cobrindo automação, orquestração, escalabilidade, segurança e monitoramento.  

## Seção 1: Conceitos e Arquitetura (Questões Teóricas)  

### 1. Infraestrutura e Orquestração  
- Qual a diferença entre Vertex AI Pipelines e Kubeflow Pipelines na GCP? Quando escolher um em vez do outro?
  
#### 📌 Vertex AI Pipelines vs. Kubeflow Pipelines (KFP) na GCP

##### 🌟 Vertex AI Pipelines
✅ **Gerenciado pela GCP** → Sem necessidade de gerenciar Kubernetes  
✅ **Integração nativa** com Vertex AI, IAM, Logging  
✅ **Segurança aprimorada** com IAM  
✅ **Foco no desenvolvimento** sem sobrecarga operacional  

📍 **Quando escolher?**  
- Se quer uma solução **pronta e fácil** de usar  
- Se já usa **Vertex AI**  
- Se **não quer gerenciar Kubernetes**  

---

##### 🛠️ Kubeflow Pipelines no GKE
✅ **Autogerenciado no Kubernetes** (GKE)  
✅ **Mais flexível** e personalizável  
✅ **Menor custo** para workloads grandes  
✅ **Possível uso híbrido/multicloud**  

📍 **Quando escolher?**  
- Se precisa de **controle total sobre a infraestrutura**  
- Se já tem **expertise em Kubernetes**  
- Se quer **rodar workloads híbridos**  

---

##### 🔥 Comparação rápida

| Característica          | **Vertex AI Pipelines** | **Kubeflow Pipelines (GKE)** |
|------------------------|-----------------------|-----------------------------|
| **Gerenciamento**      | Automático (GCP)      | Manual (Kubernetes)        |
| **Infraestrutura**     | Oculta                | GKE gerenciado pelo usuário |
| **Integração GCP**     | Total (Vertex AI, IAM, Logging) | Parcial |
| **Flexibilidade**      | Menor                  | Alta (customizável)        |
| **Escalabilidade**     | Automática             | Controlada pelo usuário    |
| **Segurança (IAM)**    | Integrada com GCP      | Definida pelo usuário      |
| **Custo**              | Paga conforme uso      | Pode ser mais barato em alto volume |

##### 🚀 **Recomendação**
- **Vertex AI Pipelines** → Para produtividade, facilidade e integração com GCP  
- **Kubeflow Pipelines (GKE)** → Para flexibilidade, personalização e workloads híbridos  
  
- Explique como você estruturaria uma infraestrutura escalável para treinar e servir modelos de ML na GCP.
  #### 🚀 Infraestrutura Escalável para ML na GCP

##### 🔹 **Arquitetura Geral**
A infraestrutura deve permitir **treinamento escalável**, **armazenamento eficiente**, **serviço de inferência otimizado** e **monitoramento contínuo**.  

---

##### 🔥 **1. Treinamento Escalável**
##### ✅ **Gerenciamento de Dados**
- **Cloud Storage (GCS)** → Armazena datasets grandes  
- **BigQuery** → Para análise e manipulação de dados estruturados  
- **Feature Store (Vertex AI)** → Gerencia features reutilizáveis  

##### ✅ **Treinamento Distribuído**
- **Vertex AI Training** → Escalável, suporta GPUs/TPUs  
- **Dataflow** → Para pré-processamento distribuído  
- **Kubeflow Pipelines** / **Vertex AI Pipelines** → Automação de workflows  

##### ✅ **Gerenciamento de Experimentos**
- **Vertex AI Experiments** → Rastreamento automático  
- **MLflow** (Self-hosted no GKE) → Alternativa customizável  

---

##### ⚡ **2. Implantação e Servir Modelos**
##### ✅ **Opções de Deployment**
- **Vertex AI Endpoints** → Modelo gerenciado, autoescalável  
- **Cloud Run** → Para modelos leves via API  
- **GKE (Kubernetes Engine)** → Para inferência customizada e de alto volume  

##### ✅ **Otimização de Inferência**
- **Vertex AI Prediction** → Autoescalável, otimizado para GPUs/TPUs  
- **TF Serving / TorchServe no GKE** → Para arquiteturas customizadas  
- **Redis / Memorystore** → Cache para previsões frequentes  

---

##### 📊 **3. Monitoramento e Observabilidade**
- **Vertex AI Model Monitoring** → Detecta drift de dados  
- **Cloud Logging & Monitoring** → Para logs e métricas  
- **Prometheus + Grafana (GKE)** → Para monitoramento customizado  

---

##### 🎯 **Resumo da Infraestrutura**
| Componente         | Tecnologia (GCP)                        |
|--------------------|----------------------------------------|
| **Armazenamento**  | Cloud Storage, BigQuery, Feature Store |
| **Treinamento**    | Vertex AI Training, Dataflow, Pipelines |
| **Serviço de ML**  | Vertex AI Endpoints, Cloud Run, GKE     |
| **Monitoramento**  | Model Monitoring, Logging, Prometheus  |

##### 🚀 **Conclusão**
- Para **simplicidade e escalabilidade**, use **Vertex AI**.  
- Para **customização**, use **GKE + Kubeflow**.  
- Para **inferência otimizada**, combine **GPU/TPU + caching**.  

### 2. CI/CD para Machine Learning  
- Como você implementaria uma pipeline CI/CD para modelos de ML na GCP utilizando Cloud Build, Vertex AI e Terraform?
  #### Resposta: 🚀 CI/CD para Modelos de ML na GCP com Cloud Build, Vertex AI e Terraform

Uma **pipeline CI/CD** para modelos de ML na GCP precisa automatizar **treinamento, validação, implantação e monitoramento**. Abaixo está uma estrutura escalável usando **Cloud Build**, **Vertex AI** e **Terraform**.

---

##### 📌 **1. Estrutura da Pipeline**
##### ✅ **Infraestrutura como Código (IaC)**
- **Terraform** → Provisiona os recursos na GCP (**Bucket, Vertex AI, IAM, GKE, etc.**)

##### ✅ **Treinamento e Validação**
- **Cloud Build** → Executa pipelines de ML  
- **Vertex AI Training** → Treinamento distribuído (GPUs/TPUs)  
- **Cloud Storage** → Armazena datasets e artefatos  
- **Vertex AI Experiments** → Registro de experimentos  

##### ✅ **Implantação e Monitoramento**
- **Cloud Build + Vertex AI Endpoints** → Servir modelos  
- **Cloud Run** → Alternativa para API leve  
- **Vertex AI Model Monitoring** → Detecta drift de dados  
- **Cloud Logging & Monitoring** → Coleta logs e métricas  

---

##### 🔥 **2. Fluxo da Pipeline**
```bash
graph TD;
  DevOps["👨‍💻 Dev/ML Engineer"] -->|Code Commit| GitHub/GitLab
  GitHub/GitLab -->|Trigger| Cloud Build
  Cloud Build -->|Terraform Apply| GCP Infra
  Cloud Build -->|Train Model| Vertex AI Training
  Vertex AI Training -->|Store Artifacts| Cloud Storage
  Cloud Build -->|Validate Model| Vertex AI Experiments
  Vertex AI Experiments -->|Pass? Yes| Deploy
  Deploy -->|Vertex AI Endpoints| Serving
  Deploy -->|Cloud Run| API (Alternative)
  Serving -->|Monitor| Vertex AI Model Monitoring
  Serving -->|Logs| Cloud Logging
```
- Explique como gerenciar versionamento de modelos no Vertex AI Model Registry e como reverter um modelo para uma versão anterior.
#### 📌 Gerenciamento de Versionamento de Modelos no Vertex AI Model Registry

O **Vertex AI Model Registry** permite armazenar, versionar e gerenciar modelos de ML na GCP, facilitando controle de versões e rollback.

---

##### 🔹 **1. Como Versionar um Modelo no Vertex AI**
Cada vez que um modelo é atualizado, o Vertex AI cria uma **nova versão** dentro do mesmo registro.

##### ✅ **Registrar um Novo Modelo**
```bash
gcloud ai models upload \
  --region=us-central1 \
  --display-name=my-model \
  --artifact-uri=gs://ml-models-bucket/model-v1 \
  --container-image-uri=gcr.io/cloud-aiplatform/prediction/tf2-cpu
```
Isso cria version 1 do modelo.

```bash
gcloud ai models upload \
  --region=us-central1 \
  --display-name=my-model \
  --version-aliases=v2 \
  --artifact-uri=gs://ml-models-bucket/model-v2
```
Isso adiciona a version 2 ao modelo existente.

Para visualizar todas as versões registradas:
```bash
gcloud ai models list --region=us-central1
```

Para ver detalhes de um modelo específico:
```bash
gcloud ai models describe my-model --region=us-central1
```

Caso a nova versão tenha problemas, é possível reverter para uma versão estável.
Desativar a versão problemática (exemplo: version 2):
```bash
gcloud ai models versions delete v2 \
  --model=my-model \
  --region=us-central1
```

Reimplantar uma versão anterior (exemplo: version 1):
```bash
gcloud ai endpoints deploy-model \
  --model=my-model \
  --deployed-model-display-name=my-model-v1 \
  --region=us-central1 \
  --traffic-split=0=100
```
### 3. Monitoramento e Observabilidade  
- Como monitorar um modelo de ML em produção na GCP para detectar desvio de conceito (concept drift)?
  #### 📌 Monitoramento de Desvio de Conceito (Concept Drift) na GCP

Para monitorar um modelo de ML em produção na GCP e detectar **desvio de conceito (concept drift)**, há duas abordagens principais que eu usaria:

---

##### 🔹 **1. Usando Evidently**
O **Evidently** é uma ferramenta de código aberto que facilita a detecção de **drift de dados e modelo**. Ele permite realizar análises de drift de forma contínua e oferece relatórios automáticos.

##### ✅ **Configuração com Evidently:**
- **Integração com GCP**: Pode ser configurado para rodar em notebooks ou servidores no GKE.
- **Monitoramento contínuo**: O Evidently permite gerar relatórios sobre drift de conceito, drift de dados e performance do modelo.
- **Notificações**: Pode ser configurado para enviar alertas quando o drift ultrapassa um limiar pré-definido.

```python
import evidently
from evidently.dashboard import Dashboard
from evidently.dashboard.tabs import DataDriftTab
```

# Criar dashboard
dashboard = Dashboard(tabs=[DataDriftTab()])
dashboard.calculate(reference_data, production_data)

# Gerar relatório de drift
dashboard.save("drift_report.html")

   
- Quais métricas-chave você acompanharia para garantir a performance e confiabilidade de um modelo implantado no Vertex AI?
#### 📌 Métricas-Chave para Garantir a Performance e Confiabilidade de um Modelo no Vertex AI

Para garantir que um modelo implantado no **Vertex AI** esteja performando de forma adequada e confiável, é fundamental acompanhar diversas métricas que abordam tanto a **performance do modelo** quanto a **confiabilidade da operação**.

---

##### 🔹 **1. Métricas de Performance do Modelo**
Essas métricas medem a qualidade e a precisão das previsões feitas pelo modelo.

##### ✅ **Acurácia (Accuracy)**
- Mede a proporção de previsões corretas em relação ao total de previsões.  
- **Importante para problemas de classificação**.

##### ✅ **Precisão e Recall**
- **Precisão (Precision)**: Proporção de previsões positivas corretas.
- **Recall (Sensibilidade)**: Proporção de casos positivos reais corretamente identificados.
- **F1-Score**: Média harmônica entre precisão e recall, especialmente útil para dados desbalanceados.

##### ✅ **AUC-ROC e AUC-PR**
- **AUC-ROC**: Avalia a capacidade do modelo de classificar corretamente entre as classes.
- **AUC-PR**: Avaliação mais robusta em datasets desbalanceados, medindo o desempenho de forma mais sensível ao desbalanceamento de classes.

##### ✅ **Métricas de Regressão (para modelos de regressão)**
- **Erro Absoluto Médio (MAE)**: Diferença média entre os valores previstos e reais.
- **Erro Quadrático Médio (MSE)**: Penaliza mais fortemente os erros maiores.
- **R² (Coeficiente de Determinação)**: Mede a qualidade da previsão em relação à variabilidade dos dados.

---

##### 🔹 **2. Métricas de Confiabilidade e Monitoramento Operacional**
Essas métricas são fundamentais para garantir a **estabilidade e confiabilidade** do modelo em produção.

##### ✅ **Drift de Dados e Conceito (Concept Drift)**
- **Monitoramento de drift** para detectar mudanças nos dados de entrada e na relação entre variáveis ao longo do tempo. Isso ajuda a identificar quando o modelo precisa ser retrainado.

##### ✅ **Latency (Latência)**
- **Tempo de resposta do modelo** para realizar uma previsão. A latência é importante em sistemas que exigem respostas rápidas, como em produção de tempo real.

##### ✅ **Throughput**
- **Quantidade de previsões feitas por unidade de tempo**. Essa métrica ajuda a garantir que o modelo consiga lidar com a carga de trabalho esperada sem degradar o desempenho.

##### ✅ **Utilização de Recursos**
- **Uso de CPU/GPU e Memória**: Monitorar o uso de recursos ajuda a garantir que o modelo esteja operando de forma eficiente e não está consumindo recursos excessivos, o que poderia impactar outros serviços.

---

##### 🔹 **3. Métricas de Confiabilidade do Modelo em Produção**
Essas métricas ajudam a garantir que o modelo esteja funcionando corretamente ao longo do tempo.

##### ✅ **Taxa de Erro e Falhas**
- **Monitoramento de falhas**: Acompanhar a **taxa de erros** no modelo e se o serviço de previsão está disponível sem falhas (erros 500 ou falhas de resposta).
  
##### ✅ **Acuracidade do Modelo em Produção**
- Medir a **performance contínua** do modelo com dados reais. A performance pode degradar com o tempo devido a mudanças nos dados ou no ambiente de produção.

---

##### 🎯 **Conclusão**
Para garantir a **performance e confiabilidade** de um modelo no Vertex AI, é importante monitorar tanto **métricas de performance** como **métricas operacionais**. Isso inclui:

- **Performance do modelo**: Acurácia, F1-Score, AUC-ROC, entre outras.
- **Desempenho operacional**: Latência, throughput, uso de recursos.
- **Monitoramento de drift**: Detecção de mudanças nos dados e comportamento do modelo.
  
Essas métricas ajudam a garantir que o modelo permaneça eficiente, preciso e estável ao longo do tempo.

#### 4. Segurança e Compliance  
- Como garantir a segurança e privacidade dos dados ao treinar modelos na GCP? Quais serviços da GCP você utilizaria?
##### 📌 Garantindo Segurança e Privacidade dos Dados ao Treinar Modelos na GCP

Ao treinar modelos de machine learning (ML) na **Google Cloud Platform (GCP)**, é fundamental implementar boas práticas de segurança e privacidade para proteger os dados sensíveis. A GCP oferece uma série de ferramentas e serviços que podem ser usados para garantir a **proteção de dados** e o **cumprimento de regulamentos** de privacidade.

---

##### 🔹 **1. Criptografia de Dados**
##### ✅ **Criptografia em Trânsito e em Repouso**
- **Criptografia em Trânsito**: A GCP garante que todos os dados sejam criptografados enquanto são transferidos entre os serviços usando protocolos como TLS.
- **Criptografia em Repouso**: Todos os dados armazenados, como dados de treinamento ou modelos, são criptografados automaticamente com **Google-managed keys** ou **Customer-managed keys (CMEK)**.

##### ✅ **Cloud Key Management (KMS)**
- O **Cloud KMS** permite a criação e gerenciamento de chaves de criptografia personalizadas para controlar o acesso aos dados sensíveis de forma granular.

---

##### 🔹 **2. Controle de Acesso e Identidade**
##### ✅ **Identity and Access Management (IAM)**
- **IAM** permite gerenciar quem tem acesso aos recursos da GCP e o que eles podem fazer. É possível definir permissões específicas para usuários, grupos e serviços.
  
##### ✅ **VPC Service Controls**
- O **VPC Service Controls** cria perímetros de segurança em torno de recursos, restringindo o acesso a dados críticos e impedindo exfiltração de dados de forma inadvertida.

##### ✅ **Google Cloud Identity**
- Gerencia identidades e autenticação de usuários. Permite um controle centralizado sobre quem pode acessar os recursos e dados sensíveis.

---

##### 🔹 **3. Proteção de Dados Pessoais (Privacy)**
##### ✅ **Data Loss Prevention (DLP)**
- O **Cloud DLP** ajuda a identificar, classificar e proteger dados pessoais sensíveis (como informações de cartão de crédito ou CPF) em tempo de execução. Você pode usar o DLP para fazer uma auditoria e aplicar regras de anonimização nos dados antes de usá-los para treinamento.

##### ✅ **Confidential Computing**
- A **Confidential VMs** e **Confidential GKE Nodes** permitem processar dados sensíveis enquanto os mantém criptografados durante o processamento. Isso oferece proteção adicional para modelos que precisam manipular dados confidenciais.

---

##### 🔹 **4. Monitoramento e Auditoria**
##### ✅ **Cloud Audit Logs**
- **Cloud Audit Logs** registra todas as ações feitas na GCP, proporcionando um histórico completo de quem fez o quê e quando. Isso é essencial para auditorias de segurança e monitoramento de acesso.

##### ✅ **Cloud Security Command Center**
- O **Cloud Security Command Center** oferece uma visão geral da segurança dos seus recursos e pode identificar vulnerabilidades, configurações incorretas e outras ameaças potenciais.

---

##### 🔹 **5. Gerenciamento de Dados de Treinamento**
##### ✅ **BigQuery e Dataflow**
- **BigQuery** permite analisar grandes volumes de dados enquanto mantém as práticas de segurança e compliance, como criptografia e controle de acesso. 
- **Dataflow** pode ser usado para processar dados de forma segura e eficiente, com opções de criptografia em trânsito e em repouso.

##### ✅ **Vertex AI Workbench**
- Quando treinando modelos no **Vertex AI Workbench**, é possível configurar a segurança em torno dos notebooks, utilizando **IAM** para controle de acesso e criptografia de dados sensíveis.

---

##### 🔹 **6. Proteção Contra Ataques e Desastres**
##### ✅ **Cloud Armor**
- **Cloud Armor** oferece proteção contra ataques DDoS, garantindo que seus recursos na GCP permaneçam disponíveis e seguros.

##### ✅ **Cloud Storage**
- **Cloud Storage** oferece controle granular de acesso aos dados, além de backup e recuperação, para garantir que os dados de treinamento estejam protegidos contra falhas e desastres.

---

##### 🎯 **Conclusão**
Para garantir a **segurança** e a **privacidade** dos dados ao treinar modelos na GCP, você pode usar uma combinação dos seguintes serviços:

- **Criptografia**: GCP KMS, Cloud DLP, Criptografia em Trânsito e Repouso.
- **Controle de Acesso**: IAM, VPC Service Controls, Cloud Identity.
- **Proteção de Dados Sensíveis**: Cloud DLP, Confidential Computing.
- **Monitoramento e Auditoria**: Cloud Audit Logs, Cloud Security Command Center.
- **Gerenciamento de Dados de Treinamento**: BigQuery, Dataflow, Vertex AI Workbench.
- **Proteção Contra Ataques**: Cloud Armor, Cloud Storage.

Com esses serviços e boas práticas, você pode garantir que seus dados e modelos de ML estejam **seguros**, **conformes** e protegidos contra acessos não autorizados ou uso indevido.
 
- Quais práticas de controle de acesso você aplicaria para proteger pipelines de treinamento e inferência na GCP?
  #### 📌 Práticas de Controle de Acesso para Proteger Pipelines de Treinamento e Inferência na GCP

Proteger as **pipelines de treinamento** e **inferência** na **Google Cloud Platform (GCP)** exige a implementação de um controle de acesso rigoroso. A seguir, explico as práticas de controle de acesso que devem ser aplicadas para proteger esses pipelines e garantir que apenas usuários ou sistemas autorizados possam interagir com os dados e modelos.

---

##### 🔹 **1. Uso do IAM (Identity and Access Management)**
##### ✅ **Princípios de Menor Privilégio**
- Configure permissões para garantir que os usuários e sistemas tenham apenas as permissões necessárias para executar suas tarefas, sem acesso a recursos adicionais.
  
##### ✅ **Criação de Papéis Personalizados**
- Crie **papéis personalizados** no IAM para conceder permissões específicas para diferentes componentes das pipelines, como:
  - **Treinamento**: Acesso apenas a recursos de treinamento e modelos.
  - **Inferência**: Acesso restrito a modelos implantados, sem acesso a dados sensíveis.
  - **Gestores de Modelos**: Permissão para visualizar, versionar e reverter modelos.

##### ✅ **Política de Acesso Baseada em Funções (RBAC)**
- Defina **funções específicas** para diferentes equipes, como Cientistas de Dados, Engenheiros de Dados e Administradores de GCP, com permissões bem delimitadas para interagir com recursos como **Cloud Storage**, **Vertex AI**, e **BigQuery**.

---

##### 🔹 **2. Controle de Acesso para Pipelines de Treinamento**
##### ✅ **Controle de Acesso a Dados Sensíveis**
- Utilize **VPC Service Controls** para restringir o acesso aos dados e garantir que apenas usuários ou serviços dentro de uma rede segura possam interagir com dados sensíveis durante o treinamento.

##### ✅ **Controle de Acesso ao Vertex AI**
- No **Vertex AI**, crie **papéis específicos** para os pipelines de treinamento, como:
  - **Treinamento de Modelos**: Permissão para iniciar e gerenciar o processo de treinamento de modelos.
  - **Administração de Pipelines**: Permissão para configurar e monitorar pipelines.
  
##### ✅ **Gerenciamento de Chaves de Criptografia (CMEK)**
- Utilize **Customer-Managed Encryption Keys (CMEK)** para garantir que somente usuários com permissão possam descriptografar dados enquanto os pipelines de treinamento estão em execução.

---

##### 🔹 **3. Controle de Acesso para Inferência**
##### ✅ **Controle de Acesso a Modelos Implantados**
- **IAM** no Vertex AI pode ser configurado para controlar o acesso a modelos implantados:
  - **Inferência**: Permite apenas que usuários ou sistemas autorizados façam chamadas de inferência no modelo.
  - **Monitoramento e Auditoria**: Permite que a equipe de DevOps ou Segurança visualize logs de inferência e monitore possíveis problemas de segurança.

##### ✅ **Autenticação e Autorização para API de Inferência**
- Configure autenticação para APIs de inferência utilizando **Service Accounts**. Isso garante que apenas usuários ou sistemas autenticados possam realizar requisições para modelos de produção.

---

##### 🔹 **4. Controle de Acesso com Redes e VPC**
##### ✅ **VPC Service Controls**
- Utilize **VPC Service Controls** para restringir a comunicação entre diferentes serviços da GCP e evitar a exfiltração de dados de maneira inadvertida, garantindo que apenas usuários ou sistemas com a permissão correta possam acessar os dados e modelos em pipelines de treinamento e inferência.

### ✅ **Segurança de Rede com Firewalls**
- Configure **firewalls** para limitar o tráfego entre diferentes instâncias e serviços, permitindo acesso apenas de fontes confiáveis e com autenticação adequada.

---

##### 🔹 **5. Monitoramento e Auditoria**
##### ✅ **Cloud Audit Logs**
- Use **Cloud Audit Logs** para registrar todas as ações realizadas nas pipelines de treinamento e inferência. Isso permite uma **auditoria completa** e a detecção de qualquer acesso não autorizado ou atividade suspeita.

##### ✅ **Cloud Security Command Center**
- Utilize o **Security Command Center** para monitorar as configurações de segurança e detectar riscos, como configurações incorretas ou acessos não autorizados a pipelines e modelos.

---

##### 🎯 **Conclusão**
Aplicar um controle de acesso robusto para pipelines de **treinamento** e **inferência** na GCP envolve:

1. **IAM**: Criar papéis personalizados e seguir o princípio de menor privilégio.
2. **Controle de Acesso a Dados e Modelos**: Usar VPC Service Controls, chaves de criptografia personalizadas (CMEK) e controle de acesso ao Vertex AI.
3. **Redes e VPC**: Restringir o acesso com **firewalls** e **VPC Service Controls**.
4. **Monitoramento**: Usar **Cloud Audit Logs** e o **Cloud Security Command Center** para garantir a segurança.

Essas práticas asseguram que suas pipelines de ML estejam seguras e protegidas contra acessos não autorizados.


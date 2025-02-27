# Engenheiro-MLOps-GCP

# Objetivo  
Avaliar o conhecimento e a experiência do candidato em MLOps com foco na Google Cloud Platform (GCP), cobrindo automação, orquestração, escalabilidade, segurança e monitoramento.  

## Seção 1: Conceitos e Arquitetura (Questões Teóricas)  

### 1. Infraestrutura e Orquestração  
- Qual a diferença entre Vertex AI Pipelines e Kubeflow Pipelines na GCP? Quando escolher um em vez do outro?
  
# Resposta: 📌 Vertex AI Pipelines vs. Kubeflow Pipelines (KFP) na GCP

## 🌟 Vertex AI Pipelines
✅ **Gerenciado pela GCP** → Sem necessidade de gerenciar Kubernetes  
✅ **Integração nativa** com Vertex AI, IAM, Logging  
✅ **Segurança aprimorada** com IAM  
✅ **Foco no desenvolvimento** sem sobrecarga operacional  

📍 **Quando escolher?**  
- Se quer uma solução **pronta e fácil** de usar  
- Se já usa **Vertex AI**  
- Se **não quer gerenciar Kubernetes**  

---

## 🛠️ Kubeflow Pipelines no GKE
✅ **Autogerenciado no Kubernetes** (GKE)  
✅ **Mais flexível** e personalizável  
✅ **Menor custo** para workloads grandes  
✅ **Possível uso híbrido/multicloud**  

📍 **Quando escolher?**  
- Se precisa de **controle total sobre a infraestrutura**  
- Se já tem **expertise em Kubernetes**  
- Se quer **rodar workloads híbridos**  

---

## 🔥 Comparação rápida

| Característica          | **Vertex AI Pipelines** | **Kubeflow Pipelines (GKE)** |
|------------------------|-----------------------|-----------------------------|
| **Gerenciamento**      | Automático (GCP)      | Manual (Kubernetes)        |
| **Infraestrutura**     | Oculta                | GKE gerenciado pelo usuário |
| **Integração GCP**     | Total (Vertex AI, IAM, Logging) | Parcial |
| **Flexibilidade**      | Menor                  | Alta (customizável)        |
| **Escalabilidade**     | Automática             | Controlada pelo usuário    |
| **Segurança (IAM)**    | Integrada com GCP      | Definida pelo usuário      |
| **Custo**              | Paga conforme uso      | Pode ser mais barato em alto volume |

### 🚀 **Recomendação**
- **Vertex AI Pipelines** → Para produtividade, facilidade e integração com GCP  
- **Kubeflow Pipelines (GKE)** → Para flexibilidade, personalização e workloads híbridos  
  
- Explique como você estruturaria uma infraestrutura escalável para treinar e servir modelos de ML na GCP.
  # Resposta: 🚀 Infraestrutura Escalável para ML na GCP

## 🔹 **Arquitetura Geral**
A infraestrutura deve permitir **treinamento escalável**, **armazenamento eficiente**, **serviço de inferência otimizado** e **monitoramento contínuo**.  

---

## 🔥 **1. Treinamento Escalável**
### ✅ **Gerenciamento de Dados**
- **Cloud Storage (GCS)** → Armazena datasets grandes  
- **BigQuery** → Para análise e manipulação de dados estruturados  
- **Feature Store (Vertex AI)** → Gerencia features reutilizáveis  

### ✅ **Treinamento Distribuído**
- **Vertex AI Training** → Escalável, suporta GPUs/TPUs  
- **Dataflow** → Para pré-processamento distribuído  
- **Kubeflow Pipelines** / **Vertex AI Pipelines** → Automação de workflows  

### ✅ **Gerenciamento de Experimentos**
- **Vertex AI Experiments** → Rastreamento automático  
- **MLflow** (Self-hosted no GKE) → Alternativa customizável  

---

## ⚡ **2. Implantação e Servir Modelos**
### ✅ **Opções de Deployment**
- **Vertex AI Endpoints** → Modelo gerenciado, autoescalável  
- **Cloud Run** → Para modelos leves via API  
- **GKE (Kubernetes Engine)** → Para inferência customizada e de alto volume  

### ✅ **Otimização de Inferência**
- **Vertex AI Prediction** → Autoescalável, otimizado para GPUs/TPUs  
- **TF Serving / TorchServe no GKE** → Para arquiteturas customizadas  
- **Redis / Memorystore** → Cache para previsões frequentes  

---

## 📊 **3. Monitoramento e Observabilidade**
- **Vertex AI Model Monitoring** → Detecta drift de dados  
- **Cloud Logging & Monitoring** → Para logs e métricas  
- **Prometheus + Grafana (GKE)** → Para monitoramento customizado  

---

## 🎯 **Resumo da Infraestrutura**
| Componente         | Tecnologia (GCP)                        |
|--------------------|----------------------------------------|
| **Armazenamento**  | Cloud Storage, BigQuery, Feature Store |
| **Treinamento**    | Vertex AI Training, Dataflow, Pipelines |
| **Serviço de ML**  | Vertex AI Endpoints, Cloud Run, GKE     |
| **Monitoramento**  | Model Monitoring, Logging, Prometheus  |

### 🚀 **Conclusão**
- Para **simplicidade e escalabilidade**, use **Vertex AI**.  
- Para **customização**, use **GKE + Kubeflow**.  
- Para **inferência otimizada**, combine **GPU/TPU + caching**.  

### 2. CI/CD para Machine Learning  
- Como você implementaria uma pipeline CI/CD para modelos de ML na GCP utilizando Cloud Build, Vertex AI e Terraform?
  # Resposta: 🚀 CI/CD para Modelos de ML na GCP com Cloud Build, Vertex AI e Terraform

Uma **pipeline CI/CD** para modelos de ML na GCP precisa automatizar **treinamento, validação, implantação e monitoramento**. Abaixo está uma estrutura escalável usando **Cloud Build**, **Vertex AI** e **Terraform**.

---

## 📌 **1. Estrutura da Pipeline**
### ✅ **Infraestrutura como Código (IaC)**
- **Terraform** → Provisiona os recursos na GCP (**Bucket, Vertex AI, IAM, GKE, etc.**)

### ✅ **Treinamento e Validação**
- **Cloud Build** → Executa pipelines de ML  
- **Vertex AI Training** → Treinamento distribuído (GPUs/TPUs)  
- **Cloud Storage** → Armazena datasets e artefatos  
- **Vertex AI Experiments** → Registro de experimentos  

### ✅ **Implantação e Monitoramento**
- **Cloud Build + Vertex AI Endpoints** → Servir modelos  
- **Cloud Run** → Alternativa para API leve  
- **Vertex AI Model Monitoring** → Detecta drift de dados  
- **Cloud Logging & Monitoring** → Coleta logs e métricas  

---

## 🔥 **2. Fluxo da Pipeline**
```mermaid
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
# Resposta: 📌 Gerenciamento de Versionamento de Modelos no Vertex AI Model Registry

O **Vertex AI Model Registry** permite armazenar, versionar e gerenciar modelos de ML na GCP, facilitando controle de versões e rollback.

---

## 🔹 **1. Como Versionar um Modelo no Vertex AI**
Cada vez que um modelo é atualizado, o Vertex AI cria uma **nova versão** dentro do mesmo registro.

### ✅ **Registrar um Novo Modelo**
```bash
gcloud ai models upload \
  --region=us-central1 \
  --display-name=my-model \
  --artifact-uri=gs://ml-models-bucket/model-v1 \
  --container-image-uri=gcr.io/cloud-aiplatform/prediction/tf2-cpu
```
Isso cria version 1 do modelo.

gcloud ai models upload \
  --region=us-central1 \
  --display-name=my-model \
  --version-aliases=v2 \
  --artifact-uri=gs://ml-models-bucket/model-v2
Isso adiciona a version 2 ao modelo existente.

Para visualizar todas as versões registradas:
gcloud ai models list --region=us-central1

Para ver detalhes de um modelo específico:
gcloud ai models describe my-model --region=us-central1

Caso a nova versão tenha problemas, é possível reverter para uma versão estável.
Desativar a versão problemática (exemplo: version 2):

gcloud ai models versions delete v2 \
  --model=my-model \
  --region=us-central1

Reimplantar uma versão anterior (exemplo: version 1):
gcloud ai endpoints deploy-model \
  --model=my-model \
  --deployed-model-display-name=my-model-v1 \
  --region=us-central1 \
  --traffic-split=0=100

### 3. Monitoramento e Observabilidade  
- Como monitorar um modelo de ML em produção na GCP para detectar desvio de conceito (concept drift)?  
- Quais métricas-chave você acompanharia para garantir a performance e confiabilidade de um modelo implantado no Vertex AI?  

### 4. Segurança e Compliance  
- Como garantir a segurança e privacidade dos dados ao treinar modelos na GCP? Quais serviços da GCP você utilizaria?  
- Quais práticas de controle de acesso você aplicaria para proteger pipelines de treinamento e inferência na GCP?  

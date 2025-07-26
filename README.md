# 🏗️ HumanGov Infrastructure

Infraestrutura multi-tenant e reutilizável na AWS, implementada com Terraform, focada em aplicações no modelo SaaS.

---

## 📌 Visão Geral

Este projeto implementa uma base de infraestrutura moderna para aplicações SaaS que precisam atender múltiplos clientes (tenants), mantendo seus dados e recursos isolados.

A estrutura é modular, segura e fácil de replicar. Tudo é gerenciado por código (IaC), utilizando Terraform e armazenado de forma segura no GitHub.

---

## 🧱 Componentes Criados por Tenant

Para cada cliente, o Terraform provisiona automaticamente:

- 🖥️ **Instância EC2** para executar a aplicação
- 📁 **Bucket S3** exclusivo para armazenar dados
- 🗂️ **Tabela DynamoDB** com partição por tenant
- 🔐 **IAM Roles e Policies** com acesso restrito

---

## 📂 Estrutura do Projeto

```

human-gov-infrastructure/
├── main.tf
├── variables.tf
├── outputs.tf
├── backend.tf
├── modules/
│   ├── ec2/
│   ├── s3/
│   ├── dynamodb/
│   └── iam/
└── tenants/
├── tenant1.tfvars
└── tenant2.tfvars

````

- `modules/`: módulos reutilizáveis para cada tipo de recurso
- `main.tf`: módulo raiz que orquestra os recursos
- `tenants/*.tfvars`: arquivos com variáveis específicas de cada cliente

---

## 🔐 Segurança e Backend

- O estado do Terraform (`terraform.tfstate`) é armazenado em um **bucket S3** com **criptografia** e **versionamento** habilitados.
- O **DynamoDB** é usado para locking do estado remoto, evitando execuções concorrentes.
- Secrets e credenciais não são armazenados no repositório — são passados via variáveis seguras.

---

## 🚀 Como Usar

1. Clone o repositório:
   ```bash
   git clone https://github.com/nazareno-jr/human-gov-infrastructure.git
   cd human-gov-infrastructure
````

2. Configure suas credenciais AWS (via `aws configure` ou variáveis de ambiente)

3. Inicialize o Terraform:

   ```bash
   terraform init
   ```

4. Aplique o ambiente de um tenant específico:

   ```bash
   terraform apply -var-file="tenants/tenant1.tfvars"
   ```

---

## 📈 Próximos Passos (em andamento)

* Integração com GitHub Actions para CI/CD
* Monitoramento com CloudWatch
* Diagrama de arquitetura
* Exposição com DNS + SSL via ACM
* Documentação para novos colaboradores

---

## ✍️ Autor

Desenvolvido por [Nazareno Jr.](https://github.com/nazareno-jr)
Projeto open-source para estudos, testes e demonstrações em ambiente AWS.

---

## 🛡️ Licença

Este projeto está licenciado sob os termos da **MIT License**.

```

---

Se quiser, posso agora gerar o **diagrama da arquitetura** com estilo AWS, mostrando EC2, S3, DynamoDB e IAM por tenant. Posso fazer isso?
```

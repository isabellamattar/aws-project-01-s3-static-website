# aws-project-01-s3-static-website

# ☁️ AWS Project 01: Static Website Hosting with S3, Versioning & Lifecycle Management

![AWS](https://img.shields.io/badge/AWS-S3-orange?style=for-the-badge&logo=amazon-s3)
![Status](https://img.shields.io/badge/Status-Completed-green?style=for-the-badge)

##  Visão Geral do Projeto
Este projeto demonstra a implementação de uma solução de hospedagem para websites estáticos altamente disponível, escalável e de baixo custo utilizando o **Amazon S3**. Além da hospedagem estática, foram implementadas práticas recomendadas de segurança, resiliência contra falhas humanas (via **S3 Versioning**) e governança de custos (**FinOps** via **Lifecycle Rules**).

---

##  Arquitetura da Solução

![Arquitetura da Solução](./arquitetura-projeto-1.png)

### Fluxo da Solução:
1. **Acesso Público Controlado:** O bucket foi configurado para hospedagem estática com uma *Bucket Policy* explícita para permissão de leitura pública (`s3:GetObject`).
2. **Versionamento Nativo:** O recurso de *S3 Versioning* garante a criação de histórico para qualquer arquivo sobrescrito ou deletado acidentalmente.
3. **Gestão de Ciclo de Vida (FinOps):** Regras automatizadas garantem que versões antigas e não-atuais de arquivos transitem para classes de armazenamento mais baratas (*Standard-IA*) após 30 dias e sejam purgadas após 90 dias, reduzindo custos desnecessários.

---

##  Serviços e Tecnologias Utilizadas
* **Amazon S3 (Simple Storage Service):** Hospedagem de objetos e servidor web estático.
* **S3 Static Website Hosting:** Módulo de roteamento para páginas web estáticas (`index.html`).
* **S3 Bucket Policies (JSON):** Configuração de acesso granular IAM para o bucket.
* **S3 Versioning:** Mecanismo de recuperação de desastres e histórico de arquivos.
* **S3 Lifecycle Rules:** Automação de ciclo de vida de objetos para otimização financeira.
* **HTML5 / CSS3:** Aplicação web estática demonstrativa.

---

##  Passo a Passo de Implementação

### 1. Criação e Liberabilidade do Bucket S3
- Bucket criado com o nome globalmente único `aws-project-01-s3-static-website`.
- Desativação do *Block All Public Access* para permitir a entrega de conteúdo estático via web.

### 2. Configuração de Hospedagem Estática e Permissões
- Ativação do *Static Website Hosting* com `index.html` definido como *Index Document*.
- Aplicação da seguinte política de bucket para acesso público de leitura:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::aws-project-01-s3-static-website/*"
        }
    ]
}

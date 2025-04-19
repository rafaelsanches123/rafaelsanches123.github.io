---
layout: post
title:  "Começando com Terraform: Provisione infraestrutura como código"
date:   2025-04-14 21:00:00 -0300
categories: IaC Terraform Infraestrutura Código Programação
---

![Terraform]({{ site.url }}/assets/terraform.png){:style="width: 100%" }

## Introdução
Terraform é uma ferramenta de infraestrutura como código (IaC) criada pela HashiCorp. Com ela, você pode definir e automatizar toda a infraestrutura da sua aplicação usando código. Neste post, vou te mostrar como começar a usar Terraform com um exemplo prático e simples.

## O que é infraestrutura como código (IaC)?
Infraestrutura como código é o processo de gerenciar e provisionar infraestrutura por meio de arquivos de configuração legíveis por máquinas, ao invés de processos manuais. Isso traz várias vantagens:

- **Automatização:** Criação de ambientes sem cliques manuais.
- **Versionamento:** Mudanças rastreadas com Git.
- **Consistência:** Infraestrutura replicável sem erro humano.

Ao usar IaC com o Terraform, você descreve o estado desejado da infraestrutura e deixa que a ferramenta se encarregue de criá-la ou atualizá-la.

Para fazer tudo isso que falamos você vai precisar conhecer duas palavrinhas muito importantes sendo elas: o **provider** e o **resource**.

### O que é um **provider**?

O **provider** (ou provedor) é o componente do Terraform que sabe **como se comunicar com a plataforma ou serviço onde você quer criar a infraestrutura**. Ele é como um “plugin” que conecta o Terraform a um ambiente externo, como:

- **AWS**
- **Azure**
- **Google Cloud**
- **Docker**
- **GitHub**
- **Kubernetes**
- **Local (para manipular arquivos locais)**


### O que é um **resource**?

Um **resource** (ou recurso) é **o que você quer criar ou gerenciar com Terraform**. Pode ser uma instância de servidor, uma base de dados, um bucket S3, um arquivo local, entre outros.

### Resumo rápido:

| Conceito   | O que é                            | Exemplo prático                        |
|------------|------------------------------------|----------------------------------------|
| **Provider** | Conexão com uma plataforma        | AWS, Azure, Google Cloud, Docker       |
| **Resource** | O que será criado/gerenciado      | VM, Bucket S3, banco de dados, arquivo |

Agora que você já entendeu um pouco dos termos e conceito do Terraform vamos ir para parte prática para te ajudar a entender melhor sobre essa ferramenta incrível.

## Instalando o Terraform
A instalação é simples:

1. Acesse o site oficial: [https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads)
2. Baixe a versão para seu sistema operacional.
3. Extraia o binário e adicione-o ao PATH do sistema.
4. Verifique no seu terminal com o comando a seguir e caso ele retorne a versão do terraform instalada isso significa que seu processo de instação e configuração funcionou com sucesso:
   ```bash
   terraform -v
   ```

## Criando seu primeiro projeto com Terraform
Vamos criar um arquivo local usando o provider "local". Crie uma pasta e dentro dela o arquivo `main.tf` com o seguinte conteúdo:

```hcl
provider "local" {}

resource "local_file" "hello_world" {
  content  = "Olá, Terraform!"
  filename = "hello.txt"
}
```

Agora rode os seguintes comandos:

```bash
terraform init     # Inicializa o projeto
terraform plan     # Mostra o que será criado
terraform apply    # Aplica as mudanças
```

O arquivo `hello.txt` será criado na sua pasta com o texto "Olá, Terraform!".

## Explicando o que aconteceu
- O Terraform leu o arquivo `main.tf` e viu que você queria criar um arquivo local.
- O comando `apply` criou esse recurso.
- Um arquivo `terraform.tfstate` foi criado. Ele guarda o estado da infraestrutura gerenciada.

## Terraform com docker como provider:

Usar o **Terraform com Docker** é uma forma excelente para fazer testes e entender como provisionar containers como infraestrutura como código. Abaixo está um exemplo simples que mostra como usar o provider do Docker para criar um container NGINX.

## Exemplo: Criando um container Docker com Terraform

### 1. **Pré-requisitos**
- Docker instalado e em execução. [Post do blog sobre Docker caso ainda não tenha ele instalado e configurado]({% link _posts/2023-07-16-instalando-e-configurando-o-docker.markdown %});
- Docker daemon rodando localmente.

---

### 2. **Estrutura do projeto**
Crie uma pasta chamada `terraform-docker-nginx` e dentro dela adicione um arquivo `main.tf` com o conteúdo abaixo:

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  name  = "meu_nginx"
  image = docker_image.nginx.latest
  ports {
    internal = 80
    external = 8080
  }
}
```

---

### 3. **Comandos Terraform**
No terminal, dentro da pasta do projeto:

```bash
terraform init      # Baixa os plugins necessários (como o docker)
terraform plan      # Mostra o que será criado
terraform apply     # Cria o container
```

Se tudo estiver certo, você verá uma saída parecida com:

```
docker_container.nginx: Creating...
docker_container.nginx: Creation complete after 3s
```

Depois disso, acesse [http://localhost:8080](http://localhost:8080) no navegador — você verá a tela padrão do NGINX rodando via container.

---

### 4. **Destruindo o container**
Para remover tudo que foi criado:

```bash
terraform destroy
```

---

### Explicação rápida

| Bloco Terraform      | O que faz                                           |
|----------------------|----------------------------------------------------|
| `terraform`          | Declara o provider Docker usado no projeto         |
| `provider "docker"`  | Habilita o Terraform a interagir com o Docker      |
| `docker_image`       | Baixa a imagem `nginx:latest`                      |
| `docker_container`   | Cria o container com base na imagem e publica a porta 8080 |

---


## Boas práticas iniciais
- Separe os arquivos `.tf` por responsabilidade, por exemplo:
  - `provider.tf` para os provedores
  - `main.tf` para os recursos
- Use `terraform destroy` para apagar a infraestrutura criada
- Versione seus arquivos com Git para manter histórico

## Próximos passos
Agora que você criou seu primeiro recurso, explore:
- Como criar máquinas virtuais na AWS, Azure ou GCP
- Como usar variáveis e saídas (`variables` e `outputs`)
- Como dividir o projeto em módulos reutilizáveis
- Como integrar o Terraform a pipelines de CI/CD

## Conclusão
Terraform é uma ferramenta poderosa e flexível para automatizar infraestrutura. Com apenas algumas linhas de código, você consegue criar recursos e manter seu ambiente replicável e sob controle. 

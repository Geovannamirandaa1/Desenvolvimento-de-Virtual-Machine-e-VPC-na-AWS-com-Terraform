Criação de Virtual Machine e VPC na AWS com Terraform

Introdução
Este projeto ilustra a criação de uma máquina virtual (VM) e uma Virtual Private Cloud (VPC) na AWS utilizando **Terraform**. O objetivo é fornecer um guia prático e didático para iniciantes, introduzindo conceitos básicos de infraestrutura como código (IaC), além de configurar um **Remote State** para armazenar o estado do Terraform em um bucket S3.

---

Estrutura do Repositório
O repositório está organizado para facilitar a compreensão e a manutenção do projeto. Abaixo está a estrutura dos diretórios e arquivos:

plaintext
AWS-VM-VPC/
│
├── locals.tf        # Definição de variáveis locais, como tags padrão
├── main.tf          # Configuração principal do Terraform e do backend remoto
├── outputs.tf       # Declaração das saídas, como o IP público da VM
├── variables.tf     # Declaração de variáveis reutilizáveis
└── vpc-vm.tf        # Recursos Terraform para criar a infraestrutura (VPC, VM, etc.)
```


Descrição dos Arquivos

1. locals.tf
Define variáveis locais reutilizáveis, como **tags padrão** aplicadas aos recursos. Essas tags ajudam a identificar o proprietário e o método de gerenciamento da infraestrutura.

---

2. main.tf
Arquivo principal do projeto. Nele, são configurados:
- Versão mínima do Terraform.
- Provedor AWS.
- Configuração do **Remote State**, armazenando o estado no S3 com bloqueio de estados via DynamoDB.

---

3. outputs.tf
Declara as saídas do Terraform, como:
- O ID da VPC criada.
- O endereço IP público da instância EC2.

Essas informações são úteis para acessar a VM ou integrar com outros sistemas.

---

4. variables.tf
Declara as variáveis reutilizáveis que tornam o projeto parametrizável. Por exemplo:
- Intervalos CIDR para a VPC e sub-rede.
- Tipo da instância EC2.
- Nome da chave SSH.

---

5. vpc-vm.tf
Contém a definição de todos os recursos necessários para criar a infraestrutura, incluindo:
- VPC e sub-rede pública.
- Internet Gateway e rotas.
- Security Group** com regras para conexões SSH.
- Instância EC2 com configuração de chave SSH.

---
Fluxo de Trabalho
1. Clonar o Repositório  
   Clone o repositório localmente para começar:  
   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd AWS-VM-VPC
   

2. Inicializar o Terraform  
   Configure o ambiente Terraform no diretório do projeto:  
   ```bash
   terraform init
   ```

3. Validar Configurações
   Confirme que os arquivos estão configurados corretamente:  
   ```bash
   terraform validate
   ```

4. Planejar e Aplicar
   Gere um plano de execução e aplique as configurações:  
   ```bash
   terraform plan
   terraform apply
   ```

5. Verificar Saídas  
   Após aplicar, as saídas, como o **IP público da instância EC2**, serão exibidas. Use-as para acessar sua VM:  
   ```bash
   ssh -i <sua-chave-privada.pem> ec2-user@<IP-PUBLICO>
   ```

---
Requisitos
- Conta AWS com permissões adequadas.
- Terraform instalado (versão 1.3.0 ou superior).
- Chave SSH pública criada e disponível localmente (por exemplo, `aws-key.pub`).

---

Expansões Futuras
- Configurar monitoramento da instância EC2 com Amazon CloudWatch.
- Adicionar regras de segurança mais específicas no Security Group.
- Automatizar o provisionamento da VM com scripts de inicialização.


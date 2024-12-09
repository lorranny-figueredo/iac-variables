# iac-variables README

Este repositório utiliza input variables para personalizar módulos do Terraform sem modificar seu código, facilitando a reutilização em diferentes configurações. Além disso, contém os arquivos necessários para configurar um ambiente IaC com Terraform em um container Docker, com o objetivo de provisionar e destruir uma instância na AWS.


## Pré-requisitos
* Docker instalado na sua máquina.
* Credenciais da AWS (Access Key e Secret Key).

## Passo a Passo

### 1. Construir a Imagem Docker
```
docker build -t iac-variables-image:latest .
```

### 2. Executar o Container Docker
Após a construção da imagem, cire o container Docker com o comando abaixo:


```
docker run -dit --name iac-variables iac-variables-image:iac /bin/bash
```


### 3. Acessar o Terminal do Container
Agora, entre no terminal do container iac-variables com o seguinte comando:


```
docker exec -it iac-variables /bin/bash
```

### 4. Configurar AWS CLI
Dentro do terminal do container, configure as credenciais da AWS executando o comando:


```
aws configure
```

Digite as credenciais de acesso (Access Key e Secret Key) quando solicitado.

### 5. Inicializar o Terraform
No terminal do container, navegue até o diretório onde o arquivo main.tf está localizado:


```
cd /iac-variables
```

Em seguida, execute o comando para inicializar o Terraform:


```
terraform init
```


### 6. Intalar vim e criar terraform.tfvars e variables.tf

Intalar vim
```
apt-get install vim
```

criar terraform.tfvars
```
vi terraform.tfvars
```
Entrar no modo de inserção: Pressione i. <br>
Digitar conteúdo do terraform.tfvars. <br>
Sair do modo de inserção: Pressione Esc. <br>
Sair do Vim e salvar o arquivo: 
```
:wq
```

criar variables.tf
```
vi variables.tf
```
Entrar no modo de inserção: Pressione i. <br>
Digitar conteúdo do variables.tf. <br>
Sair do modo de inserção: Pressione Esc.<br>
Sair do Vim e salvar o arquivo:
```
:wq
```
### 7. Validar o Plano do Terraform
Para validar a configuração e ver o que será provisionado, execute:


```
terraform plan
```

O Terraform mostrará um plano detalhado dos recursos que serão criados na AWS.

### 8. Provisionar a Instância na AWS
Se o plano estiver correto e você estiver pronto para provisionar a instância, execute:


```
terraform apply
```
Isso criará a instância na AWS.

### 9. Destruir os Recursos Provisionados
Após finalizar o uso da instância, você pode destruir a instância EC2 criada:


```
terraform destroy
```

## Observações

Se você criar uma instância EC2 usando o Terraform e não especificar a VPC, o Terraform irá, por padrão, utilizar a VPC Default da sua conta. Isso significa que a sua instância será criada dentro dessa VPC.


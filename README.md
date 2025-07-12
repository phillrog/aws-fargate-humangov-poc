<img width="1879" height="605" alt="image" src="https://github.com/user-attachments/assets/d810bfab-17ae-4a96-8ee7-47700bf50b6f" />

### **Parte 01 – Containerização e Envio da Imagem com Docker + ECR**

Nesta etapa, você irá empacotar a aplicação **HumanGov** e o **Webserver** (Nginx) em imagem Docker e realizar o envio (push) das imagens para o **Amazon Elastic Container Registry (ECR)**.

Isso inclui:

- Criação do Dockerfile com as dependências da aplicação;
- Construção e teste local da imagem;
- Autenticação no ECR e envio seguro da imagem para o repositório na AWS.

***O objetivo é garantir que a aplicação esteja pronta para ser executada em ambiente containerizado e armazenada com segurança no repositório da nuvem.***

---

### **Parte 02 – Provisionamento de Recursos com Terraform**

Com a imagem já publicada no ECR, você irá utilizar **Terraform** para provisionar os recursos da AWS que compõem a infraestrutura da aplicação:

- **Buckets S3** para armazenamento de dados;
- **Tabelas DynamoDB** para persistência de registros;
- E vamos também criar um Cluster ECS!

***Essa etapa assegura a consistência da infraestrutura, com provisionamento automatizado, versionado e replicável.***

---

### **Parte 03 – Deploy Manual com ECS: Criando Task Definitions e Services**

Nesta última fase, você criará manualmente a **definição de tarefa (Task Definition)** no ECS, apontando para a imagem do ECR, e implantará a aplicação através de um **serviço ECS**.

Isso envolve:

- Configurar o tipo de rede e alocação de recursos da task;
- Associar a imagem do container publicada no ECR;
- Lançar o serviço ECS e verificar o funcionamento da aplicação por tenant.

***Essa etapa demonstra o fluxo de deploy manual, destacando a complexidade e a importância de automações em projetos futuros.***


- Crie **IAM Role** para a Execução das “Tasks”:
    
    <aside>
    💡
    
    Assim como criamos **IAM Roles** para permitir que as instâncias **EC2** executem ações em **tabelas DynamoDB** e **buckets S3**, também precisamos definir uma **IAM Role específica para o Cluster ECS**. Essa role é essencial para que o ECS tenha permissão de **executar as tasks** da aplicação com segurança e controle de acesso adequado.
    
    </aside>
    
    **IAM | Roles**
    
    - **AWS service**
    - **Service or use case: `Elastic Container Service`**
    - **Chose a use case for the specific service | Use case: `Elastic Container Service Task`**
    - **Permissões:**
        - **`AmazonS3FullAccess`**
        - **`AmazonDynamoDBFullAccess`**
        - **`AmazonECSTaskExecutionRolePolicy`**
    - **Name: `HumanGovECSExecutionRole`**
        
        ***Create Role***

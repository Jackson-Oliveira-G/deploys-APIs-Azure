# deploys-APIs-Azure

Vou explicar como fazer isso usando o **Azure App Service**, que é uma das maneiras mais comuns para hospedar APIs RESTful na nuvem, e algumas outras opções populares como **Azure Functions** ou **Docker containers** no Azure. Vou te guiar por um processo detalhado.

### 1. **Preparando o Ambiente Localmente (Desenvolvimento da API)**
Antes de fazer o deploy, é importante garantir que sua API esteja funcionando corretamente localmente.

#### Exemplo com Node.js:
Caso esteja desenvolvendo uma API com **Node.js**, por exemplo, você pode criar uma aplicação simples com o framework **Express**:

```bash
mkdir minha-api
cd minha-api
npm init -y
npm install express
```

Crie o arquivo **index.js**:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('API funcionando!');
});

app.listen(port, () => {
  console.log(`API rodando em http://localhost:${port}`);
});
```

Agora, sua API está pronta para ser testada localmente. Execute o comando:

```bash
node index.js
```

### 2. **Criando e Configurando o Azure App Service**
Agora que sua API está pronta, vamos criar o **Azure App Service**, que é uma plataforma gerenciada para hospedar aplicações web e APIs.

#### Passos:
1. **Acesse o portal do Azure**: Vá para o [portal do Azure](https://portal.azure.com/).
2. **Crie um novo recurso**:
   - Clique em **Criar um recurso**.
   - Selecione **Web App**.
   - Preencha as informações:
     - **Assinatura**: Selecione a assinatura que você está utilizando.
     - **Grupo de Recursos**: Crie um novo ou use um existente.
     - **Nome do App**: Escolha um nome único para o seu App Service.
     - **Sistema Operacional**: Escolha entre Windows ou Linux (dependendo de como você configurou a sua API).
     - **Plano de hospedagem**: Escolha o plano de hosting. Para testes, você pode escolher o plano gratuito.
3. Clique em **Revisar + Criar** e depois em **Criar**.

### 3. **Deploy da API no Azure App Service**
Agora que seu App Service está configurado, você pode fazer o deploy da sua API.

#### Método 1: Deploy via Git (GitHub ou Azure Repos)
O Azure permite que você faça o deploy contínuo da sua API diretamente do seu repositório Git (GitHub, GitLab, Azure Repos, etc.).

1. **Configuração do Deployment Center**:
   - No portal do Azure, acesse o App Service que você criou.
   - Vá para **Deployment Center**.
   - Escolha **GitHub** ou **Azure Repos** (dependendo de onde está o código da sua API).
   - Conecte sua conta do GitHub ou Azure Repos e selecione o repositório onde sua API está.
   - Selecione o branch que deseja fazer o deploy.
   - Clique em **Conectar** e depois **Concluir**.

   O Azure fará o deploy automático sempre que houver um novo commit no branch selecionado.

#### Método 2: Deploy via FTP
Caso prefira usar FTP para fazer o upload do seu código diretamente, siga estas etapas:

1. No portal do Azure, dentro do seu App Service, vá para **Configuração** → **Deployment Center**.
2. Habilite o **FTP** e anote as credenciais fornecidas.
3. Use um cliente FTP (como FileZilla) para conectar ao servidor e enviar os arquivos da sua API.

#### Método 3: Deploy via Azure CLI
Você pode também usar o **Azure CLI** para fazer o deploy diretamente da sua aplicação para o App Service. Se o **Azure CLI** estiver instalado, execute o seguinte comando no terminal:

```bash
az webapp up --name <nome-do-app> --resource-group <nome-do-grupo-de-recursos>
```

Isso fará o upload do código e o configurará automaticamente no Azure App Service.

### 4. **Configuração de Banco de Dados (se necessário)**
Se sua API utiliza um banco de dados, você pode configurar um **Azure SQL Database**, **Cosmos DB**, ou outro serviço de banco de dados no Azure.

1. Crie um **Banco de Dados** no Azure.
2. Configure as variáveis de ambiente no App Service com as strings de conexão necessárias para o banco de dados (vá em **Configuração** → **Configurações de aplicativo**).

### 5. **Testando a API**
Agora, depois de fazer o deploy da sua API, você pode acessar a URL pública do seu App Service para testá-la. No portal do Azure, na página do seu App Service, você verá a URL para o seu endpoint.

### 6. **Monitoramento e Logs**
Acompanhe o desempenho e monitore sua API utilizando o **Azure Monitor** e **Application Insights**. Estes serviços fornecem métricas, logs de aplicação e diagnósticos para acompanhar a saúde da sua API e identificar problemas.

1. **Application Insights**: Você pode habilitar o Application Insights para obter métricas detalhadas sobre como sua API está se comportando e coletar logs de erros.

### 7. **Escalabilidade**
Azure App Service oferece escalabilidade automática, ou seja, você pode configurar seu app para escalar automaticamente dependendo da carga de tráfego.

1. Acesse **Escalabilidade** no portal do Azure.
2. Defina a escala automática com base em regras (ex.: aumentar o número de instâncias quando a carga for maior que 80%).

---

Esses são os passos principais para fazer o deploy de uma API no Azure usando o **App Service**. Dependendo das suas necessidades, você também pode explorar **Azure Functions** (para APIs serverless) ou utilizar **Azure Kubernetes Service (AKS)** para deploy de APIs em containers.

Se você precisar de mais detalhes sobre algum desses passos, ou se estiver utilizando uma tecnologia diferente, é só avisar!

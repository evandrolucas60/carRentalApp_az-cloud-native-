## Projeto App RentCar

Este repositório contém uma aplicação de aluguel de carros, composta por um backend em Node.js (BFF) e funções Azure Functions responsáveis pelo processamento de locações e pagamentos.

## 📁 Estrutura do Projeto

```
app-rentCar/
  rc-backend/             # Backend Node.js (BFF)
    index.js
    package.json
    Dockerfile
    .env
    query.sql
  az-functions/
    fnRentProcess/        # Solução Azure Functions
      fnPayment/          # Função de pagamento
        Function1.cs
        PaymentModel.cs
        Program.cs
      fnRentProcess/      # Função de processamento de locação
        Function1.cs
        Program.cs
      fnSBRentProcess/    # Função para integração com Service Bus (opcional/futuro)
```

## 📌 Descrição

* **rc-backend**: API desenvolvida em Node.js que recebe as requisições de locação, constrói a mensagem e envia para a fila do Azure Service Bus.
* **az-functions/fnRentProcess**: Solução em Azure Functions que consome as mensagens da fila, processa locações, efetua pagamentos e realiza outras integrações necessárias.

## ▶️ Como Executar

### 🔧 Backend Node.js

1. Navegue até a pasta `rc-backend`:

   ```sh
   cd app-rentCar/rc-backend
   ```

2. Instale as dependências:

   ```sh
   npm install
   ```

3. Configure as variáveis de ambiente no arquivo `.env`:

   ```env
   KEY_VAULT_URL=<sua-url-keyvault>
   SERVICE_BUS_CONNECTION_STRING=<sua-connection-string>
   ```

4. Inicie o servidor:

   ```sh
   npm start
   ```

   O backend estará disponível em: `http://localhost:3001`

### ☁️ Azure Functions

1. Navegue até a pasta `az-functions/fnRentProcess`.
2. Abra a solução `fnRentProcess.sln` no Visual Studio.
3. Configure as variáveis de ambiente necessárias (no Visual Studio ou via `local.settings.json`).
4. Execute as funções desejadas, como `fnPayment` ou `fnRentProcess`.

## 🔗 Endpoints

### `POST /api/locacao`

Recebe os dados da locação e envia uma mensagem para a fila do Azure Service Bus.

**Exemplo de body:**

```json
{
  "name": "Evandrio Lucas Da Silva",
  "email": "evandrolucas@email.com",
  "modelo": "Fiat Uno",
  "ano": 1998,
  "data": "6 week"
}
```

## 🛠️ Tecnologias Utilizadas

* **Backend**: Node.js, Express, dotenv
* **Azure SDKs**: @azure/identity, @azure/keyvault-secrets, @azure/service-bus
* **Serverless**: Azure Functions (.NET)
* **Outros**: Azure Service Bus, Azure Key Vault

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Consulte o arquivo [LICENSE](./LICENSE) para mais detalhes.

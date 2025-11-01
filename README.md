
# Azure Web App Project

This project demonstrates how to deploy a simple Flask web application to Azure App Services with autoscaling, custom domains, and performance monitoring.

## 📁 Project Structure
```
azure_web_app_project/
│
├── app/
│   ├── __init__.py
│   └── main.py
│
├── requirements.txt
├── startup.txt
├── azure-pipelines.yml
└── autoscale.json
```

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- Azure CLI
- Azure Subscription
- Git

### Setup Instructions
1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd azure_web_app_project
   ```

2. Create a virtual environment and install dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scriptsctivate`
   pip install -r requirements.txt
   ```

3. Run the app locally:
   ```bash
   python app/main.py
   ```

## ☁️ Deploy to Azure

1. Login to Azure:
   ```bash
   az login
   ```

2. Create a resource group and App Service plan:
   ```bash
   az group create --name <resource-group> --location <location>
   az appservice plan create --name <app-service-plan> --resource-group <resource-group> --sku B1 --is-linux
   ```

3. Create the Web App:
   ```bash
   az webapp create --resource-group <resource-group> --plan <app-service-plan> --name <app-name> --runtime "PYTHON|3.8" --deployment-local-git
   ```

4. Deploy the app using Git or Azure DevOps (see `azure-pipelines.yml`).

## 📈 Autoscaling

The `autoscale.json` file defines autoscaling rules based on CPU usage. To apply:
```bash
az monitor autoscale create --resource-group <resource-group> --resource <app-service-plan>   --resource-type Microsoft.Web/serverfarms --name autoscale-rule --min-count 1 --max-count 3 --count 1   --condition "Percentage CPU > 70 avg 5m" --scale out 1
```

## 🔍 Monitoring

Enable Application Insights via Azure Portal or CLI:
```bash
az monitor app-insights component create --app <app-name> --location <location> --resource-group <resource-group>
```

## 📄 License
This project is licensed under the MIT License.


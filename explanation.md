# These are all the tags I would have used since I couldn't get any azure quotas in time 

## 1. **Bash commands**

### 

- This will install helm - the package managment tool.
  ```bash
  sudo snap install helm --classic
  ```
### 

- This adds helm repositories for Loki, Promtail, and Grafana.
  ```bash
  helm repo add grafana https://grafana.github.io/helm-charts
    helm repo update
  ```
  ### 

- This will deploy loki using helm.
  ```bash
  helm upgrade --install loki grafana/loki-stack --namespace monitoring --create-namespace
  ```
  ### 

- This will deploy grafana using helm.
  ```bash
  helm upgrade --install grafana grafana/grafana --namespace monitoring
  ```
  ### 

- This gives you the grafana password .
  ```bash
  kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
  ```
  ### 

- This is to port-forward grafana to access it locally.
  ```bash
  kubectl port-forward --namespace monitoring service/grafana 3000:80
  ```
- In data source you set this url to access it locally http://loki:3100

### 

- After creating a new dashboard in grafana you can use the logs panel to query logs from Loki so that you can visualize them.
  



## 2. **Azure CLI Commands**

### 

- This will create an Azure Kubernetes Service cluster.
  ```bash
  az aks create --resource-group kevin-testR \
    --name kevin-cluster \
    --node-count 1\
    --enable-managed-identity \
    --generate-ssh-keys
  ```
  
### 

- This fetches the credentials that are used to connect to the AKS cluster.
  ```bash
  az aks get-credentials --resource-group kevin-testR --name kevin-cluster
  ```

## 3. **Kubectl Commands**

### 

- This will list all nodes in the AKS cluster.
  ```bash
  kubectl get nodes
  ```

### 

- This applies the YAML configuration file to the cluster.
  ```bash
  kubectl apply -f pipeline.yaml
  ```

### 

- This is to forward a port from a Kubernetes service to localhost.
  ```bash
  kubectl port-forward svc/grafana 3000:80 -n monitoring
  ```
  

## 4. **Helm Commands**

### 

- This updates local Helm repository cache.
  ```bash
  helm repo update
  ```


## 5. **Tekton Commands**

### 

- This starts a Tekton pipeline execution.
  ```bash
  tkn pipeline start build-and-deploy
  ```

## 6. **ModSecurity Configuration**

### 

- This is to intall Nginx Ingress Controller with ModSecurity enabled.
  ```bash
  helm install nginx-ingress ingress-nginx/ingress-nginx \
    --set controller.enableModsecurity=true \
    --set controller.enableOWASPCoreRules=true
  ```
  - The first one enables modsecurity 
  - The second one enables OWASP core rules ( this will protect the web application from attack paterns)
  



This explanation.md file provides all the tags used in the challenge to configure logging, CI/CD, and security on AKS using the Ubuntu terminal.


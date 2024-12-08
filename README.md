# Kubernets Actions - Declarative 

Nesse repositoro esta o primeiro exemplo de como usarmos kubernets de forma declarativa. Priemria coisa a se fazer é criar um arquivo .yaml, tanto faz o nome do arquivo. A ideia é muito semelhante a um arquivo docker-compose.

Todo arquivo .yaml do kubernts tem a estrutura abaixo:

```bash
apiVersion: *** (Versão kubernets)
kind: *** Qual Object desejamos chamar (Deployment, Service, Jobs, Pods)
metadata:
  name: name_of_deployment

--  a partir daqui comeca todos as especificacoes tecnicas do kubernets
spec:
  ***
  ***
```

Podemos criar dois arquivos, um para cada objetivo que desejamos, por exemplo deployment.yaml e outro service.yaml

Vamos criar o arquivo deployment.yaml

```bash
apiVersion: apps/v1 
kind: Deployment  
metadata:
  name: name_of_deployment

spec:
  replicas: 1
  selector:
    matchlabels:
      app: second-app
      tier backend
  template:
    metadata:
      labels:
        app: second-app
        tier: backend
    spec:
      containers:
        - name: second-add
        image: rafaelfabri/name_of_img
```

```bash
apiVersion: v1
kind: Service
metadata:
  name: name_of_Service
  
spec:
  selector:
    matchLabels:
      app: second-app
    
  ports:
  - protocols: 'TCP' 
    port: 80
    targetPort: 8080
    
  type: LoadBalancer
```

```bash
kubectl apply -f=deployment.yaml
```  

```bash
kubectl apply -f=serivce.yaml
```  

Se quisermos rodar tudo junto de uma vez so.

```bash
kubectl apply -f=deployment.yaml,serivce.yaml
```  

Mas tambem podemos colocar tudo em um unico arquivo temos que colocar o ---

```bash
apiVersion: apps/v1 -- (Versão kubernets)
kind: *** Qual Object desejamos chamar (Deployment, Service, Jobs, Pods)
metadata:
  name: name_of_deployment

spec:
  replicas: 1
  selector:
    matchlabels:
      app: second-app
      tier backend
  template:
    metadata:
      labels:
        app: second-app
        tier: backend
    spec:
      containers:
        - name: second-add
        image: rafaelfabri/name_of_img

---

apiVersion: v1
kind: Service
metadata:
  name: name_of_Service
  
spec:
  selector:
    matchLabels:
      app: second-app
    
  ports:
  - protocols: 'TCP' 
    port: 80
    targetPort: 8080
    
  type: LoadBalancer

```



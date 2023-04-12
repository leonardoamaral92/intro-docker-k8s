# Como configurar o projeto

Pré-requisitos:
- Minikube
- Python 


## Configurando a imagem no Hub

Importante: Execute dentro da pasta do projeto para ter visibilidade do arquivo Dockerfile usando . 

1. Vamos começar construindo a imagem:
    `docker build -t <nome-imagem> .`

2. Em seguite, após a imagem ser construída, para executar digite:
    `docker run -d -p 5000:5000 --name <nome-que-quiser> --rm <nome-imagem>`

    Para verificar se está rodando:
    `docker ps`

    Se tudo estiver certo, já pode acessar no seu browser: localhost:5000

3. Para enviar ao Hub do Docker, crie sua conta no Hub e digite os comandos: 

    3.1 Para logar no hub: `docker login`

    Importante: Semelhante ao Git, é preciso criar um repositório para conseguir dar push na imagem.

    3.2 Para subir a imagem: `docker push nome-imagem>`

## Configurando o deployment

1. Para criar o deployment vamos rodar o comando:
Importante: esteja com o minikube executando e logado com o docker

    `kubectl create deployment flask-deployment --image=<caminho-imagem-no-dockerhub>`

2. Para saber mais detalhes sobre os deployments, execute os dois comandos:
    - `kubectl get deployments`
    - `kubectl describe deployments`

3. Para saber mais detalhes sobre os pods, execute os dois comandos:
    - `kubectl get pods`
    - `kubectl describe pods`    

4. Caso queira reiniciar os pods manualmente devido a algum problema:
    - `kubectl rollout restart deployment flask-deployment`

## Criando e configurando o service 

1. Vamos começar expondo nosso deployment criado anteriormente:    
    - `kubectl expose deployment flask-deployment --type=LoadBalancer --port=5000`  
    Atenção na porta de exposição, escolhemos a mesma que está configurada no projeto python e na imagem docker.  

2. Gerando um IP para o service:
    - `minikube service <nome>`  

3. Verificar todos os serviços disponíveis e obter mais detalhes, respectivamente:
    - `kubectl get services` 
    - `kubectl describe services/<nome>` 

## Replicando a aplicação

1. Criando replicas de pods
    - `kubectl scale deploymenty/<nome> --replicas=<numero>`
    
    Após isso é possível ver o efeito no dashboard do minikube ou com o comando para listar pods. 


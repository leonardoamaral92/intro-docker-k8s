# Como configurar o projeto

Pré-requisitos:
- Minikube
- Python 


## Executando o deployment

Executando o arquivo deployment:
- `kubectl apply -f <ARQUIVO>`

Parando o deployment pelo arquivo:
- `kubectl delete -f <ARQUIVO>`

## Executando o service

Executando o arquivo service (mesma maneira do deployment):
- `kubectl apply -f <ARQUIVO>`

Gerando IP de acesso com Minikube:
- `minikube service <NOME>`

Parando o serviço (mesma maneira do deployment):
- `kubectl delete -f <ARQUIVO>`

## Atualizando a imagem do deployment

- Imagina que você alterou seu projeto e precisa refazer a imagem
1. `docker build -t <caminho-imagem-hub:flag> .`
2. `docker push <caminho-imagem-hub:flag>`
3. Agtualize a tag da imagem no arquivo de deployment
4. `kubectl apply -f <arquivo-deployment>`

O Kubernetes vai identificar a mudança da imagem, vai derrubar os pods desatualizados e subir novos pods atualizados. 
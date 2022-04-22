# Projeto prático: Otimização de uma imagem golang
Desafio imagem go &lt; 2mb - Treinamento Full Cycle

## Descrição do projeto

Esse desafio é muito empolgante principalmente se você nunca trabalhou com a linguagem Go!
Você terá que publicar uma imagem no docker hub. Quando executarmos:

    -  docker run <seu-user>/codeeducation
    
Temos que ter o seguinte resultado: `Code.education Rocks!`

Se você perceber, essa imagem apenas realiza um print da mensagem como resultado final, logo, vale a pena dar uma conferida no próprio site da Go Lang para aprender como fazer um "olá mundo".

Lembrando que a Go Lang possui imagens oficiais prontas, vale a pena consultar o Docker Hub.

A imagem de nosso projeto Go precisa ter menos de 2MB =)

Dica: No vídeo de introdução sobre o Docker quando falamos sobre o sistema de arquivos em camadas, apresento uma imagem "raiz", talvez seja uma boa utilizá-la.

Divirta-se

## Utilizando o multi-stage build para compilar a aplicação e otimizar a imagem

## Dockerfile.scratch

- Stage 1

```
# Iniciando uma imagem base golang:alpine
FROM golang:1.16.4-alpine3.13 AS build

# criando diretório de trabalho
WORKDIR /go/app

ADD . .

#Rodando go mod init com o nome do modulo 
RUN go mod init menos-de-2mb
RUN CGO_ENABLED=0 go build -o app


```
- Stage 2
```
# Iniciando com scratch
FROM scratch as production


# copiando o binário
COPY --from=build /go/app/app /app

# executando 
ENTRYPOINT ["/app"]


# Build 
docker build -t 18091982/codeeducation .

## Images
```
docker images
```

## Run
docker run 18091982/codeeducation


# Resultado
docker run 18091982/codeeducation










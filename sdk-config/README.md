# SDK-Config Docker Image

Este Dockerfile constrói uma imagem Docker que configura um ambiente de desenvolvimento para Android usando Ubuntu como base. Ele inclui o Java SDK, Android SDK e outras ferramentas essenciais para desenvolvimento Android.

## Sobre a Imagem

Esta imagem foi projetada para simplificar a configuração inicial para desenvolvimento Android, encapsulando o Android SDK e as ferramentas de linha de comando necessárias. É ideal para ambientes de integração contínua (CI/CD) ou para desenvolvedores que desejam um ambiente pronto para uso sem a necessidade de configuração manual extensiva.

## Ferramentas Incluídas

- **Java OpenJDK 21**: Ambiente de execução Java completo.
- **Android SDK Command Line Tools**: Ferramentas necessárias para desenvolvimento Android via linha de comando.
- **Android Platform Tools**: Ferramentas que suportam desenvolvimento Android, como adb.
- **Android Build Tools para API 34**: Ferramentas necessárias para compilar aplicações Android.

## Organização do Dockerfile

O Dockerfile segue uma estrutura lógica para construção da imagem:

1. **Base da Imagem**: Usa `ubuntu:jammy-20240427` como a imagem base.
2. **Instalação de Pacotes**: Instala todos os pacotes necessários para o desenvolvimento, incluindo ferramentas de sistema e desenvolvimento.
3. **Configuração do Android SDK**: Instala e configura o Android SDK e suas ferramentas associadas.
4. **Limpeza**: Remove arquivos desnecessários para manter a imagem enxuta.

## Como Usar

### Pré-requisitos

- **Docker** instalado na sua máquina. [Instale Docker aqui](https://docs.docker.com/get-docker/)

### Executando a Imagem

Para utilizar esta imagem, você pode puxá-la diretamente do Docker Hub e executá-la em seu ambiente local:

```bash
docker pull thehprogrammer/sdk-config:latest
```

Após puxar a imagem, você pode iniciar um container usando:

```bash
docker run -it thehprogrammer/sdk-config /bin/bash
```

Este comando inicia um shell interativo dentro do container, permitindo que você execute comandos relacionados ao Android SDK.

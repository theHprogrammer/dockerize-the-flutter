# ASDF-Flutter Docker Image

Este Dockerfile constrói uma imagem Docker que configura um ambiente de desenvolvimento para Flutter usando o sistema ASDF para gerenciamento de versões. Ele inclui o Flutter SDK totalmente configurado e pronto para uso, junto com a capacidade de gerenciar outras ferramentas e versões usando ASDF.

## Sobre a Imagem

Esta imagem foi projetada para oferecer flexibilidade e facilidade no desenvolvimento de aplicações Flutter. Ela é baseada na imagem `sdk-config`, que já inclui todas as configurações necessárias do Android SDK, proporcionando um ambiente completo para o desenvolvimento Flutter e Android.

## Ferramentas Incluídas

- **ASDF Version Manager**: Permite a gestão de múltiplas versões de linguagens e ferramentas de desenvolvimento.
- **Flutter SDK**: Ambiente de desenvolvimento Flutter configurado para começar a codificar imediatamente.
- **Android SDK (herdado da sdk-config)**: Ferramentas essenciais do Android SDK estão disponíveis e configuradas.

## Organização do Dockerfile

O Dockerfile segue uma estrutura lógica para construção da imagem:

1. **Base da Imagem**: Inicia a partir da `thehprogrammer/sdk-config:latest`.
2. **Configuração do ASDF**: Instala e configura o ASDF para gerenciar o Flutter e outras possíveis ferramentas.
3. **Instalação do Flutter**: Utiliza o ASDF para instalar e configurar a versão desejada do Flutter.

## Como Usar

### Pré-requisitos

- **Docker** instalado na sua máquina. [Instale Docker aqui](https://docs.docker.com/get-docker/)

### Executando a Imagem

Para utilizar esta imagem, você pode puxá-la diretamente do Docker Hub e executá-la em seu ambiente local:

```bash
docker pull thehprogrammer/asdf-flutter:latest
```

Após puxar a imagem, você pode iniciar um container usando:

```bash
docker run -it thehprogrammer/asdf-flutter /bin/bash
```

Este comando inicia um shell interativo dentro do container, permitindo que você execute comandos Flutter e desenvolva suas aplicações.

Para desenvolvimento web com Google Chrome ou testes em dispositivos físicos, você pode usar:

```bash
docker run -it --privileged \
  -v /usr/bin/google-chrome:/usr/bin/google-chrome \
  -v /dev/bus/usb:/dev/bus/usb \
  -v $(pwd):/home/user/workspace \
  -e CHROME_EXECUTABLE=/usr/bin/google-chrome \
  thehprogrammer/asdf-flutter
```

Isso configura o container para acessar o Google Chrome instalado localmente e dispositivos USB conectados para desenvolvimento Android e testes web.

> OBS: Certifique-se de que o Google Chrome está instalado na sua máquina e que você tem permissões para acessar dispositivos USB. O path do Chrome pode variar dependendo do sistema operacional.
# Dockernize-the-Flutter

Este projeto visa fornecer um ambiente Dockerizado completo para o desenvolvimento de aplicações com o Flutter, facilitando a configuração e padronizando o ambiente de desenvolvimento para todos os contribuidores.

## Sumário

- [Sobre o Projeto](#sobre-o-projeto)
- [Recursos](#recursos)
- [Como Executar](#como-executar)
- [Contribuição](#contribuição)
- [Licença](#licença)
- [Contato](#contato)

## Sobre o Projeto

O "Dockernize-the-Flutter" é uma iniciativa para criar um ambiente de desenvolvimento isolado usando Docker, que encapsula todas as ferramentas necessárias para desenvolver aplicações Flutter. Isso inclui a configuração do Flutter SDK, Android SDK, e outras dependências, dentro de containers Docker, simplificando o processo de setup para novos desenvolvedores e evitando discrepâncias entre ambientes de desenvolvimento.

A escolha do ASDF como gerenciador de versões para a instalação do Flutter permite uma flexibilidade sem precedentes na gestão de múltiplas versões do Flutter ou outras ferramentas de linha de comando. Isto é particularmente útil em ambientes de desenvolvimento onde a compatibilidade entre diferentes versões de ferramentas pode ser um desafio, ou quando há a necessidade de testar a aplicação em várias versões do Flutter sem afetar a configuração global. Além disso, o ASDF permite que os desenvolvedores adicionem facilmente novas linguagens ou frameworks ao seu ambiente Dockerizado, ajustando-se às necessidades em evolução dos projetos e equipes.

## Recursos

Este projeto inclui:

- Dockerfile para criar uma imagem com o Flutter SDK instalado via ASDF.
- Dockerfile para configurar o Android SDK, ferramentas de linha de comando e NDK.
- Guia detalhado de como usar os containers e executar aplicações Flutter.

Vamos ajustar a seção "Como Executar" para incluir informações sobre a obtenção das imagens do Docker Hub, além de oferecer uma descrição mais detalhada sobre como usar esses containers para desenvolver aplicações Flutter. Aqui está uma versão revisada:

## Como Executar

Para utilizar este ambiente Dockerizado, siga os passos abaixo:

### Pré-requisitos

- **Docker** instalado na sua máquina. [Instale Docker aqui](https://docs.docker.com/get-docker/)
- **Git** para clonar o repositório.

### Instalação e Uso

- **Obtenha as Imagens Docker:**

    - Para puxar a imagem do Flutter configurado com ASDF do Docker Hub, execute:
    ```bash
    docker pull thehprogrammer/asdf-flutter
    ```

    - Para puxar a imagem com as ferramentas do SDK do Android:
    ```bash
    docker pull thehprogrammer/sdk-config
    ```

- **Execute o Container:**

    Para iniciar um ambiente de desenvolvimento com a imagem do Flutter, execute:
    ```bash
    docker run -it --name flutter-dev thehprogrammer/asdf-flutter
    ```

   Esta ação irá inicializar um container onde você pode começar a desenvolver suas aplicações Flutter.

### Usando o Container

Após executar o container, você estará dentro do ambiente Dockerizado configurado para desenvolvimento Flutter. Aqui você pode executar comandos do Flutter, criar novos projetos e editar seus projetos existentes.

- Para criar um novo projeto Flutter:
    ```bash
    flutter create nome_do_projeto
    ```

- Para rodar um projeto Flutter:
    ```bash
    cd nome_do_projeto
    flutter run
    ```

Lembre-se de montar seu diretório de trabalho local no container usando a opção `-v` do Docker se você deseja persistir os dados ou acessar os projetos diretamente do seu sistema de arquivos local:

```bash
docker run -it -v $(pwd):/home/user/workspace --name flutter-dev thehprogrammer/asdf-flutter
cd workspace
```

### Configuração para Desenvolvimento Android e Web

Para testar aplicações Flutter para web e Android, configure o Docker para usar o Google Chrome local e para conectar dispositivos Android via USB.

#### Executando com Suporte ao Chrome e USB para Android

1. **Google Chrome Local:**

    **Para Linux:**
    ```bash
    docker run -it --name flutter-dev \
    -v /usr/bin/google-chrome:/usr/bin/google-chrome \
    -e CHROME_EXECUTABLE=/usr/bin/google-chrome \
    thehprogrammer/asdf-flutter
    ```

    **Para Windows:**
    ```powershell
    docker run -it --name flutter-dev `
    -v "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe":/usr/bin/google-chrome `
    -e CHROME_EXECUTABLE=/usr/bin/google-chrome `
    thehprogrammer/asdf-flutter
    ```

2. **Acesso a Dispositivos USB (para Android):**

    **Para Linux:**
    ```bash
    docker run -it --name flutter-dev \
    --privileged \
    -v /dev/bus/usb:/dev/bus/usb \
    -v $(pwd):/home/user/workspace \
    thehprogrammer/asdf-flutter
    ```

    **Para Windows:**
    ```powershell
    docker run -it --name flutter-dev `
    --privileged `
    -v "C:\Path\To\Your\ADB\Folder":/dev/bus/usb `
    -v "$(pwd):C:\Users\<YourUserName>\workspace" `
    thehprogrammer/asdf-flutter
    ```

#### Combinando Configurações

Para combinar as configurações de Chrome e USB no Linux:

```bash
docker run -it --name flutter-dev \
--privileged \
-v /opt/google/chrome/chrome:/opt/google/chrome/chrome \
-v /dev/bus/usb:/dev/bus/usb \
-v $(pwd):/home/user/workspace \
-e CHROME_EXECUTABLE=/opt/google/chrome/chrome \
thehprogrammer/asdf-flutter
```

Para Windows, assegure-se de ajustar os caminhos conforme necessário. O suporte para USB em Windows pode requerer configurações adicionais específicas para o sistema.

### Notas Finais

- **Segurança**: Executar containers com a flag `--privileged` pode ser arriscado, pois concede ao container acesso a todos os dispositivos do host.
- **Portabilidade**: Essas configurações são específicas para Linux e Windows. Para macOS, os caminhos e métodos podem variar. Adapte conforme necessário para seu sistema operacional.

## Contribuição

Sua contribuição é fundamental para o sucesso deste projeto! Veja nosso arquivo [CONTRIBUTING.md](CONTRIBUTING.md) para mais detalhes sobre como você pode contribuir.

## Licença

Distribuído sob a Licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais informações.

<br>

## 👨‍💻 Author

<table align="center">
    <tr>
        <td align="center">
            <a href="https://github.com/theHprogrammer">
                <img src="https://avatars.githubusercontent.com/u/79870881?v=4" width="150px;" alt="Helder's Image" />
                <br />
                <sub><b>Helder Henrique</b></sub>
            </a>
        </td>    
    </tr>
</table>
<h4 align="center">
   By: <a href="https://www.linkedin.com/in/theHprogrammer/" target="_blank"> Helder Henrique </a>
</h4>
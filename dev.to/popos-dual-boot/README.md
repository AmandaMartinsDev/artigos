![Logo do PopOS com paisagem desfocada de um porto com barcos e ilhas.](images/cover.jpg)

> Tags: #braziliandevs #popos #linux #dualboot

> Neste post vocẽ encontrará uma coleção de passos para a instalação do PopOS, de acordo com a minha utilização e preferências, com o objetivo de documentar para futuras instalações, além de ajudar e facilitar para outras pessoas desenvolvedoras de todos os níveis, que pretendem utilizar o PopOS, e/ou tenham ou pretendem ter dual-boot do PopOS com o Windows ou outras distros.

---

## 💻 Informações do sistema

- [Pop!_OS 22.04 LTS](https://pop.system76.com/)
- GNOME 42.2 com X11
- Processador: Intel Core i3
- Placa de vídeo: Intel HD Graphics
- Memória RAM: 8GB
- SSD: 240GB

---

## 💾 Partições do SSD

- (~52mb) Boot do Windows em `/dev/sda1`
- (~170gb) Partição principal do Windows 10 em `/dev/sda2`
- (~520mb) Boot do Linux `/boot` em `/dev/sda3`
- (~64gb) Partição principal do Linux `/` em `/dev/sda4`

---

## 🚀 Dual Boot do Windows com PopOS

Para realizar o Dual Boot após instalar o PopOS, você precisa ter o Windows pré-instalado no seu computador e rodar os seguintes comandos:

```bash
sudo apt install os-prober
```

Para testar, basta utilizar esse comando, ele deve retornar o Windows que você possui instalado:

```bash
sudo os-prober
```

Por padrão, o os-prober é bloqueado no PopOS, assim como em distros baseadas em Ubuntu, para ativá-lo, basta rodar o seguinte comando:

```bash
sudo gedit /etc/default/grub
```

E adicionar a linha abaixo no arquivo que será aberto para edição:

```
GRUB_DISABLE_OS_PROBER=false
```

Por fim, basta executar o seguinte comando:

```bash
sudo grub-install
```

Se tudo der certo, ao reiniciar o PC, você verá uma tela para escolher iniciar um dos sistemas.

---

## ✅ Configurações básicas

Para começar, abra as configurações do sistema e altere as seguintes opções:

- Desktop > Desktop Options:

  - Super Key Action > **Applications**
  - Top Bar > Show Workspaces Button > **Turn off**

- Desktop > Dock > 

  - Dock Options

    - Extend dock to the edges of the screen > **Turn off**
    - Show Applications Icon in Dock > **Turn off**
    - Show Launcher Icon in Dock > **Turn off**
    - Show Workspaces Icon in Dock > **Turn off**
    - Show Mounted Drives > **Turn off**
    - Icon Click Action > **Launch or Minimize Windows**

  - Dock Visibility > Show Dock on Display > **All Displays**

  - Dock Size > **Small (36px)**

---

## 📦 Instalações básicas

Primeiro, vamos atualizar o nosso sistema com seguintes comandos:

```bash
sudo apt update && sudo apt upgrade
```

Feito isso, vamos instalar um pacote completo, com várias ferramentas úteis e codecs necessários para reproduzir arquivos de mídia:

```bash
sudo apt install ubuntu-restricted-extras
```

---

## 🔑 Configurando o Git com GitHub

Primeiro, precisamos instalar o Git:

```bash
sudo apt install -y git
```

Feito isso, configure e verifique o seu nome com os comandos abaixo:

```bash
git config --global user.name "Seu Nome no GitHub"
```

Para configurar o seu email, utilize o comando abaixo:

```bash
git config --global user.email "seu@email.com"
```

Agora, para gerar a nossa chave SSH, utilize o seguinte comando:

```bash
ssh-keygen -t ed25519 -C "seu@email.com"
```

Inicialize o agente de SSH e o ambiente com o seguinte comando:

```bash
eval "$(ssh-agent -s)"
```

Adicione a chave gerada ao seu agente SSH:

```bash
ssh-add ~/.ssh/id_ed25519
```

Copie o conteúdo apresentado pelo comando abaixo da chave gerada :

```bash
cat ~/.ssh/id_ed25519.pub
```

Por fim, vá na sua conta do GitHub pelo navegador, procure por SSH and GPG keys nas configurações, crie uma chave com o título que preferir, e cole o conteúdo copiado no passo anterior.

---

##  ⚙️ Instalando o NodeJS atualizado

Primeiro adicione o nodesource com o seguinte comando:

```bash
curl -sL https://deb.nodesource.com/setup_16.x | sudo bash -
```

Feito isso, basta instalar o NodeJS normalmente:

```bash
sudo apt install -y nodejs
```

Para verificar a versão do NodeJS, basta utilizar este comando:

```bash
node -v
```

---

## ⚒️ Instalando o .NET Framework

Adicione os pacotes necessários com os comandos abaixo:

```bash
wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb; && \
  sudo dpkg -i packages-microsoft-prod.deb && \
  rm packages-microsoft-prod.deb
```

Instale o SDK e o Runtime:

```bash
sudo apt-get update; && \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-6.0 && \
  sudo apt-get install -y aspnetcore-runtime-6.0
```

---

## 🤓 Personalizando o Bash

Instale o oh-my-bash com o comando abaixo:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

Caso queira utilizar algum tema específico, vocẽ pode editar o arquivo abaixo:

```bash
gedit /home/.bashrc
```

Feito isso, basta alterar para o tema que desejar a linha abaixo, no meu caso, eu utilizo o tema `minimal`:

```
OSH_THEME="minimal"
```

---

## ✨ Bônus

Você pode fazer uma limpeza nos pacotes e dependências não utilizadas na sua máquina com os comandos abaixo:

```bash
sudo apt clean && sudo apt autoremove
```

---

## 🧰 IDEs

As minhas IDEs são da JetBrains, e para isso, eu utilizo o JetBrains Toolbox, pois é uma ótima ferramenta para instalar e manter atualizadas automaticamente todas as suas IDEs da empresa.

Para isso, basta baixar o pacote no site abaixo, extrair e executar o arquivo, ele irá instalar a toolbox, e vocẽ poderá excluir os arquivos baixados.

<https://www.jetbrains.com/pt-br/toolbox-app/>

---

## 📦 Outros softwares

- 📹 OBS Studio:

```bash
sudo apt install -y obs-studio
```

- 📢 Discord:

```bash
sudo apt install -y discord
```

- 🚀 Insomnia:

```bash
echo "deb [trusted=yes arch=amd64] https://download.konghq.com/insomnia-ubuntu/ default all" \
    | sudo tee -a /etc/apt/sources.list.d/insomnia.list; && \
   sudo apt-get update && \
   sudo apt-get install insomnia
```

- 🤪 Gitmoji CLI:

```bash
npm i gitmoji-cli
```

- 🎨 GIMP:

```bash
sudo apt install -y gimp
```

- 🗿 Blender:

```bash
sudo apt install -y blender
```

- 🕹️ Godot Engine:

<https://godotengine.org/>
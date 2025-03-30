# COMO CONFIGURAR DUAS OU MAIS CHAVES SSH PARA TER DIVERSAS CONTAS GIT NO MESMO COMPUTADOR? (WINDOWS, LINUX E MACOS)

![Banner](./images/banner.png)

- [Ver no Medium](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13)
- [Ver em ingles](README.md)

Se você já tentou gerenciar mais de uma conta no **GitHub**, **GitLab** ou qualquer outro serviço de controle de versão, sabe que pode ser um desafio. Um momento você está contribuindo para um projeto pessoal, no outro precisa fazer um commit sério na conta do trabalho, e então… ❌ *“Permission denied (publickey)”*. O Git simplesmente não sabe qual chave usar, e você fica ali, alternando contas, copiando e colando comandos ou, pior, deslogando e logando o tempo todo. 😩

Mas calma! ✋ Existe uma solução prática, elegante e definitiva: **configurar múltiplas chaves SSH** no seu computador. Assim, cada conta terá sua própria identidade, e o Git saberá exatamente qual usar em cada situação. **Sem conflitos, sem erros frustrantes e, o melhor, sem precisar repetir configurações toda hora.**

Neste guia, vamos mostrar o **passo a passo** para configurar duas ou mais chaves SSH e gerenciar diversas contas Git no mesmo computador. Seja no **Windows, Linux ou MacOS**, você vai aprender a criar, organizar e utilizar suas chaves SSH de maneira eficiente, garantindo que seus commits sempre vão para o lugar certo. ✅

Então, bora acabar com esses problemas de permissão e deixar tudo rodando suave? 🚀

---

## 📌 Sumário

🔍 **Bora ver o que você vai ver nesse guia?**

- [COMO CONFIGURAR DUAS OU MAIS CHAVES SSH PARA TER DIVERSAS CONTAS GIT NO MESMO COMPUTADOR? (WINDOWS, LINUX E MACOS)](#como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-windows-linux-e-macos)
  - [📌 Sumário](#-sumário)
  - [1. Por que você pode precisar de várias chaves SSH? :key:](#1-por-que-você-pode-precisar-de-várias-chaves-ssh-key)
  - [2️. O que são chaves SSH e como funcionam? :gear:](#2️-o-que-são-chaves-ssh-e-como-funcionam-gear)
  - [3. Pré-requisitos :computer:](#3-pré-requisitos-computer)
    - [No Windows](#no-windows)
    - [No Linux](#no-linux)
    - [No MacOS](#no-macos)
  - [4. Organização dos repositórios :package:](#4-organização-dos-repositórios-package)
    - [Importante](#importante)
    - [No Windows, Linux e MacOs (mesmo processo)](#no-windows-linux-e-macos-mesmo-processo)
  - [5. Geração das chaves SSH :lock:](#5-geração-das-chaves-ssh-lock)
    - [No Windows, Linux e MacOs](#no-windows-linux-e-macos)
  - [6. Criação dos arquivos de configuração de cada uma das contas no Git :page\_with\_curl:](#6-criação-dos-arquivos-de-configuração-de-cada-uma-das-contas-no-git-page_with_curl)
    - [No Windows, Linux e MacOs (parte comum)](#no-windows-linux-e-macos-parte-comum)
    - [No Windows](#no-windows-1)
    - [No Linux e MacOs](#no-linux-e-macos)
  - [7. Criação do arquivo de configuração geral e encaminhamento do Git :link:](#7-criação-do-arquivo-de-configuração-geral-e-encaminhamento-do-git-link)
    - [No Windows, Linux e MacOs (parte comum)](#no-windows-linux-e-macos-parte-comum-1)
    - [No Windows](#no-windows-2)
    - [No Linux e MacOs](#no-linux-e-macos-1)
  - [8. Cópia das chaves SSH para colocá-las nos serviços :cloud:](#8-cópia-das-chaves-ssh-para-colocá-las-nos-serviços-cloud)
    - [No Windows, Linux e MacOs](#no-windows-linux-e-macos-1)
  - [9. Adição das chaves SSH aos serviços (GitHub, GitLab, Bitbucket, etc) :cloud:](#9-adição-das-chaves-ssh-aos-serviços-github-gitlab-bitbucket-etc-cloud)
    - [GitHub](#github)
    - [GitLab](#gitlab)
    - [BitBucket](#bitbucket)
  - [10. Próximos passos :rocket:](#10-próximos-passos-rocket)
    - [O que é essa tal de chave GPG?](#o-que-é-essa-tal-de-chave-gpg)
    - [Vantagens de usar GPG](#vantagens-de-usar-gpg)
  - [Quem é Bruno Tanabe?](#quem-é-bruno-tanabe)

---

## 1. Por que você pode precisar de várias chaves SSH? :key:

Se você já tentou gerenciar duas ou mais contas no **GitHub, GitLab, BitBucket** ou em algum outro serviço de controle de versão na mesma máquina, provavelmente já se deparou com aquele fatídico **“Permission denied (publickey)”**. ❌ Isso acontece porque o seu computador não sabe qual chave SSH deve ser utilizada quando você tem múltiplas contas.

Agora, imagine que você tem **duas contas no GitHub**:

- 🏠 **Uma pessoal**, onde você mantém seus projetos e aquele repositório cheio de experimentos.
- 💼 **Uma do trabalho**, onde os commits precisam ser sérios e profissionais (sem *final-final-v2-AGORA-VAI* 🙈).

Outro cenário comum: você trabalha para **múltiplos clientes ou projetos** e precisa acessar repositórios em serviços diferentes, cada um com credenciais distintas. Ter chaves separadas evita dores de cabeça, já que cada conta pode ter sua própria identidade SSH **sem conflitos**. ✅

Se já passou por isso, relaxa. **Você não está sozinho!** O Git não foi feito pra lidar com múltiplas contas de maneira simples por padrão, mas a boa notícia é que **tem solução**. E não, **não precisa ficar copiando e colando chaves ou ficar deslogando e logando toda hora**. 😌

Configurar **múltiplas chaves SSH** no seu computador é o segredo para manter sua vida digital organizada, evitar erros chatos e garantir que seus commits vão para o lugar certo. **E o melhor: depois de configurar, você não precisa mais se preocupar com isso!** 🎉

Neste guia, você vai aprender a configurar tudo do jeito certo para **alternar entre contas de forma automática, sem dor de cabeça**. 🤩

---

## 2️. O que são chaves SSH e como funcionam? :gear:

Antes de sair gerando chaves e configurando tudo, vale entender rapidinho o que é **SSH** e por que ele é tão útil para o Git. 🧐

Imagine que você tem um **clube superexclusivo** e, para entrar, precisa de um convite especial que só você possui. No mundo da tecnologia, o **SSH (Secure Shell)** funciona mais ou menos assim: em vez de digitar senhas toda vez que quiser acessar um servidor ou um repositório Git, você usa um **par de chaves criptográficas** que garantem que só você tem permissão para entrar. 🔐

Esse par de chaves funciona assim:

- 🔑 **Chave privada:** Fica guardada no seu computador, como um segredo que só você conhece.
- 🔓 **Chave pública:** Vai para o servidor (**GitHub, GitLab, etc.**) e funciona como um **“cadeado”** que só pode ser aberto pela sua chave privada.

Quando você tenta se conectar, o servidor verifica se a sua **chave privada** corresponde à **chave pública cadastrada**. Se baterem, **acesso liberado!** ✅

O melhor de tudo? **Você não precisa digitar sua senha toda vez**, e o processo é muito mais seguro do que ficar armazenando senhas por aí. 🔒 Agora que você já sabe como isso funciona, bora configurar suas **chaves SSH do jeito certo**? 😃

---

## 3. Pré-requisitos :computer:

Antes de sair configurando chaves SSH, precisamos garantir que o **Git** está instalado na sua máquina. Sem ele, nada feito. Aqui vai o **passo a passo simples e sem enrolação**:

### No Windows

1. [Acesse o site oficial do **Git** na página de downloads para Windows](https://git-scm.com/downloads/win).
2. Baixe a versão correspondente do seu computador, **32-bit ou 64-bit**.
3. Depois de baixar, clique no arquivo `.exe` e execute como **Administrador**.
4. Vai abrir aquele instalador clássico cheio de “Next”. Pode ir clicando **Next, Next, Next** e aceitando tudo — as configurações padrão já funcionam bem.
5. Quando terminar, abra o terminal (**Prompt de Comando ou PowerShell**) e digite:

   ```bash
   git --help
   ```

Se aparecer uma lista de comandos do Git, **tá tudo certo!** Se der erro, tenta reiniciar o computador e roda o comando de novo. 🔄

### No Linux

1. Abra o terminal e digite:

   ```bash
   git --help
   ```

Se aparecer aquele monte de instruções e comandos do Git, **parabéns! O Git já tá instalado.** 🎉

Se o terminal reclamar que o comando não existe, é só instalar com:

  ```bash
  sudo apt install git
  ```

(Esse comando é para distribuições baseadas em Debian, tipo Ubuntu. Se for outra distro, ajusta aí pro seu gerenciador de pacotes.) 🐧

Depois disso, digita de novo `git --help` só pra confirmar. Se aparecer o textão de comandos, **sucesso** — o Git já tá na área e pronto pra ação! 🚀

### No MacOS

1. Primeiro, abre o **Terminal** (você pode buscar por “Terminal” no Spotlight ou abrir via Launchpad).
2. Digita o comando abaixo e aperta **Enter**:

   ```bash
   git --help
   ```

Se o Git já estiver instalado, ele vai mostrar aquela lista de comandos e opções — ou seja, **tá tudo certo.** ✔️

Se o terminal disser que o comando não existe ou pedir pra instalar ferramentas de linha de comando, ele provavelmente vai abrir uma janelinha perguntando se você quer instalar o **Xcode Command Line Tools**. Pode aceitar sem medo, só clicar em **Instalar** e seguir as instruções. 📲

Depois que a instalação terminar, testa de novo:

  ```bash
  git --help
  ```

Se aparecer o textão de comandos do Git, pronto! **Tá instalado.** 🎉

**Obs.:** No Mac, o Git já vem pré-instalado na maioria das versões, então pode ser que você já tenha ele sem nem saber. 😉

---

## 4. Organização dos repositórios :package:

Agora que já temos o Git instalado, vamos organizar a bagunça. A ideia aqui é simples: **criar uma estrutura de pastas no seu computador** pra separar os repositórios de cada conta Git que você usa — seja **GitHub, GitLab, Bitbucket** ou tudo junto.

Eu, por exemplo, tenho **duas contas**: uma **pessoal** e outra do **trabalho**. Então vou criar duas pastas, uma pra cada conta. Mas se você tiver três, quatro ou quinze contas (vai saber, né?), é só repetir o processo pra cada uma.

### Importante

Essa **não é a única forma** de organizar múltiplas contas Git, mas honestamente, é a forma que considero **mais prática, limpa e que evita dor de cabeça no futuro.** Dá pra usar a mesma chave SSH em duas contas? Dá. Mas **não é recomendado**. Misturar chaves pode virar uma baita confusão de permissões e segurança — sem falar que, se quiser usar chaves **GPG** depois (vou falar disso no fim do tutorial), já vai estar tudo certinho. 🔑

Eu curto criar uma pasta chamada **Workspace** na raiz do meu usuário e deixar tudo lá dentro. Mas você pode organizar do jeito que quiser, no local que quiser. 📂

### No Windows, Linux e MacOs (mesmo processo)

Vamos ao passo-a-passo. Funciona igual no **Windows, Linux e MacOs**, então aqui não tem diferença de sistema.

Nesse caso, vou mostrar como eu faço considerando a minha estrutura de pastas então faça as etapas como quiser, incluindo via interface se achar mais fácil. Se for fazer a mesma estrutura que eu, basta acompanhar as etapas abaixo.

1. No terminal, primeiro você vai para a raiz do seu usuário:

   ```bash
   cd ~
   ```

2. Agora, cria uma pasta chamada **Workspace** (ou qualquer outro nome que você preferir):

   ```bash
   mkdir Workspace
   ```

3. Entra na pasta que acabou de criar:

   ```bash
   cd Workspace
   ```

4. Agora vamos criar as pastas pra cada conta. No meu caso, vou chamar de **Personal** e **Work**, mas você pode escolher os nomes que quiser, basta saber o nome dessas pastas e onde elas estão:

   ```bash
   mkdir Personal 
   mkdir Work
   ```

Pastinhas criadas, **organização no jeito**. Assim, cada pasta vai estar na conta certa, sem risco de misturar diferentes contas em diferentes projetos, **bora criar as chaves SSH!**

---

## 5. Geração das chaves SSH :lock:

Agora chegou a hora de gerar as famosas **chaves SSH** — aquelas que vão garantir que o **Git** reconheça quem é você sem ficar pedindo senha toda hora. 🔑

Assim como na criação das pastas, você pode gerar essas chaves onde quiser, desde que depois configure certinho o caminho no arquivo do Git (lá na etapa 7).
Mas, pra manter tudo organizado e evitar dor de cabeça, eu recomendo seguir o padrão que a galera usa: guardar tudo dentro da pasta oculta **.ssh** na raiz do seu usuário. É limpo, prático e já funciona com vários serviços. 👨‍💻

Se quiser fazer diferente, tudo bem! Só não esquece de anotar o caminho e o nome das chaves, porque a gente vai precisar disso depois.

### No Windows, Linux e MacOs

Vamos ao passo a passo — assim como o passo anterior, os comandos funcionam igual no **Windows, Linux ou MacOs**:

1. Volte para a pasta raiz do seu usuário:

   ```bash
   cd ~
   ```

2. Crie a pasta **.ssh** (se ela já existir, pode pular este comando):

   ```bash
   mkdir .ssh
   ```

3. Entre na pasta **.ssh**:

   ```bash
   cd .ssh
   ```

Agora vem a parte importante: gerar uma chave SSH para cada conta que você vai usar. 🔑

No meu caso, tenho uma conta **pessoal** e outra do **trabalho**, então vou criar duas chaves. O nome dos arquivos pode ser o que você quiser — eu gosto de deixar algo que me ajude a lembrar qual é qual (mas de novo, anote ou lembre o nome e o caminho do arquivo, você vai precisar deles depois).

Para gerar a chave da conta **pessoal**:

  ```bash
  ssh-keygen -f personal_ssh_key
  ```

Para gerar a chave da conta **do trabalho**:

  ```bash
  ssh-keygen -f work_ssh_key
  ```

Quando rodar cada comando, o terminal vai perguntar se você quer colocar uma **senha** na chave. Essa senha é **opcional**. Se quiser deixar sem senha (pra não precisar digitar toda vez), só apertar **Enter** duas vezes.

O terminal vai mostrar uma mensagem parecida com essa:

  ```bash
  bruno-tanabe@Windows-Tanabe:~/.ssh$ ssh-keygen -f test_key
  Generating public/private ed25519 key pair.
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in test_key
  Your public key has been saved in test_key.pub
  The key fingerprint is:
  SHA256:cuw52mK3WSC6iCDDL2/0Hjq18lxlc9slxlIlB1uimkw bruno-tanabe@Windows-Tanabe
  The key's randomart image is:
  +--[ED25519 256]--+
  |             +.+ |
  |            . B  |
  |         E . o   |
  |       .o o o    |
  |      o SB o + . |
  |.  . o =ooo = o  |
  |+.. +...+ .. .   |
  |o+.=o+=o.+       |
  |. =+*=.o+.       |
  +----[SHA256]-----+
  ```

Cada geração de chave que você fizer irá criar **dois arquivos**:

- `sua_chave` → sua chave **privada** (não compartilhe com ninguém! 🚫)
- `sua_chave.pub` → sua chave **pública** (essa sim você vai enviar pro GitHub, GitLab, etc. 🌐)

Repita o processo para todas as contas que tiver.

Pronto! **Suas chaves SSH estão criadas** e salvas no seu computador. No próximo passo, a gente vai criar os arquivos de configuração do Git.

---

## 6. Criação dos arquivos de configuração de cada uma das contas no Git :page_with_curl:

Agora que você já criou suas pastas e gerou suas chaves SSH, vamos para a próxima etapa: **criar os arquivos de configuração** para cada conta Git que você tem.

Basicamente, cada conta vai ter um arquivo próprio com as informações dela — **nome, e-mail e qual chave SSH ela deve usar**. Isso é o que vai permitir que, na mesma máquina, você possa trabalhar com várias contas sem o Git ficar perdido sem saber quem é você. 💼

Mais uma vez: você pode criar esses arquivos onde quiser e chamar do que quiser.

Mas, pra manter a casa arrumada, eu gosto de deixá-los numa pastinha chamada **.git** na raiz do meu usuário. Então, aqui no tutorial, vamos seguir esse caminho — mas sinta-se livre pra organizar do seu jeito. 🏡

### No Windows, Linux e MacOs (parte comum)

1. Primeiro, volte pra raiz do seu usuário:

   ```bash
   cd ~
   ```

2. Crie a pasta onde vão ficar os arquivos de configuração:

   ```bash
   mkdir .git
   ```

3. Entre nessa pasta:

   ```bash
   cd .git
   ```

Agora, bora criar os arquivos de configuração. O processo muda um pouquinho dependendo do seu sistema:

### No Windows

1. Pra criar o arquivo da conta **pessoal**:

   ```bash
   echo > .gitconfig-personal
   ```

2. Abra o arquivo com o **Notepad** (ou qualquer editor que preferir):

   ```bash
   notepad .gitconfig-personal
   ```

Dentro do arquivo, cole essas informações adaptando para os dados da sua conta pessoal (Eu pedi para anotar ou lembrar o nome e o caminho do arquivo, lembra? Você vai usar eles nessa etapa e se fez como eu pedi não vai precisar voltar para consultar) 📋:

  ```ini
  [user]
      name = nome pessoal das informações da conta que você está configurando
      email = email das informações da conta que você está configurando
  [core]
      sshCommand = "ssh -i caminho_da_sua_chave_ssh/nome_da_sua_chave_ssh"
  ```

Se você está fazendo as configurações da mesma maneira que eu, vai ter um arquivo semelhante a:

  ```ini
  [user]
      name = Bruno Tanabe
      email = brunotanabe@pessoal.com
  [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
  ```

Salve e feche.

Agora, eu repetirei o processo para a minha conta do **trabalho**:

  ```bash
  echo > .gitconfig-work
  notepad .gitconfig-work
  ```

E no arquivo:

  ```ini
  [user]
      name = Bruno Tanabe Trabalho
      email = brunotanabe@trabalho.com
  [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
  ```

Salve e pronto! ✅

**Lembrete:** Você precisa de um arquivo `.gitconfig-referencia` pra **cada conta** que quiser configurar, e dentro dele vai colocar o **nome, e-mail e o caminho da chave SSH** correspondente. Assim o Git vai saber direitinho qual conta usar em cada projeto.

### No Linux e MacOs

1. Pra criar o arquivo da conta **pessoal**:

   ```bash
   touch .gitconfig-personal
   ```

2. Abra o arquivo no editor que quiser (vou usar o **Nano** aqui):

   ```bash
   nano .gitconfig-personal
   ```

Dentro do arquivo, cole essas informações adaptando para os dados da sua conta pessoal 📋:

  ```ini
  [user]
      name = nome pessoal das informações da conta que você está configurando
      email = email das informações da conta que você está configurando
  [core]
      sshCommand = "ssh -i caminho_da_sua_chave_ssh/nome_da_sua_chave_ssh"
  ```

Se você está fazendo as configurações da mesma maneira que eu, vai ter um arquivo semelhante a:

  ```ini
  [user]
      name = Bruno Tanabe
      email = brunotanabe@pessoal.com
  [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
  ```

Salve (no Nano, é **CTRL + O**, depois **ENTER** e **CTRL + X** pra sair). 💾

Agora, eu repetirei o processo para a minha conta do **trabalho**:

  ```bash
  touch .gitconfig-work
  nano .gitconfig-work
  ```

E no arquivo:

  ```ini
  [user]
      name = Bruno Tanabe Trabalho
      email = brunotanabe@trabalho.com
  [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
  ```

Salve e pronto! ✅

**Lembrete:** Você precisa de um arquivo `.gitconfig-referencia` pra **cada conta** que quiser configurar, e dentro dele vai colocar o **nome, e-mail e o caminho da chave SSH** correspondente. Assim o Git vai saber direitinho qual conta usar em cada projeto.

---

## 7. Criação do arquivo de configuração geral e encaminhamento do Git :link:

Beleza, agora que você já tem as configurações individuais de cada conta prontas, chegou a hora de amarrar tudo. Esse arquivo aqui vai ser o ponto central, o arquivo que diz pra sua máquina:

> “Ei, quando eu estiver trabalhando nessa pasta aqui, usa essa conta. Quando for naquela outra, usa a outra conta.” 📂➡️👥

Diferente dos passos anteriores, esse arquivo precisa obrigatoriamente estar na **raiz do seu usuário** e se chamar exatamente **.gitconfig** — sem firulas, sem outro nome, sem mudar de lugar.

### No Windows, Linux e MacOs (parte comum)

Primeiro, volte pra raiz do seu usuário (como sempre):

  ```bash
  cd ~
  ```

### No Windows

1. Crie o arquivo:

   ```bash
   echo > .gitconfig
   ```

2. Abra com o **Notepad** (ou qualquer editor que você goste):

   ```bash
   notepad .gitconfig
   ```

Agora, dentro do arquivo, você vai adicionar um bloco **includeIf** pra cada conta que configurou. Basicamente, você vai dizer:

“Se o projeto estiver nessa pasta, use essa configuração.” 📂⚙️

Preencha o arquivo com a localização das suas pastas e de cada um dos seus arquivos de configuração.

  ```ini
  [includeIf "gitdir:caminho_da_pasta_dos_seus_projetos_pessoais"]
      path = caminho_do_arquivo_de_configuracao_correspondente_da_pasta_pessoal
  [includeIf "gitdir:caminho_da_pasta_dos_seus_projetos_do_trabalho"]
      path = caminho_do_arquivo_de_configuracao_correspondente_da_pasta_do_trabalho
  ```

Exemplo de como deve ficar (se seguiu a estrutura que usamos até agora):

  ```ini
  [includeIf "gitdir:~/Workspace/Personal/"]
      path = ~/.git/.gitconfig-personal
  [includeIf "gitdir:~/Workspace/Work/"]
      path = ~/.git/.gitconfig-work
  ```

**Importante:**

- A pasta que você coloca no `gitdir` precisa ser exatamente a mesma que você criou lá no passo da criação dos diretórios. 📁
- O caminho no `path` precisa apontar certinho pro arquivo de configuração que você criou pra cada conta.

Salve e feche o arquivo.

### No Linux e MacOs

1. Crie o arquivo:

   ```bash
   touch .gitconfig
   ```

2. Abra com o **Nano** (ou qualquer editor de sua preferência):

   ```bash
   nano .gitconfig
   ```

Agora, dentro do arquivo, você vai adicionar um bloco **includeIf** pra cada conta que configurou. Basicamente, você vai dizer:

“Se o projeto estiver nessa pasta, use essa configuração.” 📂⚙️

Preencha o arquivo com a localização das suas pastas e de cada um dos seus arquivos de configuração.

  ```ini
  [includeIf "gitdir:caminho_da_pasta_dos_seus_projetos_pessoais"]
      path = caminho_do_arquivo_de_configuracao_correspondente_da_pasta_pessoal
  [includeIf "gitdir:caminho_da_pasta_dos_seus_projetos_do_trabalho"]
      path = caminho_do_arquivo_de_configuracao_correspondente_da_pasta_do_trabalho
  ```

Exemplo de como deve ficar (se seguiu a estrutura que usamos até agora):

  ```ini
  [includeIf "gitdir:~/Workspace/Personal/"]
      path = ~/.git/.gitconfig-personal
  [includeIf "gitdir:~/Workspace/Work/"]
      path = ~/.git/.gitconfig-work
  ```

**Importante:**

- A pasta que você coloca no `gitdir` precisa ser exatamente a mesma que você criou lá no passo da criação dos diretórios. 📁
- O caminho no `path` precisa apontar certinho pro arquivo de configuração que você criou pra cada conta.

Salve e feche (CTRL + O, depois ENTER, e CTRL + X pra sair do Nano). 💾

---

## 8. Cópia das chaves SSH para colocá-las nos serviços :cloud:

Esse passo é rapidinho: basicamente, você vai copiar a parte pública da chave SSH que criou e colar no painel de configuração do serviço que usa. 🔑💻

A chave que você precisa enviar pro serviço é sempre o arquivo que termina com **.pub** (exemplo: `personal_ssh_key.pub` ou `work_ssh_key.pub`).

### No Windows, Linux e MacOs

1. Primeiro, volte pra raiz do seu usuário (Mais uma vez):

   ```bash
   cd ~
   ```

2. Entre na pasta onde você armazena suas chaves SSH (no meu caso estão todas em uma pasta oculta **.ssh** na raiz do meu usuário, então após o comando abaixo estarei dentro dela):

   ```bash
   cd .ssh
   ```

3. Use esse comando pra exibir o conteúdo da sua chave pública e copie ele, por exemplo:

   ```bash
   cat personal_ssh_key.pub
   ```

A resposta desse comando será a sua chave pública, ela será algo como, não compartilhe essa chave com ninguém! (Não, essa não é a minha chave). 🤫

  ```txt
  ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOVd+GSxOHO0ajlagl4DnHz8rgU/Ied1uSII7a+GfeXW brunotanabe@Windows
  ```

Ou, se quiser copiar a do trabalho:

  ```bash
  cat work_ssh_key.pub
  ```

Eu recomendo que você vá copiando cada chave e adicionando ela a cada serviço correspondente, então fique alternando entre os passos 8 e 9. 🔄

---

## 9. Adição das chaves SSH aos serviços (GitHub, GitLab, Bitbucket, etc) :cloud:

Boa notícia: toda a configuração no seu computador já tá pronta! Agora falta só um detalhe pra tudo funcionar redondinho — avisar pros serviços de controle de versão (GitHub, GitLab, Bitbucket ou qualquer outro) que você tem uma chave SSH e que eles podem confiar nela. 🔑💻

Agora que você já copiou as chaves, bora colar no seu serviço favorito:

Aqui você verá como adicionar as chaves nos principais serviços de versionamento de código, mas caso use outro basta achar uma sessão semelhante e adicionar as chaves.

### GitHub

1. Acesse: [https://github.com/settings/keys](https://github.com/settings/keys)
2. Clique em **New SSH key**.
3. Dê um nome pra chave (ex: **Personal** ou **Work**).
4. Cole o conteúdo da chave pública no campo **Key**.
5. Clique em **Add SSH key**. Pronto! ✅

### GitLab

1. Acesse: [https://gitlab.com/-/profile/ssh_keys](https://gitlab.com/-/profile/ssh_keys)
2. No campo **Key**, cole sua chave pública.
3. Dê um título pra identificar (ex: **Macbook Pessoal** ou **Trabalho**).
4. Clique em **Add key**. 🔑

### BitBucket

1. Acesse: [https://bitbucket.org/account/settings/ssh-keys/](https://bitbucket.org/account/settings/ssh-keys/)
2. Clique em **Add key**.
3. No campo **Label**, dê um nome pra sua chave.
4. No campo **Key**, cole sua chave pública.
5. Salve. 💾

E pronto! Sua máquina e o serviço de controle de versão agora estão falando a mesma língua. Na próxima vez que você clonar, fazer um **push** ou **pull**, a mágica vai acontecer sem você precisar digitar senha nenhuma. ✨

**Observação**: Caso você receba o aviso abaixo ao tentar fazer a manipulação de algum repositório na nuvem, basta responder com **yes**.

```txt
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

---

## 10. Próximos passos :rocket:

Agora que você configurou tudo certinho, sua máquina já tá pronta pro jogo! Pode clonar repositório, fazer **commit**, **push**, **pull**… tudo sem senha, tudo lindo e funcionando. 🎉

Mas… (sempre tem um “mas”, né? 😉)
Algumas empresas gostam de um nível a mais de segurança e exigem que, além da autenticação SSH, você também assine seus commits com uma **chave GPG**.

### O que é essa tal de chave GPG?

Resumindo: é uma outra camada de segurança que serve pra garantir que aquele commit foi realmente feito por você e não por outra pessoa má intencionada que tem acesso ao repositório e quis se passar por você. 🔐

Quando você assina um commit com GPG, ele aparece lá no GitHub, GitLab ou Bitbucket com um selinho de **“Verified”** — tipo um **check azul** do Twitter, só que útil de verdade. ✅

### Vantagens de usar GPG

- Dá mais confiança no histórico do projeto. 📜
- Evita que alguém com acesso ao repositório faça um commit “fingindo ser você”. 🕵️‍♂️
- Algumas empresas só aceitam **PRs** com commits assinados. 🔒

Se quiser aprender como gerar, configurar e usar essas chaves GPG em múltiplas contas (seguindo essa mesma linha simples e sem enrolação), eu também escrevi um artigo no Medium só sobre isso. Tá aqui o link:

[Configuração de Chaves GPG para múltiplas contas Git (ainda em desenvolvimento)](https://medium.com/@tanabebruno)

Assim você já deixa sua máquina 100% blindada e pronta pra qualquer cenário. 🛡️

---

## Quem é Bruno Tanabe?

Se você chegou até aqui e ainda não se perguntou “quem diabos é esse cara que me fez configurar tudo isso?”, parabéns pela paciência! Mas, caso tenha ficado curioso, deixa eu me apresentar rapidinho. 👋

Sou **Bruno Tanabe**, desenvolvedor focado em backend e inteligência artificial, sempre criando soluções escaláveis e inovadoras (ou pelo menos tentando). Se curtiu o tutorial e quiser trocar uma ideia, aqui estão meus contatos:

Me encontra aqui:

- [LinkedIn](https://www.linkedin.com/in/tanabebruno/)
- [GitHub](https://github.com/BrunoTanabe)
- [Email](mailto:tanabebruno@gmail.com)
- [Medium](https://medium.com/@tanabebruno)

Agora sim, missão cumprida! 🎯

---

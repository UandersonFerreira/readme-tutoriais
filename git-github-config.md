# Introdução ao Git e ao GitHub

##  Diferenças básicas entre o Git e GitHub
1.  **Git**:
    
    -   O Git é um sistema de controle de versão distribuído.
    -   Ele permite que você rastreie as mudanças em seu código-fonte ao longo do tempo, mantendo um histórico completo das alterações.
    -   Você pode trabalhar localmente em seu computador sem estar conectado à Internet.
    -   Ele é usado principalmente por desenvolvedores para gerenciar o controle de versão de projetos de software.
2.  **GitHub**:
    
    -   O GitHub, por outro lado, é uma plataforma de hospedagem de repositórios Git na nuvem.
    -   Ele fornece uma interface baseada na web para que os desenvolvedores possam colaborar em projetos, armazenar repositórios Git, fazer o controle de versão e muito mais.
    -   Ele oferece recursos adicionais, como rastreamento de problemas (issues), pull requests, integração contínua e colaboração de equipe.
    -   O GitHub permite que você compartilhe seu código com outras pessoas e colabore em projetos de código aberto.

De forma,mais resumida, a principal diferença é que o Git é o **sistema de controle de versão** em si, enquanto o GitHub é uma **plataforma de hospedagem baseada na web que utiliza o Git para controle de versão** e colaboração em projetos de software. Existem outras plataformas de hospedagem de repositórios Git, como GitLab e Bitbucket, que oferecem funcionalidades semelhantes às do GitHub.

### Comandos básicos para um bom desempenho no terminal Linux e Windows
#####  Listagem  
	 -  Linux
		 - ls
	-  Windows
		 - dir
	
#####  navegar entre pastas
	-  Linux
		 cd caminho-do-diretório
	-  Windows
		 - dir
#####  Limpeza da tela
	-  Linux
		clear ou crtl + l
	-  Windows
		 - cls
#### Tab
- Para completar nomes quando estiver digitando no terminal de ambos OS.

#####  Criação de pastas/diretórios
	-  Linux e  Windows
		mkdir nome-da-pasta

#####  Criando um arquivo
	-  Linux e Windows (com conteúdo)
		 - echo "mensagem" > nome-do-arquivo.txt
	- Linux arquivo vazio
		- touch nome-do-arquivo
	- Windows arquivo vazio
		- type nul > nome-do-arquivo
#####  Deletar arquivos e diretório
	-  Linux
			- Arquivos
			 - rm nome-do-arquivo
		- Diretórios
			 - rmdir nome-do-diretorio (Vazio)
			 - rm -rf nome-do-diretorio

	-  Windows
		- Arquivos
			 - del nome-do-arquivo
		- Diretórios
			 - rmdir nome-da-pasta /S /Q

### Realizando a instalação do GIT no Linux

#### Adicionando o PPA do git para pegar a última versão do git
1 - `sudo add-apt-repository ppa:git-core/ppa -y`

2 - `sudo apt update`
 3 - `sudo apt install git -y`

### Objetos internos do Git

1.  **BLOBS (Binary Large Objects)**:
    
    -   Os objetos BLOBS armazenam o conteúdo real dos arquivos. Cada arquivo em um repositório Git é representado como um objeto BLOB.
    -   Os BLOBS são identificados por um hash SHA-1 exclusivo, calculado com base no conteúdo do arquivo.
    -   São imutáveis, ou seja, uma vez criados, não podem ser alterados. As alterações em um arquivo resultam na criação de um novo BLOB.
2.  **TREES**:
    
    -   Os objetos TREES representam diretórios em um repositório Git.
    -   Um objeto TREE contém referências aos BLOBS que representam os arquivos dentro desse diretório e outras árvores para representar subdiretórios.
    -   As árvores também são identificadas por um hash SHA-1 exclusivo.
3.  **COMMITS**:
    
    -   Os objetos COMMITS representam um ponto específico na história do repositório.
    -   Cada commit inclui informações como um hash para a árvore que representa o estado do projeto naquele momento, um ou mais pais (commits anteriores), uma mensagem de log e metadados do autor.
    -   Os commits também são identificados por um hash SHA-1 exclusivo.
    -   Ao contrário dos BLOBS e TREES, os COMMITS são objetos de controle de versão que mantêm uma referência à versão anterior do projeto.

Em resumo, BLOBS representam o conteúdo real dos arquivos, TREES representam a estrutura de diretórios e arquivos dentro de um diretório e COMMITS representam pontos específicos na história do projeto. Juntos, esses três tipos de objetos permitem ao Git rastrear todas as alterações feitas em um repositório, mantendo uma história completa e rastreável do projeto.


### Configurando a Chave SSH e Token
1. Criando a chave SSH com e-mail do github de preferência
 ```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Obs.: Será solicitado a criação de um senha e então será gerado duas chaves, sendo uma privada e outra pública com extensão **.pub** no nome.

2. Navegue até o diretório onde as chaves foram criadas e então liste a chave publica para pegar o SSH gerado que será exposto no gitHub.
```shell
cd /home/seu-nome-de-usuario/.ssh/
```
```shell
ls
```
Será listado as duas chaves: **id_ed25519    id_ed25519.pub**, então execute o cat é copie o SSH gerado 
```shell
cat id_ed25519.pub
```
3. com a chave em mãos acesse o github e vá em configurações ->  SSH and GPT keys é crie a chave SSH informando um nome e a chave copiada anteriormente.

4. Inicializando o ssh-agent no fundo
( em background).
```shell
eval "$(ssh-agent -s)"
> Agent pid 59566
```
5. No terminal, dentro do diretório das chaves, iremos passar a chave privada para o ssh-agent, para realizar a descriptografia de toda mensagem criptografada que for recebida.
```shell
ssh-add id_ed25519
```
Confirma com a senha gerada anteriormente e pronto a máquina está configurada para uso. basta clonar um repositório pela chave ssh e usa-lo em sua máquina. 

### Configurações Básicas do Git Localmente no Linux
```
#Seu nome completo que vai ser utilizado em qualquer commit (confirmação) recém-criado.
git config --global user.name "seu-nome"

#Seu endereço de e-mail que vai ser utilizado em qualquer commit (confirmação) recém-criado.
#DICA: recomendo você usar o seu endereço de email utilizado na autenticação do Github
git config --global user.email "your_email@example.com"

# Listar as configurações setadas
git config --list
```

### Criando um novo repositório pela linha de comando utilizando a chave SSH
```shell
echo "# readme-tutoriais" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin **chave-ssh-do-repositório-criado**
git push -u origin main
```
# Enviando um repositório existente a partir da linha de comando utilizando a chave SSH

```shell
git remote add origin **chave-ssh-do-repositório-criado**
git branch -M main
git push -u origin main
```

###  Comandos git

# Comandos Git

## `git init`
Inicialize um repositório Git em um diretório. 

```sh
git init
```
**Exemplo de uso:** Você está começando um novo projeto e deseja rastrear as alterações de código usando o Git.

---

## `git clone`
Clone um repositório Git existente para o seu computador.

```sh
git clone https://github.com/seu-usuario/seu-repositorio.git
```
**Exemplo de uso:** Você quer trabalhar em um projeto que já está no GitHub.

---

## `git status`
Verifique o status atual do seu repositório.

```sh
git status
```
**Exemplo de uso:** Antes de fazer um commit, você quer ver quais arquivos foram modificados ou adicionados.

---

## `git add`
Adicione arquivos ou alterações específicas ao próximo commit.

```sh
git add nome-do-arquivo
git add .
```
**Exemplo de uso:** Você fez alterações em alguns arquivos e está pronto para adicioná-los ao próximo commit. O segundo comando (`git add .`) adiciona todas as mudanças.

---

## `git commit`
Crie um novo commit com as alterações adicionadas.

```sh
git commit -m "Mensagem do commit"
```
**Exemplo de uso:** Você adicionou suas mudanças e agora quer criar um snapshot dessas mudanças com uma mensagem descritiva.

---

## `git pull`
Atualize seu repositório local com as alterações do repositório remoto.

```sh
git pull origin nome-da-branch
```
**Exemplo de uso:** Você quer garantir que tem as últimas alterações do repositório remoto antes de começar a trabalhar.

---

## `git push`
Envie suas alterações para o repositório remoto.

```sh
git push origin nome-da-branch
```
**Exemplo de uso:** Você terminou de trabalhar em uma feature e quer enviar suas mudanças para o repositório remoto.

---

## `git log`
Exiba o histórico de commits do seu repositório.

```sh
git log
git log --oneline --graph --decorate --all
```
**Exemplo de uso:** Você quer ver a lista de commits para entender a história do projeto. O segundo comando fornece uma visualização mais amigável.

---

## `git diff`
Mostre as diferenças entre o seu diretório de trabalho atual e a última versão commitada.

```sh
git diff
git diff nome-do-arquivo
```
**Exemplo de uso:** Você quer ver o que mudou em um arquivo específico antes de adicioná-lo ao commit.

---

## `git branch`
Liste todas as branches no seu repositório.

```sh
git branch
git branch -a
```
**Exemplo de uso:** Você quer ver todas as branches locais e remotas.

---

## `git checkout`
Mude para uma branch específica.

```sh
git checkout nome-da-branch
git checkout -b nova-branch
```
**Exemplo de uso:** Você quer começar a trabalhar em uma nova feature em uma branch separada. O segundo comando cria e muda para uma nova branch.

---

## `git merge`
Mescle alterações de uma branch para outra.

```sh
git merge nome-da-outra-branch
```
**Exemplo de uso:** Você terminou de desenvolver uma feature em uma branch separada e quer mesclar as mudanças de volta para a branch principal.

---

## `git stash`
Guarde temporariamente as alterações não comprometidas.

```sh
git stash
git checkout outra-branch # muda de branch e faz o que precisa
git checkout branch-de-trabalho # volta para a branch
git stash pop #aplica as mudanças guardadas.


```
**Exemplo de uso:** Você precisa mudar de branch rapidamente e não quer comprometer suas alterações ainda. `git stash pop` aplica as mudanças guardadas.

---

## `git remote`
Mostre os repositórios remotos configurados no seu projeto.

```sh
git remote -v
```
**Exemplo de uso:** Você quer verificar quais repositórios remotos estão configurados.

---

## `git fetch`
Baixe as últimas alterações do repositório remoto.

```sh
git fetch origin
```
**Exemplo de uso:** Você quer ver as mudanças no repositório remoto sem integrá-las imediatamente na sua branch atual.

---

## `git rebase`
Reorganize os commits.

```sh
git rebase nome-da-branch
```
**Exemplo de uso:** Você quer aplicar suas mudanças em cima das últimas mudanças de outra branch, criando uma história linear.

---

## `git cherry-pick`
Aplique um commit específico de uma branch para outra.

```sh
git cherry-pick hash-do-commit
```
**Exemplo de uso:** Você quer aplicar uma correção específica de uma branch para outra sem mesclar tudo.

---

## `git reset`
Desfaça commits anteriores ou redefina o estado do seu repositório.

```sh
git reset HEAD~1
git reset --hard HEAD~1
git reset --soft HEAD~1
```
**Exemplo de uso:** O primeiro comando desfaz o último commit mantendo as mudanças no diretório de trabalho. O segundo desfaz o commit e as mudanças. O terceiro desfaz o commit mas mantém as mudanças para serem commitadas novamente.

---

## `git tag`
Crie tags para marcar versões específicas do seu código.

```sh
git tag v1.0.0
git tag -a v1.0.0 -m "Versão 1.0.0"
```
**Exemplo de uso:** Você quer marcar um ponto específico no histórico do seu projeto, como um lançamento de versão.

---

## `git clean`
Remova arquivos não rastreados do seu diretório de trabalho.

```sh
git clean -f
git clean -fd
```
**Exemplo de uso:** Você quer remover arquivos e diretórios não rastreados para limpar seu diretório de trabalho.

---

## Aliases do Git
Configure alias personalizados para comandos Git frequentemente usados para economizar tempo.

```sh
git config --global alias.co checkout
git config --global alias.st status
git config --global alias.ci commit
```
**Exemplo de uso:** Facilita o uso de comandos frequentemente usados com nomes mais curtos. Assim, ao invés de digitar git checkout, você pode simplesmente digitar git co

    

Consultando a documentação do Git (`git --help` ou `git [comando] --help`) para obter informações detalhadas sobre cada comando e suas opções.

### Ciclo de vida de arquivos 

Status

Os status são situações (num grosso modo) que os arquivos se encontram. Esses status são:

    Untracked - O arquivo acabou de ser adicionado mas ainda não foi visto pelo Git

    Unmodifier - Quando o arquivo foi visto pelo git mas não foi modificado.

    Modified - O arquivo foi modificado.

    Staged - Área onde será criada a versão.

![Alt text](/.github/img/image.png)

Como vemos na imagem, existem regras que levam um arquivo de um status para outro. Seguindo o fluxo podemos definir como sendo:

    Untracked -> Unmodified
    Quando adicionamos um arquivo e ele é visto pelo Git e não tem modificações, ele passa a ter o status de unmodified.

    Unmodified -> Modified
    Quando qualquer alteração no arquivo é executada.

    Modified -> Staged
    Quando a modificação é salva no Git. Neste momento ela ainda não foi efetivada.

    Staged -> Unmodified
    Essa alteração se dá quando realizamos um commit, aqui um código hash da modificação é gerada e nosso arquivo está apto a receber novas mudanças do código para um novo commit.

    Unmodified -> Untracked
    Quando removemos um arquivo.

  (referência: https://dev.to/lazarocontato/git-um-breve-estudo-9gl)

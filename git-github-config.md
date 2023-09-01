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

**`git init`**: Inicialize um repositório Git em um diretório.
- `git init`

**`git clone`**: Clone um repositório Git existente para o seu computador.
   
-   `git clone https://github.com/seu-usuario/seu-repositorio.git` 
    
  **`git status`**: Verifique o status atual do seu repositório.
    
    
-   `git status` 
    
  **`git add`**: Adicione arquivos ou alterações específicas ao próximo commit.
    
    
-   `git add nome-do-arquivo` 
    
 **`git commit`**: Crie um novo commit com as alterações adicionadas.
    
    
-   `git commit -m "Mensagem do commit"` 
    
**`git pull`**: Atualize seu repositório local com as alterações do repositório remoto.
    
    
-   `git pull origin nome-da-branch` 
    
   **`git push`**: Envie suas alterações para o repositório remoto.
    
    
-   `git push origin nome-da-branch` 
    
   **`git log`**: Exiba o histórico de commits do seu repositório.
   
    
-   `git log` 
    
  **`git diff`**: Mostre as diferenças entre o seu diretório de trabalho atual e a última versão commitada.
       
-   `git diff` 
    
  **`git branch`**: Liste todas as branches no seu repositório.
    
    
-   `git branch` 
    
   **`git checkout`**: Mude para uma branch específica.
    
    
-   `git checkout nome-da-branch` 
    
   **`git merge`**: Mescle alterações de uma branch para outra.
    
-   `git merge nome-da-outra-branch` 
    
  **`git stash`**: Guarde temporariamente as alterações não comprometidas.
    
    
-   `git stash` 
    
   **`git remote`**: Mostre os repositórios remotos configurados no seu projeto.
    
    
-   `git remote -v` 
    
  **`git fetch`**: Baixe as últimas alterações do repositório remoto.
   
    
-   `git fetch origin` 
    
  **`git rebase`**: Reorganize os commits.
    
    
-   `git rebase nome-da-branch` 
    
  **`git cherry-pick`**: Aplique um commit específico de uma branch para outra.
    
    
-   `git cherry-pick hash-do-commit` 
    
   **`git reset`**: Desfaça commits anteriores ou redefina o estado do seu repositório.
    
    
-   `git reset HEAD~1` 
    
  **`git tag`**: Crie tags para marcar versões específicas do seu código.
    
    
-   `git tag v1.0.0` 
    
   **`git clean`**: Remova arquivos não rastreados do seu diretório de trabalho
    
-   `git clean -f` 
    
   **Aliases do Git**: Configure alias personalizados para comandos Git frequentemente usados para economizar tempo.


  `git config --global alias.co checkout` 
    

Consultando a documentação do Git (`git --help` ou `git [comando] --help`) para obter informações detalhadas sobre cada comando e suas opções.

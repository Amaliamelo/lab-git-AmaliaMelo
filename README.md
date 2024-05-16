Instituto de Ciências Matemática e de Computação - ICMC
Universidade de São Paulo - USP
SSC0535 - GCMES | 1o Semestre de 2024 | Profa. Dra. Lina Garcés
** Lab - Comandos básicos GIT**


**1 - INSTALAR GIT NA SUA MÁQUINA LOCAL**
- No terminal digite o seguinte comando:
      git --version

**2 - CRIAR REPOSITÓRIO REMOTO NO GITHUB**
Crie um novo repositório remoto chamado: lab-git-nomeestudante

**4 CLONAR O REPOSITÓRIO REMOTO NO REPOSITÓRIO LOCAL**
Na sua máquina, na área de trabalho (Desktop), crie uma pasta chamada lab-git-basico
para ser usada como Diretório de Trabalho Local (Working Directory).
No terminal, acesse a pasta. No ubuntu use o seguinte comando:
cd Desktop/gcmes/lab-git-basico
Copie o link do repositório (perceba que para realizar a copia, o link deve terminar com a
extensão .git ). Veja o exemplo a seguir:
No terminal da sua máquina local, estando no diretório de trabalho, digite o seguinte
comando:$ git clone https://github.com/[seu repositório]
O comando clone cria um repositório vazio na máquina local e, em seguida, copia para
esse repositório local todos os commits do repositório remoto [lab-git-seunome]. No nosso
exemplo, o repositório remoto ainda está vazio.
Você pode perceber que foi criada uma nova pasta, com o nome do repositório remoto.
Pode ser verificado que, dentro dessa pasta o git criou uma pasta oculta (.git) que será
considerada o repositório local.
Obs: não deve deletar essa pasta pois perderá o registro de todas as mudanças realizadas
nos arquivos versionados.

**5 - CONFIGURAR SUA IDENTIDADE**
Uma das primeiras coisas que você deve fazer ao instalar Git é configurar seu nome de
usuário e endereço de e-mail. Isto é importante porque cada commit usa esta informação, e
ela é carimbada de forma imutável nos commits que você começa a criar:
$ git config --global user.name "Fulano de Tal"
$ git config --global user.email fulanodetal@exemplo.br
Recomendação, use o mesmo nome de usuário e e-mail da sua conta de github.
Reiterando, você precisará fazer isso somente uma vez se tiver usado a opção --global,
porque então o Git usará esta informação para qualquer coisa que você fizer naquele
sistema. Se você quiser substituir essa informação com nome diferente para um projeto
específico, você pode rodar o comando sem a opção --global dentro daquele projeto.

**6 EXECUTANDO O WORKFLOW COM REPOSITÓRIO REMOTO**
Suponha que você está trabalhando num projeto na linguagem C, e precisa criar um
programa que dado um intervalo de números inteiros, [x,y] calcule diversas operações
matemáticas, por exemplo, somatória dos inteiros no intervalo [x,y]
Após criar o arquivo, no terminal, dentro do seu diretorio de trabalho, digite o comando
$ git status
Isso significa que você está no branch main do seu repositório local, porém o arquivo main.c
não está na staged área, ou seja as mudanças deste arquivo ainda não estão sendo
controlado (tracked).
Nesse caso, precisamos adicionar o arquivo à staged área, antes de registrar as mudanças
no repositório local, como mostra o seguinte workflow:
Para isso, no terminal, no seu diretório de trabalho, digitar o seguinte comando:
$ git add main.c
Para conhecer o novo estado do arquivo main.c, digitar:
$ git status
O git está informando que um novo arquivo, main.c, foi mudado e as mudanças podem ser
registradas no repositório local.
Neste passo, o arquivo main.c passou do estado modified para o estado staged
Para guardar as mudanças do arquivo no repositório local, basta usar o seguinte comando:
$ git commit -m “criacao do arquivo main.c”
A opção -m informa a mensagem que descreve o commit.
Neste passo, o arquivo passou do estado staged para o estado commited
Para conhecer o novo estado do arquivo, digitar:
$ git status
Assim, é possível verificar que não há mudanças em espera de serem mudadas para o
estado commited no main do repositório local.

Agora, vamos adicionar mais linhas de código no arquivo main.c
Execute novamente o comando status para conhecer o estado do projeto
$ git status
A primeira mensagem ‘Your branch is based on 'origin/main', but the upstream
is gone’ significa que o branch ‘main’ do repositório remoto ‘origin’ (github) está
desatualizado, pois ainda não enviamos as mudanças para o repositório remoto.
A segunda mensagem ‘Changes not staged for commit’ significa que as mudanças do
arquivo main.c precisam ser incluídas na staged area
Para acelerar o trabalho, vamos usar o seguinte comando que permite adicionar as
mudanças na staged area e registrar as mudanças no repositório local.
$ git commit -a -m 'Adicionando a funcao soma(x,y)'
A opção -a indica que antes de executar o commit queremos adicionar na staged area
todos os arquivos rastreados (tracked) que tenham sido modificados desde o último commit.
Obtemos o seguinte resultado
Para termos noção do histórico das mudanças registradas no repositório local, podemos
executar o seguinte comando:
$ git log
Por enquanto, o histórico de mudanças para o nosso projeto vai apresentar a lista com os
dois commits realizados.

Modifique mais uma vez o arquivo main.c com as seguintes mudanças:
Execute o seguinte comando:
$ git diff
Perceba que em vermelho estão as linhas de código que foram deletadas (-), e em cor
verde estão as linhas de código adicionadas (+) no arquivo
Verifiquemos de novo o estado das mudanças do nosso arquivo
Percebemos que as últimas mudanças não estão registradas no repositório local. Dessa
forma, necessitamos adicionar as mudanças na staged area e realizar o commit para o
repositório local, como mostrado a seguir.

**6.1 PUBLICANDO AS MUDANÇAS NO REPOSITÓRIO REMOTO**
Antes de realizar mudanças no repositório remoto, você precisa configurar os tokens de
autenticação. 

**ENVIANDO MUDANÇAS NO REPOSITÓRIO REMOTO (GITHUB)**
O comando PUSH “empurra” os commits mais recentes do repositório local para o
repositório remoto.
O comando tem a seguinte sintaxe: git push <remote> <branch>
Sendo que:
<remote> é o repositório remoto, clonado, chamado repositório de origem (origin)
<branch> é a branch local que você deseja enviar para o repositório remoto, que no
nosso caso é a branch main
Sendo assim, para nosso exemplo iremos usar o seguinte comando que atualiza o
repositório remoto:
$ git push origin main
Atenção! Como sehna (password), utilizar o token gerado anteriormente.
Você pode conferir no repositório remoto do github as mudanças enviadas. Por exemplo, na
seguinte imagem podemos ver o arquivo main.c com a mensagem do último commit.
Destaca-se que as mudanças foram realizadas no branch main, pois nosso projeto somente
tem 1 branch.
Ao clicar nos commits podemos acessar a lista de commits realizados:
Ao clicar no último commit (5a4afec) é possível ver as mudanças do arquivo enviadas para
o repositório remoto naquele commit, como a seguir.
É possível observar as linhas que foram adicionadas (em cor verde) e as que foram
deletadas (em cor vermelho) nesse commit.
**6.2 TRABALHANDO COM BRANCHES**
Suponha que para o programa main.c é necessário criar uma nova função que calcule a
produtória dos números inteiros no intervalo [x,y], porém você precisa ter certeza da sua
implementação antes de realizar o commit do novo programa no branch main.
Nesse caso, recomenda-se criar um novo branch de desenvolvimento.
Antes de tudo, precisa ter certeza que os branch main do seu repositório local e remoto
estão sincronizados. Para isso usamos o comando git status
Como resultado temos que, os dois branches, o origin (main no github) e o main local,
estão atualizados.
A seguir, iremos criar um novo branch para desenvolver a nova função de forma local. Para
isso usamos o seguinte comando:
$ git branch produtoria
Agora, atualizamos o repositório remoto (origin) com o novo branch (produtoria), usando o
comando push, como ilustrado na seguinte imagem:
Obs: Usar o token gerado anteriormente como senha.
Ao clicar na branch produtora, é possível ver que ela contém uma cópia fiel do arquivo
main.c
No terminal, no repositório local, para realizarmos as mudanças no código do arquivo
main.c sem afetar a versão atual que está publicada no branch main, precisamos trocar
para o branch produtoria. Para isso, usamos o comando checkout:
$ git checkout produtoria
Para verificar o branch em que estamos trabalhando atualmente podemos usar o comando:
$ git branch
Como mostrado na seguinte imagem, nosso projeto tem 2 branches, o main e o produtoria.
Sendo que estamos trabalhando atualmente no branch produtoria, destacado em cor verde
e com o simbolo *
Modifique o arquivo main.c 
Verifique as novas mudanças realizadas no arquivo usando o comando $git diff
Verifique o estado do arquivo main.c usando o comando $ git status
As mudanças ainda não estão na staging area, então é preciso realizar a adição das
mudanças e após isso registrar as mudanças no repositório local, como mostrado a seguir:
$ git commit -a -m 'Primeira versao da funcao produtoria'
Verificar o estado das mudanças usando o comando $ git status
Podemos observar o seguinte.
- O branch produtoria local está diferente (a frente - ahead ) do branch produtoria
remoto
- Todas as mudanças no arquivo main.c no branch produtoria local estão na staged
area.
Para sincronizar o branch produtoria remoto com as últimas mudanças, usar o comando
PUSH para enviar as mudanças do branch local (produtoria) ao branch produtora do
repositório remoto (origin)
$ git push origin produtoria
Observe que o github destaca que a versão do arquivo main.c do branch produtoria está
ahead, ou seja à frente, da versão atual do arquivo main.c no branch main.
Agora, suponha que você testou o código e este funciona corretamente. No repositório
local, precisamos atualizar (merge) o branch main com a nova funcionalidade. Para isso
executamos o seguinte.
Trocar para a branch main usando o comando $ git checkout main
Verificar o branch corrente com o comando $ git branch
Estando no branch main precisamos usar o comando merge que realiza uma cópia de um
branch no branch main.
No nosso caso, iremos copiar a versão que está no branch produtoria para o branch main,
usando o seguinte comando:
$ git merge produtoria
Lembre-se que você já tinha trocado para o branch main.
Como o merge foi realizado no main do repositório local, precisamos publicar as
atualizações no repositório remoto (origin). Para isso usamos o comando
$ git push origin main
No repositório remoto, podemos observar que, o branch produtoria e o branch main estão
atualizados (up to date)
A seguinte figura sumariza o workflow usado neste exercício:

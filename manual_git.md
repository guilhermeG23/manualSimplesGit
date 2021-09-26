### Manual de GIT

Git é um sistema de versionamento de projetos, criado por Linus Torvales durante o desenvolvimento do kernel Linux, esta é uma ferramenta para gerenciar os projetos e suas versões.

#### Outros sistemas de versionamento 

* CVS
* SVN
* Mercurial

E demais outros.

---

#### Níveis

* HEAD: Estado atual do nosso código, ou seja, onde o Git os colocou;

* Working tree: Local onde os arquivos realmente estão sendo armazenados e editados;

* index: Local onde o Git armazena o que será commitado, ou seja, o local entre a working tree e o repositório Git em si.

---

#### Comandos

---

Iniciar um versionamento de um diretorio:

```
git init .
```

Criando o versionamento dentro do diretorio atual

---

Mostra os status dos arquivos no repositorio

```
git status
```

---

Adicionar um arquivo ao versionamento:

```
git add file
```

---

Remover um arquivo do versionamento:

```
git rm file
```

---

Efetiver alterações de um arquivo:

```
git commit -m "Efetiva alteracoes dos arquivos, caso não tiver o -m, ele vai abrir uma linha para esse edicao"
```

A linhas tem de ser curtas e descritivas.

---

Mostrar o histoórico de alterações do repositorio

```
git log
```

Para uma forma mais resumida, use:

```
git log --oneline
```

Para mostrar como uma linha de produção, use:

```
git log --graph
```


---

Configuração LOCAL e GLOBAL:
* Local -> Somente válido ao repositório atual com o init;
* Global -> Valido a todos os repositórios;

---

Arquivo de configuração para ignorar demais outros arquivos do repositorio, o ```.gitignore```.

Dentro do ignore, coloque os arquivos que você deseja não monitorar.

---

Um repositório para servir:
```
git init --bare
```

---

Conectar um diretorio a um repositorio remoto
```
git remote add <nome/alias> <endereço>
```

Para listar os diretorios remotos é só fazer:
```
git remote
```

Ex:
```

C:\Users\guilherme\Desktop>mkdir teste
C:\Users\guilherme\Desktop>cd teste

C:\Users\guilherme\Desktop\teste>mkdir t1

C:\Users\guilherme\Desktop\teste>mkdir t2

C:\Users\guilherme\Desktop\teste>git init --bare t2
Initialized empty Git repository in C:/Users/guilherme/Desktop/teste/t2/

C:\Users\guilherme\Desktop\teste>git init t1
Initialized empty Git repository in C:/Users/guilherme/Desktop/teste/t1/.git/

C:\Users\guilherme\Desktop\teste>cd t1

C:\Users\guilherme\Desktop\teste\t1>git remote add remotot2 C:/Users/guilherme/Desktop/teste/t2/

C:\Users\guilherme\Desktop\teste\t1>git remote
remotot2

C:\Users\guilherme\Desktop\teste\t1>git remote -v
remotot2        C:/Users/guilherme/Desktop/teste/t2/ (fetch)
remotot2        C:/Users/guilherme/Desktop/teste/t2/ (push)
```


---

Clonar um repositorio, Ex:
```
git clone <endereco> <nome_do_projeto>
```

---

Renomear um remote:
```
git remote rename <nome atual> <novo nome>
```

---

Obter os arquivos dos repositorios remotos:
```
git pull <nome do remote> <branch>
```

---

Branchs são linhas de trabalho, para ver a linha que está trabalhando, use:
```
git branch
```

Para criar uma linha, use:
```
git branch <nome da branch>
```

E para alterar entre as linhas, use:
```
git checkout <branch>
```

Criar uma branch e já trocar para ela:
```
git checkout -b <nome da branch>
```

---

Juntar linhas de trabalho, use:
```
git merge <nome da branch>
```

Isso é, sua branch atual vai receber todo o conteudo da branch alvo a partir do ultimo ponto do alvo, lembrando que, se houver alterações em mesmo ponto, haverá conflitos que necessitaram alterações para serem solucionados antes do merge definitivo.

Lembrando que o branch mergeado não é apagado.

Ex:
```
C:\Users\guilherme\Desktop\teste\t1\t2>git checkout -b segunda_linha
Switched to a new branch 'segunda_linha'

C:\Users\guilherme\Desktop\teste\t1\t2>git branch
  master
* segunda_linha

C:\Users\guilherme\Desktop\teste\t1\t2>echo "1111" >> teste_file

C:\Users\guilherme\Desktop\teste\t1\t2>
C:\Users\guilherme\Desktop\teste\t1\t2>
C:\Users\guilherme\Desktop\teste\t1\t2>git status
On branch segunda_linha
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   teste_file

no changes added to commit (use "git add" and/or "git commit -a")

C:\Users\guilherme\Desktop\teste\t1\t2>git commit -am "Adicionado linhas"
[segunda_linha d04e60f] Adicionado linhas
 1 file changed, 1 insertion(+)

C:\Users\guilherme\Desktop\teste\t1\t2>git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

C:\Users\guilherme\Desktop\teste\t1\t2>git merge segunda_linha
Updating ffb8028..d04e60f
Fast-forward
 teste_file | 1 +
 1 file changed, 1 insertion(+)

C:\Users\guilherme\Desktop\teste\t1\t2>git branch
* master
  segunda_linha

C:\Users\guilherme\Desktop\teste\t1\t2>git log --oneline
d04e60f (HEAD -> master, segunda_linha) Adicionado linhas
ffb8028 (origin/master) Nova linha
e466872 teste feito
```

---

Uma forma de evitar o uso constante do merge é usando o rebase, Ex:
```
git rebase <branch>
```

O rebase move o branch alvo para dentro do branch atual, é como se você colocar o master na frente de todos os commits de uma branch alvo, ele vai carregar todas as alterações do alvo, más já com o master na frente; 


Ex:
```
C:\Users\guilherme\Desktop\teste\t1\t2>git branch
* master
  segunda_linha

C:\Users\guilherme\Desktop\teste\t1\t2>git checkout segunda_linha
Switched to branch 'segunda_linha'

C:\Users\guilherme\Desktop\teste\t1\t2>echo "teste1" >> teste_file

C:\Users\guilherme\Desktop\teste\t1\t2>git status
On branch segunda_linha
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   teste_file

no changes added to commit (use "git add" and/or "git commit -a")

C:\Users\guilherme\Desktop\teste\t1\t2>git commit -am "Atualizando"
[segunda_linha 8304b2a] Atualizando
 1 file changed, 1 insertion(+)

C:\Users\guilherme\Desktop\teste\t1\t2>git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

C:\Users\guilherme\Desktop\teste\t1\t2>git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

C:\Users\guilherme\Desktop\teste\t1\t2>git rebase segunda_linhas
fatal: invalid upstream 'segunda_linhas'

C:\Users\guilherme\Desktop\teste\t1\t2>git rebase segunda_linha
Successfully rebased and updated refs/heads/master.

C:\Users\guilherme\Desktop\teste\t1\t2>git log --oneline
8304b2a (HEAD -> master, segunda_linha) Atualizando
d04e60f Adicionado linhas
ffb8028 (origin/master) Nova linha
e466872 teste feito
```

---

O ctrl + Z do git


Retornar o estado de um arquivo não commitado para como ele está no ultimo commit, Ex:
```
git checkout -- <arquivo>
```

Tirar um ADD de um arquivo e voltar para o estado de HEAD, use:
```
git reset HEAD <arquivo>
```

O ```HEAD``` é o estado que o arquivo deve retornar.


Agora tem o reverter de um commit, ex:
```
git revert <log de um commit>
```

Ex:
```
git revert 8304b2aba95959ccae0ac9b64bc614153bfb16af
```

Ele gera um log de retorno de commit.


---

#### Área temporaria

Guardar alteração de forma temporaria, Ex:
```
git stash
```

Listar os stash's criados:
```
git stash list
```

Para aplicar as modificações em stash, use:
```
git stash apply <numero da stash iniciando do 0> 
```

Lembrando, mesmo dando apply, ela ainda existe na stash, tem que remover depois.

Par aplicar o ultimo stash e deletar ele, use:
```
git stash pop
```

Para deletar uma stash, faça:
```
git stash drop <numero da stash iniciando do 0> 
```

---

#### Diferença entre commits

Existe o comando ```diff``` no linux que mostra as diferenças entre arquivos, sendo assim, existe no git, ex:

```
git diff <commit> <commit>
```

---

#### Criar uma marcação entre os commit's

Tag são pontos "fixos" dentro dos commits, onde você sabe que determinado código estará de determinada forma.

```
git tag -a <nome da tag> "mensagem opcional da tela"
```

A tag vira um marco, permitindo usar ela para fazer pull e push.

---

#### Unindo commits

Isso é feito para facilitar a verificação dos commits realizados do projeto:

```
git rebase -i HEAD~<commit alvo ou valor>
```

O HEAD é o commit atual e o alvo é o número de commit's realizados até o HEAD ou a chave do log do commit.

Após isso, vai ser aberto uma área para editar, onde vai ter escrito no topo os commit's com o ```pick``` na frente, o ```pick``` deve ser único por motivos que ele via o commit principal, o restante deve substituir por ```s```

---

#### Boas práticas

Boas práticas sobre o uso do commit:

* Nunca commit código que não funcione;
* Só faça isso quando algo é implementado ou alterado com sucesso;
* Sempre tenha o code final na master/main, sempre use outras linhas para fazer o gerenciamento;
* Se um problema aparece na master/main e ele é urgente, não altere, crie uma branch chamada de hotfix/<versao do desenvolvimento ou um nome especifico> para a correção, o merge tambem não é feito direto e sim numa branch de desenvolvimento que irá fazer merge a principal.

---

#### Github Issues

Na tradução literal é a lista de problemas, lá se registra problemas, reports e demais mesmo que você não seja um ativo dentro do projeto, é uma forma de contribuição.

---

#### Fork

Fork é a cópia de um projeto já postado, podendo ser usado pelo usuário que realizou o FORK sem restrições e com possibilidade de devolver essas alterações até o projeto original.

A forma de devolução é com ```PULL REQUEST```, onde o fork será enviado para análise do criador do repositório

---

#### Trazer alterações para o HEAD com base em um commit 

O comando ```cherry-pick``` é usado para trazer alterações direto para o HEAD (Atual linha de produção), Ex:

```
git cherry-pick <commit>
```

---

#### Bisect

Mostar diferenças exatas ente commits, Ex:

```
PS C:\Users\guilherme\Desktop\teste\t1\t2> git bisect start       

PS C:\Users\guilherme\Desktop\teste\t1\t2> git bisect bad HEAD    

PS C:\Users\guilherme\Desktop\teste\t1\t2> git bisect good ed6bbcb
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[772983ae7b56d03fadf98b6adbbac21d9ee30edb] teste atual

PS C:\Users\guilherme\Desktop\teste\t1\t2> git bisect bad


PS C:\Users\guilherme\Desktop\teste\t1\t2> git bisect good 
772983ae7b56d03fadf98b6adbbac21d9ee30edb was both good and bad

PS C:\Users\guilherme\Desktop\teste\t1\t2> git bisect reset
Previous HEAD position was 772983a teste atual
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 8 commits.
  (use "git push" to publish your local commits)
```

O bisect retornar o code a um estado de commit anterior, todo o BAD é que a alteração de determinado commit não está valendo, más quando der um good, esse é o commit alvo, para retonar o code da forma que era antes da pesquisa, é só dar um reset e pronto, o code retorna ao estado de commit atual.

---

#### Historico de quem fez

Mostra informações de quem fez algo, quando e oq fez, ex:

```
PS C:\Users\guilherme\Desktop\teste\t1\t2> git blame .\teste_file
^e466872 (guilhermeG23 2021-09-12 19:29:43 -0300 1) "" 
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 2) "teste"
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 3) "1111"
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 4) "teste1"
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 5) ""
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 6) ""
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 7) ""
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 8) ""
772983ae (guilhermeG23 2021-09-18 19:43:48 -0300 9) ""
```

--- 

#### Hora do show

Show é um comando que mostra alteração realizadas num determinado commit, Ex:

```
PS C:\Users\guilherme\Desktop\teste\t1\t2> git show b3b5736
commit b3b5736830a012479a13693bb530652cd426e527 (HEAD -> master)
Author: guilhermeG23 <guilhermebrechot@gmail.com.br>
Date:   Wed Sep 22 21:20:49 2021 -0300

    teste1

diff --git a/teste_file b/teste_file
index c382c58..1cc3227 100644
--- a/teste_file
+++ b/teste_file
@@ -1,6 +1,4 @@
 ""
-<<<<<<< HEAD
-=======
 "teste"
 "1111"
 "teste1"
@@ -9,4 +7,3 @@
 ""
 ""
 ""
->>>>>>> 873f5be (teste teste 1)
```

---

#### Organização com Git-Flow

Forma de organizar a linha de produção das branch;

* Master/main -> Linha produção;
* Hotfix -> Correções da principal, ele é gerado por um erro na master e quando corrigido, a master e o develop recebem um merge para se atualizarem;
* Develop -> Ambiente de testes;
* Features -> Novos implementações ao ambiente de teste;
* Release -> Momento que sai do Dev e vai para o principal, é a linha de testes e correções finais antes do merge a principal, qualquer alterações aqui vão tanto para a master quando para o develop, forá que a mesmasó existe durante a versão, a cada nova tag de versão a mesma é renovada;

![FLOW](flow.png)

---

#### Hooks

Hooks fica dentro de o .git, eles são ações dentro do git, dentro dos hooks, existem vários arquivos com nomes descritivos, Ex:

```
C:\Users\guilhermebrechot\Desktop\manual_git\.git\hooks>dir
applypatch-msg.sample
commit-msg.sample
fsmonitor-watchman.sample
post-update.sample
pre-applypatch.sample
pre-commit.sample
pre-merge-commit.sample
pre-push.sample
pre-rebase.sample
pre-receive.sample
prepare-commit-msg.sample
push-to-checkout.sample
update.sample
```

Para eles funcionarem, tem que tirar o ```.sample``` e alterar a permissão para executar.

Exemplo de deploy
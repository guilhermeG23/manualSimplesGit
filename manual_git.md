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



---

#### Boas práticas

Boas práticas sobre o uso do commit:

* Nunca commit código que não funcione;
* Só faça isso quando algo é implementado ou alterado com sucesso;

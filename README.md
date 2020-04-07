# Oficina de Git

Nessa oficina assumimos que o git já está instalado. Se não for o caso, consulte as referências para descobrir como instalar para o seu sistema.

## O que é git?

`git` é uma ferramenta de controle de versão. Tá, mas o que é controle de versão?

Pense na seguinte situação: você está trabalhando em um texto, editando, editando, apaga um pedaço, edita mais. Depois de um tempo você pensa: putz, aquele pedaço que eu apaguei tinha um trecho que eu queria pegar de volta pra usar agora. Como você faz? Aperta ctrl+z até recuperar o que apagou e torce pra não perder todo o trabalho que você fez por acidente? E se você tiver fechado o editor e não der mais pra usar o ctrl+z, já era?

Ferramentas de controle de versão permitem que você "salve" o seu trabalho várias vezes ao longo do caminho. Isso permite que você veja progresso, veja histórico e recupere qualquer ponto no passado do projeto a qualquer momento. No exemplo do texto, se você estivesse usando `git`, teria vários `commits` ao longo do caminho e poderia olhar o commit que tinha o texto que você apagou sem se preocupar em perder seu trabalho.

## Comandos básicos

Pra começar a trabalhar com git, você precisa de um `repositório`. Um repositório é uma pasta que o `git` vai monitorar para poder reconhecer alterações.

### git init

Para usar o git em uma pasta e tratá-la como repositório, use o comando `git init`:

```
cd ~/oficina-git
git init
```

Uma mensagem aparecerá:

> Initialized empty Git repository in /tmp/oficina-git/.git/

### git add e git status

Se eu edito um arquivo ele automaticamente entra pro git? Não, você precisa pedir para _trackear_ este arquivo, ou seja, adicionar ele ao git. E como eu sei se um arquivo está no git ou não? Use o comando `git status`:

![git status](./img/git-status.png)

Nesse exemplo existe um arquivo chamado `teste`, com o nome em vermelho no print, que o git não conhece. Veja que ele aparece na seção _Untracked files_, ou seja, arquivos não trackeados.

Para adicionar, use o comando `git add`:

![git add](./img/git-add.png)

A partir daqui o git vai saber que o arquivo `teste` existe e caso você faça novas alterações ele vai mostrar no `git status` que o arquivo tá modificado.

### git commit

Então blz, adicionei o arquivo `teste` e ele agora está salvo naquele histórico, né? Ainda não.

Pra isso, precisamos usar o `git commit`. O comando commit é o que realmente grava uma versão. O `git add` basicamente diz ao git: acompanha esse arquivo aqui, pega essas mudanças que eu fiz nele. O que o commit faz é um ctrl+s, ou seja, ele salva a versão atual.

```
git commit -m "Commitar arquivo teste"
```

Aqui, se você rodar o `git status` ele vai dizer que está tudo limpo e não há nada modificado no seu repositório.

### git log

Para ver o commit que você fez, use o git log:

![git log](./img/git-log.png)

Conforme você for avançando no projeto e fazendo novos commits o `git log` vai ficando mais longo e vai mostrando tudo que você fez no meio do caminho. Dá para entrar em qualquer commit e ver como eram os arquivos do seu repositório naquele momento no tempo.

Usar o git te permite viajar no tempo!

![back to the future](./img/back-to-the-future.jpg)

## Commit early, commit often

Uma boa prática no uso do git é commitar cedo e commitar com frequência. Ou seja, se você fez alterações no seu repositório e salvou já vale a pena commitar. Não espere para terminar algo grande, salve no meio do caminho e vá fazendo vários commits no meio do caminho.

Mais commits nunca é uma coisa ruim. Fica fácil de entender o passo a passo do projeto, fica fácil de voltar atrás, de consultar uma coisa que você fez antes, é sempre bom.

Commite cedo e commite com frequência!

## Remotes

Toda essa viagem no tempo é linda, mas só está acontecendo na sua máquina até agora. E se eu quiser trabalhar nesse repositório junto com outra pessoa, como eu faço? Crio um arquivo .zip e mando pra ela por email? E se depois disso nós duas fizermos alterações, como que a gente junta o que todo mundo fez?

Felizmente, temos uma opção melhor: usar _remotes_. Um remote é só uma cópia do seu repositório em outra máquina. O git é capaz de reconhecer vários remotes e entender que eles estão trabalhando no mesmo repositório, o que facilita a integração entre as mudanças feitas em vários lugares diferentes.

E é aí que entra o github.

### Github

O [github](github.com) é o maior e mais famoso _remote_ de git que existe. Ele funciona como uma enorme máquina que contém remotes de vários repositórios e de várias pessoas, é como se fosse um repositório central de git.

Além disso, ele também funciona como uma rede social, facilita com que pessoas trabalhando nos mesmos repositórios compartilhem seu código e tem muitas funcionalidades além disso, como repositórios privados, organizações, controle de acesso para definir quem pode mexer no quê e muito mais.

### git e github é a mesma coisa?

`git` é a ferramenta de linha de comando. `github` é o site pra onde nós podemos enviar as nossas mudanças e compartilhá-las com o mundo.

É comum confundir os dois mas se lembre que nós começamos a usar o `git` antes de falar sobre o `github`, o `git` é uma ferramenta independente, você pode usar ele só localmente e nunca pensar no github ou pode usar outros sites concorrentes do github também, como o [bitbucket](https://bitbucket.org/) ou o [gitlab](https://gitlab.com).

### git clone

Para trabalhar localmente com um repositório remoto, precisamos usar o comando `git clone`. O git clone faz download de um repositório git que está em outro lugar e copia ele para a sua máquina. Por exemplo, para clonar esta oficina aqui, rode:

```
git clone https://github.com/vdemario/oficina-git.git
```

O repositório `github.com/vdemario/oficina-git` é público, então você pode fazer uma cópia dele à vontade, inclusive se você não tiver uma conta no github.

### git push

Ok, fiz várias alterações no meu código, commitei várias vezes, tenho todo um histórico bonitinho do meu trabalho. Agora eu quero mandar isso pro github pra poder pegar o código em outra máquina e continuar trabalhando. Ou eu quero mandar para o github pra poder mostrar pra outra pessoa o que eu fiz e trabalharmos juntos. O comando que você precisa usar para isso é o `git push`.

```
$ git push
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 825 bytes | 825.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/vdemario/oficina-git.git
   cba46b1..45b0928  master -> master
```

Em geral, você não precisa se preocupar muito com os detalhes que o `git push` te dá, mas é importante ler principalmente o final do texto pra saber se deu tudo certo ou se um erro aconteceu. Nesse exemplo, repare na frase _completed with 1 local object_. Isso significa que o `git push` completou e conseguiu enviar dados para o repositório remoto, ou seja, para o github.

Na primeira vez que você quiser fazer push para o github, você precisa configurar a conexão entre o seu `git` local e a sua conta no `github`, para o github saber que o push que ele está recebendo vem da pessoa certa. Existem muitas formas de fazer isso que estão bem documentadas no [GitHub Help](https://help.github.com/en/github/getting-started-with-github/set-up-git#next-steps-authenticating-with-github-from-git).

### git pull

O `git pull` é o inverso do `git push`. Quando existem novas alterações no remote/github você pode usar o `git pull` pra baixar essas alterações para o seu repositório local. Isso é muito útil quando você trabalha em várias máquinas ou para quando várias pessoas trabalham no mesmo repositório.

## Outras partes interessantes

### .gitignore

Caso você queira ter alguns arquivos na sua pasta que não entrem no git você pode criar um arquivo chamado `.gitignore` e listar nele os tipos de arquivos ou pastas que você quer que o git ignore. É muito útil para ignorar pastas como o `node_modules` ou arquivos criados automaticamente por ferramentas, como arquivos com extensão `.pyc` pra quem trabalha em python e pastas com configurações de editores como `.vscode/` ou `.idea/`.

### git config

O git config tem várias configurações que podem ser globais (valem pro ambiente inteiro) ou locais (valem só para o repositório). Um dos usos mais comuns do git config é definir o nome e o email que aparecem nos commits. Funciona assim:

```
git config --global user.name "Meu Nome"
git config --global user.email meuemail@exemplo.com.br
```

## Seção bônus: branches

Está tudo indo bem e você já está super acostumada a fazer commits, dar push para mandar o seu repositório para o github e já começou a trabalhar junto com outras pessoas inclusive. A colaboração tá indo bem e vocês decidiram se dividir pra fazer partes diferentes do seu projeto, tem duas telas e a pessoa A vai fazer a tela 1 enquanto a pessoa B vai fazer a tela 2.

Vocês vão fazendo o passo a passo de cada tela, commitando e fazendo push, mas começa a ficar difícil trabalhar juntas pq estão modificando em paralelo o projeto com dois objetivos diferentes. As duas pessoas adicionam funções no fim de um arquivo por exemplo e as alterações de vocês estão atrapalhando o trabalho uma da outra.

Tem um jeito melhor de trabalhar assim: branches! Um branch é uma espécie de versão paralela do código do projeto. Até agora nós sempre trabalhamos em um branch chamado `master`. O `master` sempre existe e ele é o ponto central do projeto. Agora, na hora de colaborar, a pessoa A pode abrir um branch chamado `tela-1` e a pessoa B pode abrir um branch chamado `tela-2` e cada uma vai fazer commits para o seu branch sem ninguém atrapalhar ninguém. Depois as alterações vão para o master e aí são integradas no trabalho de todo mundo.

### git branch

Para ver quais branches existem no seu repositório local, rode o comando `git branch`:

```
$ git branch 
* master
  tela-1
```

Na primeira vez que você rodar, só vai aparecer o branch master.

### git checkout

O comando `git checkout` tem várias funções, inclusive a de criar um novo branch:

```
$ git checkout -b tela-2
Switched to a new branch 'tela-2'
```

Repare no parâmetro `-b` do `git checkout`, é ele que faz um novo branch ser criado.

Agora se você rodar o `git status` ele vai dizer que você está no branch `tela-2`:

```
$ git status
On branch tela-2
```

E o `git branch` vai mostrar o seu novo branch na lista:

```
$ git branch 
  master
  tela-1
* tela-2
```

Para trocar de um branch para outro use o comando `checkout` sem o parâmetro `-b`:

```
$ git checkout master
Switched to branch 'master'
```

### git merge

O trabalho na tela 1 ficou pronto. Pra mandar o seu trabalho para o master use o comando `git merge`. `Merge` pode ser traduzido livremente como `misturar`. Na prática, o que o merge faz é juntar os commits de um branch com os commits de outro.

```
$ git checkout master
Switched to branch 'master'
$ git merge tela-1
Updating c094039..ab8ffbe
Fast-forward
 a | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 a
```

Às vezes o `git merge` cria um novo commit quando temos muitas alterações.

Se você quiser entender melhor como branches e merges funcionam, com gráficos e detalhes sobre cenários onde acontecem conflitos de merge (alterações incompatíveis entre os dois branches), consulte a [seção 3.2 do livro Pro Git](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging).

## Ao infinito e além

Tem muito mais que se pode fazer com `git`. Corrigir erros em um commit, transformar vários commits em um só, manipular o histórico, reverter uma alteração, criar atalhos pras funções mais usadas, integrar múltiplos repositórios, usar git dentro de outras ferramentas e muito mais.

Não tente aprender tudo que dá pra fazer com `git` de uma única vez. Colabore com outras pessoas usando os comandos básicos, navegue no seu histórico, pegue prática em usar o github e volte às referências para aprender mais com o tempo.

## Referências e como se aprofundar

- [LMS](https://lms.laboratoria.la/cohorts/spl-2020-03-bc-core-sap004/courses/scm-pt)
- [Livro Pro Git](https://git-scm.com/book/en/v2)
- [Learn Git in 30 minutes](https://tutorialzine.com/2016/06/learn-git-in-30-minutes)
- [Git Best Practices](https://sethrobertson.github.io/GitBestPractices)
# Git基礎

## 目次
1. Gitとは
2. リポジトリとは 
3. Gitに重要な3つの概念
4. Gitハンズオン

### 1. Gitとは 
バージョン管理ツール。  
ソースコードの変更履歴をもち、過去の状態に戻すことが可能。  
複数人で開発する際に効果的な管理ツールになる。  

#### GitHub、GitLabについて
Gitを利用したWebサービス。  インターネット上にソースコードを公開もしくは非公開で管理することができる。  
(APIキーや業務コードは、)

世界中のプログラマやエンジニアが公開しているソースコードをライセンスに従って利用したり、  
すでにあるOSSに参加することができる。

### 2. リポジトリとは  
リポジトリはGitであつかう変更履歴が記録された作業ディレクトリ。  
リポジトリは、「ローカルリポジトリ」と「リモートリポジトリ」にわかれる。  

ローカルリポジトリ上に保存されているのが「ローカルリポジトリ」。  
Gitサーバ上にあるものが「リモートリポジトリ」。  

#### Gitの始め方
1. リモートリポジトリ -> clone -> ローカルリポジトリ  
2. リモートリポジトリ <- push <- ローカルリポジトリ  

### 3. Gitに重要な3つの概念
1. branch (ブランチ)  
2. commit (コミット)  
3. add (アド)  

Gitはコミットを最小単位として履歴を残している。  
そして、ブランチはコミットを保持している。  
すなわち、ブランチはコミットを記録するワークツリーの分岐のこと。  

addはインデックスにステージングする。  
インデックスとは、ローカルリポジトリにコミットする前のところ。  

``` git commit -m 'コメント' ``` としてコミットするとき、  
インデックスにステージングされたものがローカルリポジトリに反映される。  

コミットは一意でなければならず、commit idに記載されているハッシュ値は重複してはならない。  

#### HEADとは
HEADは、現在のブランチにおいて、最新のコミットのこと。  

HEAD^、HEAD~は、最新のコミットの1つ前のコミットのこと。  
HEAD^^、HEAD~~は最新のコミットの2つ前のコミットのこと。  

ちなみに、エイリアスとして「@」としてあらわすことができるので、  
@^、@^^、@~、@~~、@~~~などとあらわすことができる。  


### 4. Gitハンズオン
```
1. ディレクトリを作成して移動
~$ mkdir gitest
~$ cd gitest/


2. リポジトリを作成して確認
~/gitest$ git init 
Initialized empty Git repository in /home/done/gitest/.git/
~/gitest$ ls -la
total 12
drwxrwxr-x  3 user user 4096 Apr 26 23:20 .
drwxr-xr-x 11 user user 4096 Apr 26 23:18 ..
drwxrwxr-x  7 user user 4096 Apr 26 23:20 .git


3. 新規でファイルを作成する
~/gitest$ echo "test" >> test.txt
~/gitest$ cat test.txt
test


4. 新規作成したファイルをaddする
~/gitest$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt

nothing added to commit but untracked files present (use "git add" to track)
~/gitest$ git add test.txt
~/gitest$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test.txt


5. E-MailとNameを登録してcommitする
~/gitest$ git config --global user.email "you@example.com"
~/gitest$ git config --global user.name "Your Name"
~/gitest$ git commit -m "create new file"
[master (root-commit) 1b17c87] create new file
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
 ~/gitest$ git status
On branch master
nothing to commit, working tree clean


6. ファイルに変更を加えて、addしてcommitする
~/gitest$ echo "test" >> test.txt
~/gitest$ cat test.txt
test
test
~/gitest$ git add test.txt
~/gitest$ git commit -m "add to test.txt"
[master 4d080e4] add to test.txt
 1 file changed, 1 insertion(+)


7. 変更履歴を確認して、一つ前の変更履歴に戻す
~/gitest$ git log --graph
* commit 4d080e487a3fe53fc4699b31b248ebbedee7ff75 (HEAD -> master)
| Author: Your Name <you@example.com>
| Date:   Tue Apr 26 23:30:03 2022 +0900
|
|     add to test.txt
|
* commit 1b17c87b79e1a18625b802efb9da053a8b891599
  Author: Your Name <you@example.com>
  Date:   Tue Apr 26 23:27:20 2022 +0900

      create new file
~/gitest$ git checkout 1b17c87b79e1a18625b802efb9da053a8b891599
~/gitest$ cat test.txt
test
~/gitest$ git log --graph
* commit 1b17c87b79e1a18625b802efb9da053a8b891599 (HEAD)
  Author: Your Name <you@example.com>
  Date:   Tue Apr 26 23:27:20 2022 +0900

      create new file


8. 現在の最新のコミットに戻す
~/gitest$ git checkout master
~/gitest$ cat test.txt
test
test
~/gitest$ git log --graph
* commit 4d080e487a3fe53fc4699b31b248ebbedee7ff75 (HEAD -> master)
| Author: Your Name <you@example.com>
| Date:   Tue Apr 26 23:30:03 2022 +0900
|
|     add to test.txt
|
* commit 1b17c87b79e1a18625b802efb9da053a8b891599
  Author: Your Name <you@example.com>
  Date:   Tue Apr 26 23:27:20 2022 +0900

      create new file

9. ローカルリポジトリをGitHub上のリモートリポジトリに反映する
リモートリポジトリ: https://github.com/done-san/gitest
GitHubへのSSH接続はすでにできるものとする。
*注:念のため一部加工しています

~/gitest$ git remote add origin https://github.com:done-san/gitest.git
~/gitest$ git remote set-url origin git@github.com:done-san/gitest.git
~/gitest$ git remote -v
origin  git@github.com:done-san/gitest.git (fetch)
origin  git@github.com:done-san/gitest.git (push)
~/gitest$ git push origin master
The authenticity of host 'github.com (0.0.0.0)' can't be established.
ECDSA key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,0.0.0.0' (ECDSA) to the list of known hosts.
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (6/6), 434 bytes | 217.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:done-san/gitest.git
 * [new branch]      master -> master
```  

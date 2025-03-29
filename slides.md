---
title: "Git Tutorial"
titleTemplate: "%s"
theme: default
background: /images/background.jpg
highlighter: shiki
lineNumbers: true
colorSchema: "dark"
fonts:
  sans: "Noto Sans Japanese"
  serif: "Noto Sans Japanese"
  mono: "Fira Code"
class: text-left
favicon: "/images/favicon.png"
transition: slide-left
---

# Git Tutorial

初心者に向けた Git ハンズオン（GitHub もちょっと触れるよ！）

<div @click="$slidev.nav.next" class="mt-12 py-2 px-4 w-fit rounded-lg" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---

# 目次

<Toc text-sm minDepth="1" maxDepth="2" />

---

# 本講義で習得してほしいこと

- `Git` の基本的な操作、流れの理解
- `GitHub` の基本的な操作、流れの理解
- 最低限覚えてほしいコマンド
  - `git add`, `git commit` `git branch` `git merge` `git clone` `git push` `git fetch` `git pull`

---
title: はじめに①
---

# はじめに①

今回はコマンドベースで講義を進めますが、なにかとGUIツールが便利なので先に入れておきましょう！（大野が普段使用しているツールを入れてもらいますが、他にもいろんなツールがあるので興味があれば各自で調べてみてください！）

<img src="/images/git-graph.png" class="h-80 mt-4" />
<div class="absolute h-14 w-78 border-3 border-red-500 top-54 left-20 rounded-lg" />

---
title: はじめに②
---

# はじめに②

Gitコマンドの基本

基本的には下記の構成で成り立っている🙆‍♂️

`git` `[操作]` `[操作に対するオプション]` `[操作対象など]`

つまりこんな感じでコマンド入力する（パターンは無限大、、、）

```bash
# コミットする
git commit -m 'first commit'

# ブランチの確認
git branch

# マージする
git merge develop

# オプションを複数使うことも可能
git commit --amend --no-edit
```

---
title: Gitでバージョン管理する準備をしよう
layout: center
class: text-center
---

# 🧑‍💻Gitでバージョン管理する準備をしよう🧑‍💻

<div />

`git init` `git config`

---
hideInToc: true
---

# リポジトリの作成

- `git init` を使用することでGitシステムの管理を開始することができます

<div class="mt-8" />

1. `git-tutorial` というディレクトリを作成し、`VSCode` で開く
2. ターミナルからコマンド（`git init`）実行！（`ctrl` + `J`でターミナルを開けます）
3. `.git` ディレクトリが作成される

```bash {1|3-4}
git init

# こんなのが出ればOK！
Initialized empty Git repository in ...git-tutorial/.git/
```

<img src="/images/git-directory.png" class="w-100 h-32 mt-4 object-cover object-left-top" />

<Arrow v-click x1="210" y1="450" x2="110" y2="400" class="text-green-500" />

---
hideInToc: true
---

# Gitにユーザ情報を設定する

- `git config` を使用することでGitシステムにユーザー情報を登録することができます

<div class="mt-8" />

ここで設定したユーザ情報は変更履歴を記録する際に一緒に記録され、誰がその変更履歴を記録したのかを確認する場合などに使用します

<p class="text-red-400 font-bold">※改行が実行の合図なので、1行ずつ実行しましょう！</p>

```bash
git config --global user.name OhnoKeita
git config --global user.email mail@example.com
```

---
title: コミットを記録してみよう
layout: center
class: text-center
---

# 🖊️コミットを記録してみよう🖊️

<div />

`git status` `git add` `git commit`

---
hideInToc: true
---

# 作成したリポジトリにファイルを追加する

<div />

`test.txt` ファイルを新規作成しよう！

<img src="/images/add-file.png" class="h-80 mt-4" />

<Arrow x1="370" y1="330" x2="470" y2="230" class="text-green-500" />

---
hideInToc: true
---

# リポジトリの変更状態を確認する

- `git status` はリポジトリの「変更状態」を確認できるコマンドです

`git status` とターミナルに入力し、実行してみよう！

```bash {1|2-11|7-9}
git status

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt

nothing added to commit but untracked files present (use "git add" to track)
```

<div v-after class="mt-4">
  <code>Untracked files</code> は、まだコミットに含めないファイルだけど、差分があるよ！っていうステータス
</div>
<Arrow v-after x1="400" y1="400" x2="300" y2="340" class="text-green-500" />

---
hideInToc: true
---

# 今の状態はこんな感じ🤔

<div class="grid grid-cols-3 w-full items-center mt-16 gap-8">
  <div class="p-4 border-2 h-60 flex flex-col rounded-lg gap-4">
    ワーキングディレクトリ
    <div class="flex gap-2 items-center text-green-500">
      <mdi-file-document-plus-outline class="size-12" />
      test.txt
    </div>
  </div>
  <div class="p-4 border-2 h-60 flex flex-col rounded-lg gap-4">
    ステージングエリア（インデックス）
  </div>
  <div class="p-4 border-2 h-60 flex flex-col rounded-lg gap-4">
    Gitシステム
  </div>
</div>

<Arrow v-click x1="210" y1="230" x2="400" y2="230" class="text-green-500" />
<div v-after class="text-green-500 absolute top-60 left-95">
  コミット対象にするためには
  <br />
  ステージングエリアに！
</div>

---
hideInToc: true
---

# コミット対象に `test.txt` を含める

- `git add` を使用すると、ステージングエリアへの追加を行える
  - 対象にファイル名やフォルダ名を指定できる → `git add .` とすれば、全ファイルがステージングエリアに移動する

<div class="mt-8" />

1. `git add test.txt` で `test.txt` をステージングエリアに追加する
2. `git status` で現在の状況を確認

```bash {1|3|5-11|9-11}
git add test.txt

git status

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test.txt
```

<div v-after class="mt-4">
  これでステージングエリアに追加完了✨
</div>

---
hideInToc: true
---

# 今の状態はこんな感じ🫡

<div class="grid grid-cols-3 w-full items-center mt-16 gap-8">
  <div class="p-4 border-2 h-60 flex flex-col rounded-lg gap-4">
    ワーキングディレクトリ
  </div>
  <div class="p-4 border-2 h-60 flex flex-col rounded-lg gap-4">
    ステージングエリア（インデックス）
    <div class="flex gap-2 items-center text-green-500">
      <mdi-file-document-plus-outline class="size-12" />
      test.txt
    </div>
  </div>
  <div class="p-4 border-2 h-60 flex flex-col rounded-lg gap-4">
    Gitシステム
  </div>
</div>

<Arrow v-click x1="500" y1="230" x2="700" y2="230" class="text-green-500" />
<div v-after class="text-green-500 absolute top-60 left-170">
  この状態でコミットして
  <br />
  初めて記録が残る
</div>

---
hideInToc: true
---

# リポジトリにコミットを記録しよう！

<div />

- `git commit` を使用すると、コミット履歴を記録することができます
- `-m` オプションを使用することでコミットメッセージを付与することができます

```bash {1|3-}
git commit -m "test.txtの作成"

[master (root-commit) c16a597] test.txtの作成
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test.txt
```

<div v-after class="mt-4">
  こんな感じで出力されたら、コミット完了📚
</div>

---
hideInToc: true
---

# コミットを確認する

<div class="absolute h-10 w-21 border-3 border-red-500 top-37 left-78 rounded-lg" />

<div class="mt-4">
  VSCode下部の <code>Git Graph</code> をクリック
</div>

<img src="/images/git-graph-button.png" class="h-12 mt-4" />

<div class="mt-4">
  さっきのコミット履歴を確認できる！
</div>

<img src="/images/commit-confirm1.png" class="h-60 mt-4" />

<p v-click class="absolute top-80 left-140 text-green-500">コミットID（コミットハッシュ）</p>
<Arrow v-after x1="550" y1="348" x2="370" y2="362" class="text-green-500" />
<p v-click class="absolute top-90 left-140 text-green-500">コミットした人のユーザ名とメールアドレス</p>
<Arrow v-after x1="550" y1="388" x2="310" y2="390" class="text-green-500" />
<p v-click class="absolute top-100 left-140 text-green-500">コミットした日時</p>
<Arrow v-after x1="550" y1="428" x2="370" y2="415" class="text-green-500" />
<p v-click class="absolute top-110 left-140 text-green-500">コミットメッセージ</p>
<Arrow v-after x1="550" y1="468" x2="188" y2="446" class="text-green-500" />

---
hideInToc: true
layout: center
class: text-center
---

# コミットまでの流れは理解できましたか？🧐

---
hideInToc: true
---

# ファイルを編集してコミットしてみよう

1. `test.txt` に `Hello,World` と追記する

```diff
+ Hello,World
```

2. `1` で行った変更をコミットする（コミットメッセージ：`test.txtへ「Hello,World」を追記`）
3. `Git Graph` で変更を確認する

<img src="/images/commit-confirm2.png" class="h-60 mt-4" />

---
title: 変更履歴を分岐させてみよう
layout: center
class: text-center
---

# 🪵変更履歴を分岐させてみよう🪵

<div />

`git branch` `git switch`

---
hideInToc: true
---

# ブランチの状況を確認、作成する

<div />

- `git branch` で現在のブランチの一覧と参照しているブランチを確認できる（`*` が参照しているブランチ）
- `git branch {ブランチ名}` でブランチの作成ができる

`subブランチ` の作成と、ブランチの確認を行います！

```bash
# ブランチの確認
git branch
* master

# ブランチを作成
git branch sub

# ブランチの確認（subブランチが作成された！）
git branch
* master
  sub
```

---
hideInToc: true
---

# ブランチを切り替える

<div />

- `git switch {ブランチ名}` でブランチの切り替えができる

`subブランチ` へブランチを切り替える。（チェックアウトする）

```bash
# ブランチの切り替え
git switch sub

# ブランチの確認（subブランチに移動している！）
git branch
  master
* sub
```

---
hideInToc: true
---

# `subブランチ` でコミットを記録する

1. `test.txt` に `subブランチの変更` と追記する

```diff
Hello,World
+ subブランチの変更
```

2. `1` で行った変更をコミットする（コミットメッセージ：`test.txtへ「subブランチの変更」を追記`）
3. `Git Graph` で変更を確認する

<img src="/images/commit-confirm3.png" class="h-60 mt-4" />

<p v-click class="absolute top-100 left-120 text-green-500">masterブランチから派生して、変更履歴が更新されている</p>
<Arrow v-after x1="465" x2="320" y1="430" y2="360" class="text-green-500" />
<Arrow v-after x1="465" x2="290" y1="430" y2="485" class="text-green-500" />

---
hideInToc: true
layout: center
class: text-center
---

# つまり、`masterブランチ` に影響を与えずに、 `subブランチ` のみを更新できた！

<div class="mt-12" />

## 確認してみよう！🔎

---
hideInToc: true
---

# `masterブランチ` と `subブランチ` は今どんな状態なのか？

- `masterブランチ` に切り替えて、 `test.txt` を確認する

<img src="/images/test-text-file1.png" class="h-60 mt-4" />

`subブランチの変更` という文字が消えている！

つまり、`subブランチ` の変更の影響を受けていない！

---
hideInToc: true
---

# `masterブランチ` でコミットを記録する

1. `test.txt` に `masterブランチの変更` と追記する

```diff
Hello,World
+ masterブランチの変更
```

2. `1` で行った変更をコミットする（コミットメッセージ：`test.txtへ「masterブランチの変更」を追記`）
3. `Git Graph` で変更を確認する

<img src="/images/commit-confirm4.png" class="h-60 mt-4" />

<p v-click class="absolute top-81 left-140 text-green-500">masterブランチのみの変更</p>
<Arrow v-after x1="550" x2="330" y1="355" y2="355" class="text-green-500" />
<p v-after class="absolute top-112 left-140 text-green-500">subブランチのみの変更</p>
<Arrow v-after x1="550" x2="290" y1="478" y2="478" class="text-green-500" />

---
title: ブランチの変更を統合しよう
layout: center
class: text-center
---

# 🐎ブランチの変更を統合しよう🐎

<div />

`git merge`

---
hideInToc: true
---

# マージの種類は2パターンある

1. 取り込む側のブランチに新しいコミットが記録されていないパターン

   - マージコミットが作成されない（ファストフォワード）

2. 取り込む側のブランチに新しいコミットが記録されているパターン

   - マージコミットが作成される

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されていないパターンのマージをやってみよう（パターン1）

- やること：`masterブランチ` に `sub2ブランチ` の変更を統合（マージ）する

<div class="mt-8" />

1. `masterブランチ` に移動する
2. `sub2ブランチ` を作成する
3. `sub2ブランチ` に移動する
4. `test.txt` を下記のように変更し、コミットする（コミットメッセージ：`test.txtへ「sub2ブランチの変更」を追記`）

```diff
Hello,World
masterブランチの変更
+ sub2ブランチの変更
```

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されていないパターンのマージをやってみよう（パターン1）

5. `masterブランチ` 移動する
6. マージする

- `git merge {ブランチ名}` でマージを実行できます
  - 実行するブランチは取り込まれるブランチ
  - ブランチ名には取り込むブランチを記載

```bash {1|1-}
git merge sub2

Updating bbf4361..c92ad7d
Fast-forward
 test.txt | 1 +
 1 file changed, 1 insertion(+)
```

<div v-after class="absolute h-8 w-26 border-3 border-red-500 top-89 left-24 rounded-lg" />
<p v-after><code>Fast-forward</code> と表示される！</p>

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されていないパターンのマージをやってみよう（パターン1）

7. `Git Graph` で変更を確認する

<img src="/images/commit-confirm5.png" class="h-80 mt-4" />

<p class="absolute top-90 left-134 text-green-500">masterブランチとsub2ブランチが同じ位置に！</p>
<p class="absolute top-98 left-134 text-green-500">※ファストフォワードとは取り込み先のブランチに移動させる処理のことで、マージしても枝分かれの履歴が残らない</p>
<Arrow x1="520" x2="220" y1="380" y2="280" class="text-green-500" />

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されていないパターンのマージをやってみよう（パターン1）

8. `masterブランチ` の `test.txt` を確認する

<img src="/images/test-text-file2.png" class="h-60 mt-4" />

`sub2ブランチ` で加えた更新が反映されている！（マージ完了✨）

<div class="absolute h-10 w-52 border-3 border-red-500 top-81 left-37 rounded-lg" />

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されているパターンのマージをやってみよう（パターン2）

- やること：`masterブランチ` に `sub2ブランチ` の変更を統合（マージ）する

<div class="mt-8" />

1. `masterブランチ` に移動する
2. `test2.txt` を作成する
3. `2` の変更をコミットする（コミットメッセージ：`test2.txtの追加`）
4. `sub2ブランチ` に移動する
5. `test3.txt` を作成する
6. `5` の変更をコミットする（コミットメッセージ：`test3.txtの追加`）
7. `masterブランチ` 移動する

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されているパターンのマージをやってみよう（パターン2）

<div />

この時点でこんな感じ！

<img src="/images/commit-confirm6.png" class="h-80 mt-4" />

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されているパターンのマージをやってみよう（パターン2）

8. マージする

```bash {1|1-}
git merge sub2

Merge made by the 'ort' strategy.
 test3.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test3.txt
```

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されているパターンのマージをやってみよう（パターン2）

9. `Git Graph` で変更を確認する

<img src="/images/commit-confirm7.png" class="h-80 mt-4" />

<div v-click class="absolute h-25 w-13 border-3 border-red-500 top-74 left-14 rounded-lg" />

<p v-after class="absolute top-98 left-134 text-green-500">※ファストフォワードとは異なり、 <code>Merge branch sub2</code> というコミットを作成してマージを行っている（マージコミット）</p>
<Arrow v-after x1="520" x2="120" y1="420" y2="380" class="text-green-500" />

---
hideInToc: true
---

# 取り込む側のブランチに新しいコミットが記録されているパターンのマージをやってみよう（パターン2）

8. `masterブランチ` の `エクスプローラー` を確認する

<img src="/images/explorer-confirm1.png" class="h-72 mt-4" />

`masterブランチ` と `sub2ブランチ` で加えた更新が両方反映されている！（マージ完了✨）

<div class="absolute h-18 w-24 border-3 border-red-500 top-50 left-12 rounded-lg" />

---
hideInToc: true
layout: center
class: text-center
---

# もし、同じファイル、同じ行を別ブランチで編集したのち、

# マージしたらどうなる🤔

---
hideInToc: true
---

# ちょっと再現してみる

```bash
git switch master
git merge sub
```

なんか出た！👀

<img src="/images/test-text-file3.png" class="h-72 mt-4" />

---
hideInToc: true
---

# 競合（コンフリクト）

<div />

マージ実行時に同じファイルで異なる変更があった場合、うまく差分を統合できない現象のことを `競合（コンフリクト）` と言います。

<img src="/images/test-text-file3.png" class="h-72 mt-4" />

<p v-click class="absolute top-72.5 left-140 text-green-500">masterブランチの変更</p>
<Arrow v-after x1="550" x2="330" y1="320" y2="320" class="text-green-500" />
<p v-after class="absolute top-85.5 left-140 text-green-500">subブランチの変更</p>
<Arrow v-after x1="550" x2="330" y1="372" y2="372" class="text-green-500" />

---
hideInToc: true
---

# 競合（コンフリクト）の解消方法

<div />

競合は手動で直す必要がある。`<<<<<<< HEAD` `>>>>>>> sub` といった行を削除し、正しい状態に修正した後に再度コミットする必要があります。

<img src="/images/test-text-file3.png" class="h-72 mt-4" />

<div  class="absolute h-8 w-114 border-3 border-red-500 top-62 left-32 rounded-lg" />

<p class="absolute top-112 left-80 text-green-500"><code>VSCode</code> の場合、ここのボタンをクリックしたら自動的に修正してくれる</p>
<Arrow x1="520" x2="420" y1="456" y2="290" class="text-green-500" />

---
hideInToc: true
---

# 競合（コンフリクト）の解消方法

<div />

今回は下記のように修正しコミットしましょう！

<img src="/images/test-text-file4.png" class="h-60 my-4" />

```bash {1-3}
# ステージングに追加してから、コミットすること！
git add .
git commit -m "Merge branch 'sub'"

[master 9a6778c] Merge branch 'sub'
```

---
hideInToc: true
---

# 競合（コンフリクト）の解消方法

<div />

`Git Graph` で確認しよう！

<img src="/images/commit-confirm8.png" class="h-80 mt-4" />

<div v-click class="absolute h-46 w-16 border-3 border-red-500 top-60 left-14 rounded-lg" />

<p v-after class="absolute top-98 left-134 text-green-500"><code>subブランチ</code> のマージも完了✨</p>
<Arrow v-after x1="520" x2="130" y1="420" y2="260" class="text-green-500" />

---
title: Gitの便利コマンド等
layout: center
class: text-center
---

# 🚀Gitの便利コマンド等🚀

<div />

`git commit--amend` `git stash` `git -h` `.gitignore` `GUIツール`

---
hideInToc: true
---

# Gitの便利コマンド等

<div />

`Git` 自体はこれさえできれば十分に扱えますが、僕が仕事でも実際に使用するコマンド等を紹介します（全部じゃないし、これら以外にも便利なコマンドはいっぱいあります！）

ここで紹介しきれないものは、聞いたり、調べたりしてください🙆‍♂️

- `git commit--amend`
- `git stash`
- `git -h`
- `.gitignore`
- `GUIツール`

---
hideInToc: true
---

# git commit--amend

直前のコミットを修正（上書き）するためのコマンド

あ、間違えた内容でコミットしちゃった、、みたいなときに便利！

例）更新内容もコミットメッセージも間違えたとき

<img src="/images/test-text-file5.png" class="h-36 mt-4" />

<img src="/images/commit-confirm9.png" class="h-36 mt-4" />

---
hideInToc: true
---

# git commit--amend

直前のコミットを修正（上書き）するためのコマンド

<img src="/images/test-text-file6.png" class="h-32 mt-4" />

ファイルを正しく修正したのち下記コマンドを実行

```bash {2}
git add .
git commit --amend -m "test.txtに自己紹介を追加"
```

<img src="/images/commit-confirm10.png" class="h-32 mt-4" />

<p class="absolute top-91 left-148 text-green-500">前回の間違ったコミット内容を新しく書き換えた！</p>
<Arrow x1="580" x2="330" y1="392" y2="392" class="text-green-500" />

---
hideInToc: true
---

# git stash

変更を一時退避するためのコマンド

あるブランチで作業中だけど、いますぐやりたいことができたなー、作業が中途半端だからコミットはしたくないみたいなときに使える

コミットせずとも修正内容を保持しておくことができる

もちろん一時退避した内容は、好きなタイミングで元に戻すこともできます

```bash
# 今の変更内容から一時退避を作成
git stash

# 一時退避のリストを確認する
git stash list

# 一時退避を元に戻しつつ、一時退避を削除
git stash pop
```

---
hideInToc: true
---

# git -h

`Git` で使用できるコマンドをの一覧を確認できる

全部英語ですが、このコマンド何できるっけ？どんなオプションあったけ？みたいなのをコマンド上で確認できる！

```bash {1}
git -h

usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone     Clone a repository into a new directory
   init      Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add       Add file contents to the index
...
```

---
hideInToc: true
---

# .gitignore

`Git` の管理に入れたくないファイルを定義できる

基本的にリポジトリに追加されるファイルは管理対象になるが、 `.gitignore` ファイルを使用することで、特定のファイル・ディレクトリを除外することができる

いつ使うのか？

- パスワードが記載されているファイル
- Logファイル など

---
hideInToc: true
---

# .gitignore

`Git` の管理に入れたくないファイルを定義できる

1. `.gitignore` を作成・コミット（コミットメッセージ：`.gitignoreの追加`）

```diff
+ password.txt
```

2. `password.txt` を作成
3. 差分を確認する

```bash {1|1-}
git status

On branch master
nothing to commit, working tree clean
```

<p v-after>password.txtが追跡されていない！</p>

---
hideInToc: true
---

# GUIツール

Gitの履歴や操作を視覚的に確認できるツール

- [Fork](https://git-fork.com/)
- [Sourcetree](https://www.sourcetreeapp.com/)
- [VSCode](https://code.visualstudio.com/docs/sourcecontrol/overview)

実は `VSCode` でも、ボタンをポチポチするだけでGit操作ができます！

ここからはコマンドでもGUIでも、どちらを使っても大丈夫です！

<img src="/images/vscode-git.png" class="h-50 mt-4" />

---
title: GitHubを利用しよう
layout: center
class: text-center
---

# 🐙GitHubを利用しよう🐙

<div />

`git clone` `git push` `git fetch` `git pull`

---
hideInToc: true
---

# GitHubでリモートリポジトリを作成しよう

<div />

GitHubアカウントは作成している前提で進めます。（[ここからアカウントを作成する](https://github.com/)）

1. リポジトリの作成を開始する

<img src="/images/github1.png" class="h-50 mt-4" />

<div class="absolute h-11 w-21 border-3 border-red-500 top-83 left-76 rounded-lg" />

---
hideInToc: true
---

# GitHubでリモートリポジトリを作成しよう

2. リポジトリの設定を入力し、リポジトリを作成する

<img src="/images/github2.png" class="h-90 mt-4" />

<p class="absolute top-60.5 left-98 text-green-500">リポジトリ名：<code>sample-repository</code></p>
<Arrow x1="380" x2="210" y1="270" y2="270" class="text-green-500" />

<p class="absolute top-71 left-98 text-green-500">リポジトリの説明（任意項目）：空白</p>
<Arrow x1="380" x2="316" y1="312" y2="312" class="text-green-500" />

<p class="absolute top-80.5 left-98 text-green-500">公開設定（誰でも見れるようにするかの設定）：<code>Private</code></p>
<Arrow x1="380" x2="210" y1="350" y2="350" class="text-green-500" />

<p class="absolute top-93 left-98 text-green-500">その他（<code>.gitignore</code> 等の設定を入れるかどうか）：デフォルトのままでOK</p>
<Arrow x1="380" x2="210" y1="400" y2="400" class="text-green-500" />

<div class="absolute h-6 w-16 border-3 border-red-500 top-120 left-63 rounded-lg" />

---
hideInToc: true
---

# GitHubでリモートリポジトリを作成しよう

3. リモートリポジトリの作成が完了✨

<img src="/images/github3.png" class="h-90 mt-4" />

---
hideInToc: true
---

# PC上にリモートリポジトリのコピーを作成する（クローン）

<div />

1. 任意のフォルダで `VSCode` を開く
2. `git clone` コマンドを使用して、リモートリポジトリをローカル環境に複製する

```bash {1,2,7,8}
# クローン
git clone {リモートリポジトリのURL}

Cloning into 'sample-repository'...
warning: You appear to have cloned an empty repository.

# 新しくVSCodeを立ち上げる（codeコマンドはとりあえず気にしなくてOKです）
code .\sample-repository\
```

---
hideInToc: true
---

# リモートリポジトリにPC上の変更を反映させる（プッシュ）

<div />

1. `example.txt` を作成し、下記のように編集する。

```txt
Hello, World!!!
```

2. `1` の内容でコミットする（コミットメッセージ：`example.txtへ「Hello, World!!!」を追記`）
3. `git push` コマンドを実行する！

```bash {1,2|1-}
# リモートリポジトリにPC上の変更を反映させるコマンド
git push

Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 280 bytes | 280.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/.../sample-repository
 * [new branch]      main -> main
```

---
hideInToc: true
---

# リモートリポジトリにPC上の変更を反映させる（プッシュ）

<div />

4. `GitHub` を確認する

<img src="/images/github4.png" class="h-80 mt-4" />

<p class="absolute top-120 left-98 text-green-500">PCで行った変更が反映されている！</p>
<Arrow x1="500" x2="400" y1="490" y2="280" class="text-green-500" />

---
hideInToc: true
---

# リモートリポジトリにPC上の変更を反映させる（プッシュ）

<div />

ちなみにブランチのプッシュもできます！

1. `subブランチ` を作成する
2. `git push` コマンドを実行し、ブランチの作成をリモートリポジトリに反映させる

```bash {1,2|1-}
# git push {リモートリポジトリ名} {ブランチ名} → リモートに存在しないブランチをpushする際はこう記載する！
git push origin sub

Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'sub' on GitHub by visiting:
remote:      https://github.com/.../sample-repository/pull/new/sub
remote:
To https://github.com/.../sample-repository
 * [new branch]      sub -> sub
```

- `リモートリポジトリ名` とは？ → `origin` を指定すればよい！（何か特殊なことをしてない限りは大体`origin`）

```bash
git remote -v
origin  https://github.com/.../sample-repository (fetch)
origin  https://github.com/.../sample-repository (push)
```

<div class="absolute h-9.5 w-17 border-3 border-red-500 top-117 left-23 rounded-lg" />

---
hideInToc: true
---

# リモートリポジトリにPC上の変更を反映させる（プッシュ）

<div />

3. `GitHub` を確認する

<img src="/images/github5.png" class="h-80 mt-4" />

<p class="absolute top-120 left-98 text-green-500">PCで行った変更が反映されている！</p>
<Arrow x1="500" x2="106" y1="490" y2="328" class="text-green-500" />

---
hideInToc: true
---

# PC上にリモートリポジトリの変更を取得する（フェッチ）

<div />

フェッチするためににリモートリポジトリで更新を行ってから、フェッチの操作を行います。

1. `GitHub` で `sample.txt` の内容を修正する

```diff
Hello, World!!!

+ こんにちは、世界
```

<img src="/images/github6.png" class="h-40 mt-4" />

<div class="absolute h-8 w-25 border-3 border-red-500 top-78 left-192 rounded-lg" />

---
hideInToc: true
---

# PC上にリモートリポジトリの変更を取得する（フェッチ）

<div />

2. `GitHub` で `sample.txt` の内容を更新する

<img src="/images/github7.png" class="h-80 mt-4" />

<div class="absolute h-7.5 w-25 border-3 border-red-500 top-106 left-64 rounded-lg" />

---
hideInToc: true
---

# PC上にリモートリポジトリの変更を取得する（フェッチ）

<div />

3. `git fetch` コマンドを実行する

```bash
git fetch

remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 951 bytes | 237.00 KiB/s, done.
From https://github.com/.../sample-repository
   1172e97..bf3bc46  main       -> origin/main
```

4. `sample.txt` を確認する

<img src="/images/test-text-file7.png" class="h-30 mt-4" />

`GitHub` で更新した内容は反映されていない🙅‍♂️（`origin/mainブランチ` のみ反映されているから）

---
hideInToc: true
---

# PC上にリモートリポジトリの変更を取得する（フェッチ）

<div />

5. `Git Graph` で変更を確認する

<img src="/images/commit-confirm11.png" class="h-60 mt-4" />

<p class="absolute top-100 left-100 text-green-500">リモートの変更内容が <code>origin/mainブランチ</code> に反映されている！</p>
<Arrow x1="640" x2="400" y1="408" y2="332" class="text-green-500" />

---
hideInToc: true
---

# PC上にリモートリポジトリの変更を反映させる（プル）

<div />

1. `git pull` コマンドを実行する

```bash
git pull

Updating 1172e97..bf3bc46
Fast-forward
 example.txt | 2 ++
 1 file changed, 2 insertions(+)
```

2. `sample.txt` を確認する

<img src="/images/test-text-file8.png" class="h-30 mt-4" />

反映された💡

※ `git pull` は `git fetch` + `git merge` をまとめてやってくれるので、基本的にはリモートの反映を取得する際は `git pull` だけを使用するケースが多い（`git fetch` はあまり使わないイメージ）

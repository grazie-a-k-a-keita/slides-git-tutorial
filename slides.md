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
- 覚えてほしいコマンド
  - `git status`, `git add`, `git commit`

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

```txt
Hello,World
```

2. `1` で行った変更をコミットする → コミットメッセージは `text.txtへ「Hello,World」を追記` としてください
3. `Git Graph` で変更を確認する

<img src="/images/commit-confirm2.png" class="h-60 mt-4" />

---
title: 変更履歴を分岐させてみよう
layout: center
class: text-center
---

# 🪵変更履歴を分岐させてみよう🪵

<div />

`git branch`

---
hideInToc: true
---

# ブランチの状況を確認、作成する

<div />

- `git branch` で現在のブランチの一覧と参照しているブランチを確認できる（`*` が参照しているブランチ）
- `git branch {ブランチ名}` でブランチの作成ができる

`subブランチ` の作成と、ブランチの確認を行います！

```bash
git branch
* master

git branch sub

git branch
* master
  sub
```

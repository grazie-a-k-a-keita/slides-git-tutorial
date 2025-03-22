---
title: 'Git Tutorial'
titleTemplate: '%s'
theme: default
background: /images/background.jpg
highlighter: shiki
lineNumbers: true
colorSchema: 'dark'
fonts:
  sans: 'Noto Sans Japanese'
  serif: 'Noto Sans Japanese'
  mono: 'Fira Code'
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

<div />

1. `git-tutorial` というディレクトリを作成し、`VSCode` で開く
2. ターミナルからコマンド実行！（`ctrl` + `J`でターミナルを開けます）
3. `.git` ディレクトリが作成される

```bash {1|3-4}
git init

# こんなのが出ればOK！
Initialized empty Git repository in ...git-tutorial/.git/
```

<img src="/images/git-directory.png" class="h-48 mt-4" />

<Arrow v-click x1="210" y1="390" x2="110" y2="340" class="text-green-500" />

---
hideInToc: true
---

# Gitにユーザー情報を設定する

<div />

ここで設定したユーザー情報は変更履歴を記録する際に一緒に記録され、誰がその変更履歴を記録したのかを確認する場合などに使用します

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

<div />

`git status` とターミナルに入力し、実行してみよう！

リポジトリの「変更状態」を確認できるコマンドです！

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

<div />

1. `git add` を使用すると、ステージングエリアへの追加を行える

  ※対象にファイル名やフォルダ名を指定できる → `git add .` とすれば、全ファイルがステージングエリアに移動する

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

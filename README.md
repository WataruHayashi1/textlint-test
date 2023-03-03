# textlintのテスト

[textlint](https://github.com/textlint/textlint)とは、Markdownなどのテキストファイル向けのLintツールである。

## インストール

textlintはNode.js環境で動作するため、以下の方法でインストールできる。

```
$ npm install textlint
```

すでに`package.json`があるプロジェクトならば、`--save-dev`オプションをつけてのインストールが推奨される。

また、textlintはデフォルトで搭載されているlintルールは1つもない。そのため、すでに公開されているルールを別途インストールするか、自分でルールを作成する必要がある。

ここでは例として、公開されているルールの1つである、日本語の常体(である調)と敬体(ですます調)をチェックするルールをインストールする。

```
$ npm install textlint-rule-no-mix-dearu-desumasu
```

## ルールを使ってLintする

`--rule <ルール名>`オプションでルールを指定してLintできる。

具体例として、`README.md`というファイルに対して、上でインストールした常体・敬体ルールでLintしたい場合は、以下のように書ける。

```
$ npx --rule no-mix-dearu-desumasu README.md
```

## オプションを省略する

適用するルールが増えると、Lint実行の際の引数が多くなってしまう。

これを防ぐために、`.textlintrc`という設定ファイルに適用するルールについて記載する。

`.textlintrc`はJSON、YAML、JSモジュールで書くことができる。

1から作ることもできるが、`npx textlint --init`コマンドで、JSON形式のものが自動で生成される。

`.textlintrc`の内容は、以下のようになっている。

```json
{
  "plugins": {},
  "filters": {},
  "rules": {
    "no-mix-dearu-desumasu": true
  }
}
```

各種ルールについてboolean値で有効・無効の設定ができる。

また、ルールによっては、さらに細かい設定を行える。

下では、`no-mix-dearu-desumasu`の中で、見出し・本文・箇条書きをである調とし、
厳密なチェックを有効にしている。

```json
{
  "plugins": {},
  "filters": {},
  "rules": {
    "no-mix-dearu-desumasu": {
      "preferInHeader": "である",
      "preferInBody": "である",
      "preferInList": "である",
      "strict": true
    }
  }
}
```
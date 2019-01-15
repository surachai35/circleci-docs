---
layout: classic-docs
title: "Testing Config Files Locally"
description: "Testing Config Files Locally"
---
<div class="alert alert-info" role="alert">
  
<b>Note:</b> This document describes how to test and validate your config through the CircleCI API. It is also possible to install the <a href="{{ site.baseurl }}/2.0/local-cli/#overview">CircleCI CLI</a>, which allows you to <a href="{{ site.baseurl }}/2.0/local-cli/#validate-a-circleci-config">validate</a> your CircleCI config locally.
</div>

To add a script that tests your config file locally, complete the following steps:

1. シェルスクリプトを `run-build-locally.sh` などのファイル名で `.circleci` ディレクトリに作成します。
2. [こちらの手順]({{ site.baseurl }}/2.0/managing-api-tokens/#creating-a-personal-api-token)通りに API トークンを作成します。
3. コマンドラインで以下のように入力し、実行します。  
    `export CIRCLE_TOKEN=<前の手順で生成したトークン文字列>`  
    ※ < > は不要です。
4. 下記の情報を準備します。 
    - ビルド対象のコミットハッシュ
    - ユーザー名
    - プロジェクトソース
    - プロジェクト名
    - ビルド対象のブランチ
5. 用意した情報を下記のシェルスクリプトに当てはめます。

```bash
#!/usr/bin/env bash
curl --user ${CIRCLE_TOKEN}: \
    --request POST \
    --form revision=<コミットハッシュ>\
    --form config=@config.yml \
    --form notify=false \
        https://circleci.com/api/v1.1/project/<プロジェクトソース (例： github) >/<ユーザー名>/<プロジェクト名>/tree/<ブランチ>
```

このシェルスクリプトを実行すると、リポジトリを介してプッシュすることなく `config.yml` ファイルの内容をデバッグできます。

## その他のサンプル

[Using the Local CircleCI CLI]({{ site.baseurl }}/2.0/local-cli/)
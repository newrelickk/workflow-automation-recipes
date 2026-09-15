# workflow-automation-recipes
workflow Automation のレシピ集です。

## レシピ一覧

| レシピ | 概要 |
|--------|------|
| [sre-agent-report-to-slack](recipes/sre-agent-report-to-slack/) | アラート発生時に SRE Agent で原因調査し、レポートを Slack に投稿する |

## ディレクトリ構成

レシピは `recipes/` 配下に 1 レシピ 1 ディレクトリで配置します。各レシピは単体で `terraform init` / `apply` できるように自己完結させます。

```
recipes/
└── <recipe-name>/
    ├── README.md                  # レシピの説明・前提条件・セットアップ手順
    ├── main.tf                    # リソース定義
    ├── variables.tf               # 入力変数
    ├── outputs.tf                 # 出力値
    ├── versions.tf                # Provider バージョン制約
    ├── terraform.tfvars.example   # 変数ファイルサンプル
    ├── .gitignore
    ├── definitions/               # Workflow Automation YAML 定義
    └── scripts/                   # 補助スクリプト（必要な場合のみ）
```

## レシピの追加方法

1. `recipes/<recipe-name>/` を作成する（ディレクトリ名は Workflow Automation の `name` に合わせると分かりやすい）
2. 上記の構成に沿ってファイルを配置し、レシピの `README.md` に概要・前提条件・セットアップ手順を記載する
3. トークンや API Key などのシークレットは YAML や tf ファイルに直接書かず、変数（`sensitive = true`）や Secrets Manager 参照（`${{ :secrets:<namespace>:<key> }}`）を使う
4. このファイルの「レシピ一覧」に追記する

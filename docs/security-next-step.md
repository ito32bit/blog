# 次の一手（実行優先順）

このリポジトリで Dependabot セキュリティエラーを実際に減らすための、次の具体アクションです。

## 1. Lockfile を必須化する（今回追加）

- `.github/workflows/lockfile-guard.yml` を追加し、`Gemfile` / `Gemfile.lock` が変更された push / PR で、`Gemfile.lock` 欠落時に失敗させます。
- 目的: Bundler の依存解決を固定し、Dependabot の修正提案を再現可能にするため。

## 2. `Gemfile.lock` を作成してコミット（最優先）

この環境では `rubygems.org` へのアクセスが `403` で失敗するため、ローカル環境または GitHub Actions で実施してください。

```bash
bundle lock
bundle exec jekyll build
git add Gemfile.lock
git commit -m "chore(deps): add Gemfile.lock for reproducible security updates"
```

## 2-1. Lockfile 自動更新ワークフロー（今回追加）

- `.github/workflows/update-gemfile-lock.yml` を追加し、`workflow_dispatch` または毎週実行で `bundle lock` を実施します。
- `Gemfile.lock` に差分があれば自動で PR を作成します。

## 3. Dependabot アラートの潰し方

1. Security タブで Critical / High を優先
2. `direct` 依存は Dependabot PR をそのままマージ
3. `transitive` は親依存（主に `github-pages`）の更新で解消
4. 1件ごとに「再現手順」「修正PR」「リリース日」を記録

## 4. 同梱 JS（`assets/lib`）への対応

- Dependabot 対象外なので、将来は npm 管理または CDN + SRI に移行
- 既存の旧版ライブラリ（jQuery 2.1.3 / fancyBox 2.1.5 / UAParser 0.7.9 / Velocity 1.2.x）は優先度をつけて段階更新

## 5. 期待する完了条件

- `Gemfile.lock` が main に存在
- Dependabot Critical / High が 0
- dependency-review + lockfile-guard が Required Check


## 6. 今回のアラート（2026-03-29）への即応

受信した digest に基づき、次の順に対応してください。

1. `nokogiri`（Critical を含むため最優先）
2. `activesupport`
3. `commonmarker`

手順（GitHub Actions の `Update Gemfile.lock` を手動実行）:

- `gems` 入力に `nokogiri activesupport commonmarker` を指定（workflow が1件ずつ更新を試行）
- 自動作成された PR を確認し、テスト通過後にマージ
- Security タブで該当 GHSA/CVE が解消されたことを確認

> 補足: `github-pages` 依存制約で解決不能な場合は、`github-pages` の更新PRを先に取り込む必要があります。

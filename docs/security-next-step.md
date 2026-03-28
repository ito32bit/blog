# 次の一手（実行優先順）

このリポジトリで Dependabot セキュリティエラーを実際に減らすための、次の具体アクションです。

## 1. Lockfile を必須化する（今回追加）

- `.github/workflows/lockfile-guard.yml` を追加し、`Gemfile.lock` がない状態の push / PR を失敗させます。
- 目的: Bundler の依存解決を固定し、Dependabot の修正提案を再現可能にするため。

## 2. `Gemfile.lock` を作成してコミット（最優先）

この環境では `rubygems.org` へのアクセスが `403` で失敗するため、ローカル環境または GitHub Actions で実施してください。

```bash
bundle lock
bundle exec jekyll build
git add Gemfile.lock
git commit -m "chore(deps): add Gemfile.lock for reproducible security updates"
```

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

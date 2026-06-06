# Dependabot セキュリティ警告への改善提案（更新版）

> 対象: `https://github.com/ito32bit/blog/security/dependabot`

## 0. いま起きている問題の整理

Dependabot の警告が残る主因は、次の 2 つに分かれます。

1. **Bundler 依存（`Gemfile` / `Gemfile.lock`）**
   - `github-pages` は依存を広く固定するため、修正に lockfile 運用が必須です。
2. **同梱（vendored）JS 依存（`assets/lib/`）**
   - Dependabot では直接監視されず、古いライブラリが放置されやすいです。

## 1. 今回の改善（運用を強化）

### 1-1. Dependabot 設定を強化

- Bundler チェックを **weekly → daily** に変更
- `bundler-security` グループを追加し、**security updates を最優先で自動集約**
- `rebase-strategy: auto` を追加して、競合で止まりにくくする
- `target-branch: main` を明示して更新先を固定

### 1-2. PR 時点で脆弱依存をブロック

- `.github/workflows/dependency-review.yml` を追加
- `actions/dependency-review-action@v4` で、**High 以上が新規追加された PR を fail**

## 2. 直近で実施すべき対応（アラート解消用）

1. **`Gemfile.lock` を追加して Dependabot 修正 PR を有効化**
   - lockfile がないと脆弱性修正の再現性が低く、Dependabot の提案精度も落ちます。

2. **Dependabot 画面で Critical / High を先に解消**
   - 各アラートを `direct` / `transitive` に分類し、次の順で対応。
     - A: direct dependency の修正PRをマージ
     - B: transitive は親 gem（多くは `github-pages` 周辺）更新で吸収

3. **`assets/lib/` の旧版 JS を段階的に撤去**
   - 現在確認できる旧版例:
     - jQuery `v2.1.3`
     - fancyBox `2.1.5`
     - UAParser.js `0.7.9`
     - Velocity `1.2.2`
   - これらは Dependabot の対象外になりやすいため、
     npm 管理または CDN + SRI へ移行して継続更新可能にします。

## 3. 推奨ロードマップ

- **Day 1–2**
  - `Gemfile.lock` を生成・コミット
  - Dependabot の security PR を優先マージ
- **Week 1**
  - Critical / High を 0 件化
  - dependency-review を Required Check に設定
- **Week 2–3**
  - `assets/lib/` の旧版 JS を更新方式ごと移行（npm or CDN+SRI）
- **継続運用**
  - 月次で Medium/Low を削減し、例外は issue で期限管理

## 4. 補足

この環境では `bundle lock` 実行時に `rubygems.org` へのアクセスが `403 Forbidden` となるため、
lockfile 作成は CI またはローカル環境での実行が前提になります。

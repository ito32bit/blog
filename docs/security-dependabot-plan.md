# Dependabot セキュリティ警告への改善提案

> 対象: `https://github.com/ito32bit/blog/security/dependabot`

このリポジトリは Jekyll + `github-pages` gem を利用しています。`github-pages` は依存関係を幅広く固定するため、**直接依存の更新だけでは警告が解消しない**ケースがあります。

## 1. まず実施すること（即効性あり）

1. **Dependabot を Bundler + GitHub Actions で有効化**
   - 本変更で `.github/dependabot.yml` を追加済み。
   - 毎週更新 PR を作成し、セキュリティ更新の取り込みを定常化します。

2. **`Gemfile.lock` をリポジトリ管理に追加**
   - 現状 lockfile が無いため、環境ごとに異なる解決結果になります。
   - Dependabot の修正 PR も lockfile ありの方が再現性が高くなります。

3. **高優先度アラート（Critical/High）から順に対応**
   - Dependabot 画面で CVE/GHSA ごとに、
     - `direct dependency`（直接依存）
     - `transitive dependency`（間接依存）
     を分類して着手します。

## 2. 根本対策（Medium 以上を減らす）

1. **`github-pages` のメジャー追従**
   - `~> 232` のままだと取り込めない修正が出る可能性があります。
   - `Gemfile.lock` 作成後、`bundle update github-pages` で更新可能範囲を確認し、
     CI でビルド検証を通して段階的に上げる運用にします。

2. **古い同梱 JS ライブラリの棚卸し**
   - `assets/lib/` 配下に旧版ライブラリが多数存在します（jQuery/fancybox/ua-parser など）。
   - これらは Dependabot の監視対象外になりやすいため、
     npm 管理へ移行 or CDN + SRI へ置換して追従性を上げるのが有効です。

3. **脆弱性スキャンの自動化**
   - GitHub Advanced Security 利用時は CodeQL/Dependency Review を必須化。
   - PR マージ条件に「High 以上の新規脆弱性なし」を設定します。

## 3. 実施順（推奨ロードマップ）

- Week 1:
  - Dependabot 設定導入（今回）
  - `Gemfile.lock` を作成・コミット
  - Critical/High を 0 にする
- Week 2:
  - `github-pages` 更新の検証
  - 影響の少ない JS ライブラリから更新方式を統一
- Week 3 以降:
  - 月次で Medium/Low の削減
  - スキャン結果を issue 化して SLA 管理

## 4. 期待効果

- セキュリティ修正 PR の定期化（属人化防止）
- 依存更新の再現性向上（lockfile 運用）
- 将来的な警告再発の抑制（更新運用の仕組み化）

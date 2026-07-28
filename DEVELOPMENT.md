# Development Documentation

このドキュメントは、本ポートフォリオサイトの構造とカスタマイズ方法をまとめたものです。
採用担当者がコードを見る可能性もあるため、実装意図も含めて記録しています。

## 1. 全体構成

`index.html` 1ファイルに HTML / CSS / JS をすべて記述しています。
静的サイトかつ小規模なため、あえてファイル分割やビルドツールを導入せず、
「開いてすぐ動く」状態を優先しました。

```
<head>
  <style>...</style>   ← デザイントークン & 各セクションのCSS
</head>
<body>
  <header>...</header>
  <section class="hero">...</section>
  <section id="works">...</section>
  <section id="skills">...</section>
  <section id="about">...</section>
  <footer id="contact">...</footer>

  <script>
    const works = [...]   ← 作品データ
    const skills = [...]  ← スキルデータ
    // 以降、データを元にDOMを生成する処理
  </script>
</body>
```

## 2. デザイントークン（CSSカスタムプロパティ）

`:root` にまとめています。配色・フォントを変更したい場合はここだけ触れば全体に反映されます。

| 変数 | 用途 |
|---|---|
| `--bg` | 背景色（白） |
| `--bg-alt` | サブ背景（薄いグレー） |
| `--ink` | 基本テキスト色 |
| `--muted` | 補助テキスト色 |
| `--line` | 罫線・ボーダー色 |
| `--accent` | アクセントカラー（ネイビー） |
| `--accent-bright` | ホバー時などの明るいアクセント |
| `--font-display` | 見出し用フォント（Zen Kaku Gothic New） |
| `--font-body` | 本文用フォント（Inter） |
| `--font-mono` | ラベル・タグ用フォント（JetBrains Mono） |

## 3. 作品（Works）の追加・編集

`works` 配列に1オブジェクト追加するだけで、目次・詳細パネルの両方に自動反映されます。

```js
{
  title: "作品名",
  year: "制作年",
  tags: ["React", "TypeScript"],       // 一覧に表示される技術タグ
  summary: "1〜2文の概要",
  description: "詳細説明（詳細パネルに表示）",
  usage: "デモの使い方・セットアップ手順（改行は \n）",
  demoUrl: "https://...",              // Live Demo ボタンのリンク先
  githubUrl: "https://github.com/...", // GitHub ボタンのリンク先
  thumbImage: null,                    // 画像を使う場合はパス/URLを指定
  thumbFrom: "#1e3a5f",                // 画像が無い場合のグラデーション開始色
  thumbTo: "#3d6fb4"                   // グラデーション終了色
}
```

- 配列の並び順がそのまま「目次」の表示順（01, 02...）になります。
- `thumbImage` を指定すると自動的に画像表示に切り替わり、プレースホルダーの「NO IMAGE」表示は消えます。

## 4. スキルの追加・編集

`skills` 配列に `{ name, icon }` を追加するだけです。

```js
{ name: "Docker", icon: "docker" }
```

`icon` は [Simple Icons](https://simpleicons.org/) 上で検索できるスラッグ名です。
`https://cdn.simpleicons.org/{icon}` からロゴ画像を取得しているため、画像ファイルの追加は不要です。

## 5. 主要なUIの実装メモ

- **トラックリスト風の作品一覧**: `.track-row` をクリックすると `aria-expanded` を切り替え、対応する `.track-panel` の `max-height` をアニメーションさせて開閉しています。
- **波線モチーフ**: `.wave` に埋め込んだ SVG の `<path>` を `@keyframes drift` で横方向にゆっくりループさせています。`prefers-reduced-motion` 環境では全アニメーションを無効化しています。
- **スクロールで要素をフェードイン**: `.reveal` クラスを付けた要素を `IntersectionObserver` で監視し、画面内に入ったタイミングで `.in` クラスを付与しています。
- **トップへ戻るボタン**: 一定スクロール量（`window.innerHeight * 0.7`）を超えたら表示し、クリックで `window.scrollTo({ top:0, behavior:'smooth' })` を実行します。

## 6. アクセシビリティ対応

- すべてのインタラクティブ要素はキーボード操作可能（`<button>` / `<a>` を使用）
- フォーカス時に `outline` が表示されるよう `:focus-visible` を定義
- `prefers-reduced-motion: reduce` 環境ではアニメーションを最小化

## 7. 今後の改善候補（TODO）

- [x] `yourname` になっていた GitHub リンクを `ryu-sleep` に置き換え済み
- [ ] 各作品の `thumbImage` に実際のスクリーンショットを設定する
- [ ] `demoUrl` / `githubUrl` を実際のURLに差し替える
- [ ] 独自ドメインを使う場合は GitHub Pages のカスタムドメイン設定を行う

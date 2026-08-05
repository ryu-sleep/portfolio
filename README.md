# Portfolio Site

音楽プレーヤーのトラックリストをモチーフにした、ポートフォリオサイトです。
作品情報やスキルをシンプルに閲覧できるよう、HTML・CSS・JavaScriptのみで実装しています。

https://ryu-sleep.github.io/portfolio/

## 特徴

- 作品一覧を音楽の「トラックリスト」に見立てたUI（クリックで詳細をスライド展開）
- 作品ごとの概要・詳細・デモリンク・GitHubリンクを表示
- スキル一覧をアイコンカードで表示
- レスポンシブ対応（スマートフォン〜デスクトップ）
- キーボード操作、`prefers-reduced-motion` に対応したアクセシビリティ配慮
- `index.html` を開くだけで動作

## 技術スタック

- HTML5 / CSS3（カスタムプロパティ、Grid、Flexbox）
- Vanilla JavaScript（フレームワーク不使用）
- フォント: Google Fonts（Zen Kaku Gothic New / Inter / JetBrains Mono）
- アイコン: [Devicon](https://devicon.dev/)、[Iconify (Logos)](https://icon-sets.iconify.design/logos/) のCDN

## ファイル構成

```
portfolio/
├── index.html      # ページ本体（HTML / CSS / JS すべてこの1ファイル内）
└── README.md
```

## ローカルでの確認方法

`index.html` をブラウザで開くだけで確認できます。

```bash
git clone https://github.com/ryu-sleep/portfolio.git
cd portfolio
open index.html   # Windowsの場合は start index.html
```

## 内容の編集方法

作品・スキルの内容は、`index.html` 内の `<script>` にあるデータ配列を編集するだけで変更できます。

- **作品を追加/編集**: `works` 配列にオブジェクトを1つ追加・編集
- **スキルを追加/編集**: `skills` 配列に `{ name, iconUrl }` を追加・編集
  - `iconUrl` はアイコン画像の直リンクです
  - プログラミング言語・DB・ツール系は [Devicon](https://devicon.dev/) から探すのがおすすめです
  - Adobe製品などは [Iconify (Logos)](https://icon-sets.iconify.design/logos/) から探し、`https://api.iconify.design/logos/アイコン名.svg` の形式で指定します

## デプロイ（GitHub Pages）

1. GitHubにリポジトリを作成しプッシュ
2. リポジトリの **Settings → Pages** を開く
3. **Source** で対象ブランチ（`main`）と `/ (root)` を選択して保存
4. 数分後、`https://ユーザー名.github.io/リポジトリ名/` で公開される

## License

このリポジトリは、個人のポートフォリオとして自由に利用・改変して構いません。

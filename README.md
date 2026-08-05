# Marp Theme

太い文字と蛍光色を使った、技術解説向けのMarpテーマです。

## セットアップ

```bash
npm install
npm run preview
```

ブラウザで `http://localhost:8080` を開きます。

## ファイル

- `theme.css`: Marpカスタムテーマ
- `slides/sample.md`: レイアウト見本
- `slides/assets/`: スライド内で使う画像
- `dist/`: HTML/PDFの出力先

## 主なレイアウト

- `title`: 蛍光イエロー帯付きの表紙
- `section-dark`: 濃いグレーの章扉
- `lead`: 大きな説明文
- `quiz`: 4択クイズ
- `.flow`: 処理フロー
- `.two-column`: 2カラム比較

## 新しいスライドで使う

Markdownの先頭に次のFront Matterを追加します。

```yaml
---
marp: true
theme: tech-bold
paginate: true
size: 16:9
---
```

# FuriDoc Yomi — 振り仮名フォント

[Klee One](https://github.com/fontworks-fonts/Klee)（Fontworks）をベースに、常用漢字＋熟字訓漢字に対して振り仮名グリフを追加したフォントです。IVS（Ideographic Variation Sequence）で読みを選択し、PowerPoint など ruby マークアップ非対応のソフトでも振り仮名を表示できます。

## ダウンロード

[Releases](../../releases) から最新の zip をダウンロードしてください。

| ファイル | 用途 |
|---------|------|
| `FuriDocYomi.ttf` | 横書き用 |
| `FuriDocYomi-Tate.ttf` | 縦書き用 |

## インストール

1. ダウンロードした `.ttf` ファイルをダブルクリック
2. 「インストール」をクリック
3. アプリでフォント「FuriDoc Yomi」を選択

## 使い方

1. フォントをインストール
2. [FuriDoc](https://furidoc.com) で文章を入力（自動的に振り仮名が付きます）
3. 「IVS コピー」で振り仮名付きテキストをクリップボードにコピー
4. PowerPoint や Word など好きなソフトに貼り付け、フォントを「FuriDoc Yomi」に設定

これだけで、ruby マークアップに非対応のソフトでも振り仮名が正しく表示されます。

👉 [PowerPoint での使い方（詳細）](https://furidoc.com/help/ppt-furigana.html)

### 仕組み

通常の ruby（`<ruby>漢<rt>かん</rt></ruby>`）はソフト側のマークアップ対応が必要です。IVS フォントは「漢字＋読み」を一つのグリフに合成し、Unicode Variation Selector で切り替えます：

```
漢       → 通常の漢字グリフ
漢 + VS17 → 漢字グリフ＋上部に「かん」
```

OpenType cmap format 14 に対応していれば（ほぼ全てのモダンソフトが対応）、ruby 処理なしで振り仮名が自動表示されます。

### JavaScript での使用

```js
const VS = (index) => String.fromCodePoint(0xE0100 + index);

'漢' + VS(0)           // → 漢(かん)
'今' + VS(3) + '日'     // → 今日(きょう)  熟字訓
'生' + VS(4) + 'まれる'  // → 生(うま)まれる
```

読みの index は `ivs_manifest.json` を参照してください。

## 動作検証

| 環境 | 結果 | 備考 |
|------|------|------|
| ブラウザ | ✅ | cmap format 14 は広くサポート |
| PowerPoint デスクトップ版スライドショー | ✅ | フォント埋め込みで正常動作 |
| PowerPoint Online 編集 | ✅ | |
| PowerPoint Online スライドショー | ❌ | サーバー側レンダリングのためカスタムフォント非対応 |

## カバー範囲

| 指標 | 値 |
|------|-----|
| 対応漢字数 | 2,240（常用漢字 2,136 + 熟字訓表外漢字 104） |
| 振り仮名パターン数 | 13,083 |
| ソースフォント | Klee One Regular（OFL ライセンス） |

## ライセンス

本フォントは [SIL Open Font License 1.1](LICENSE) の下で公開されています。

### 出典と帰属

| リソース | ライセンス |
|---------|----------|
| [Klee One](https://github.com/fontworks-fonts/Klee) by Fontworks | SIL OFL 1.1 |
| [KANJIDIC2](https://www.edrdg.org/wiki/index.php/KANJIDIC_Project) by EDRDG | CC BY-SA 4.0 |
| [JMdict](https://www.edrdg.org/wiki/index.php/JMdict-EDICT_Dictionary_Project) by EDRDG | CC BY-SA 3.0 |

データファイルの詳細なライセンス情報は [DATA_LICENSE.md](DATA_LICENSE.md) を参照。

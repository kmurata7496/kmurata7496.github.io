# GitHub Pages 更新ガイド（kmurata7496.github.io）

このサイトは GitHub Pages の標準機能（Jekyll）で動いています。
業績・発表・研究費・プロジェクトは `_data/` フォルダの `.yml` ファイルに書かれていて、
GitHub に保存すると 1〜2 分でページに自動反映されます。HTML を直接いじる必要はありません。

---

## 1. ファイル構成

```
kmurata7496.github.io/
├─ index.html              … ページの骨組み（ふだんは触らない）
├─ _config.yml             … サイト設定（ふだんは触らない）
├─ assets/css/style.css    … デザイン（ふだんは触らない）
├─ _data/
│   ├─ publications.yml    … 業績（7区分）
│   ├─ presentations.yml   … 研究発表
│   ├─ grants.yml          … 研究費（代表者のもの）
│   ├─ projects.yml        … プロジェクト
│   └─ laconia_models.yml  … ラコニアの 3D モデル一覧
├─ projects.html           … ラコニア・プロジェクトのページ
└─ UPDATE_GUIDE_ja.md      … このガイド（サイトには表示されません）
```

---

## 2. 最初の入れ替え（1 回だけ）

1. ブラウザで `https://github.com/kmurata7496/kmurata7496.github.io` を開く。
2. 緑の **Code** ボタンの左にある **Add file → Upload files** を選ぶ。
3. 配布した zip を展開し、**中身（index.html, projects.html, _config.yml, _data フォルダ, assets フォルダ, UPDATE_GUIDE_ja.md）をまとめて**アップロード欄にドラッグする。
   - フォルダごとドラッグすれば、`_data/…` や `assets/css/…` の構造が保たれます（Chrome / Edge / Safari で可）。
   - 同名の `index.html` と `projects.html` は自動で上書きされます。
4. ページ下の **Commit changes** を押す。
5. 不要になった古いファイルがあれば削除する（例：`contact.html`）。ファイルを開き、右上の「…」→ **Delete file** → **Commit changes**。
6. **Settings → Pages** を開き、次のようになっているか確認する。
   - Source: **Deploy from a branch**
   - Branch: **main** / **/(root)**
7. **Actions** タブを開き、「pages build and deployment」が緑のチェックになれば公開完了。
   `https://kmurata7496.github.io/` を開いて確認する（古い表示が出たら強制再読み込み：Mac は ⌘+Shift+R、Windows は Ctrl+F5）。

---

## 3. ふだんの更新（業績を 1 件足す場合）

1. リポジトリで `_data/publications.yml` を開く。
2. 右上の **鉛筆アイコン（Edit this file）** を押す。
3. 該当する区分（例：`label: "Journal articles"`）の `items:` の**すぐ下**に、既存の項目をまねて追加する。

   ```yaml
       - year: "2026"
         authors: "K. Murata, H. Hayakawa"
         title: "Title of the New Article"
         venue: "Journal Name"
         post: " 12/3, 45–67"
         doi: "10.xxxx/xxxxx"
         tags: "Refereed"

   ```

   - 行頭の空白（インデント）は既存の項目と**ぴったり同じ**にしてください（`- year` の前に半角スペース 4 つ）。
   - 値はすべて `"…"` で囲みます。不要なフィールド（`doi` や `tags` など）は行ごと省略できます。
   - 日本語業績は英訳タイトルにし、`tags` に `In Japanese` を入れます。
   - 本の章などは `pre: "in T. Masuda (ed.), "` のように、書名の前に来る文字列を `pre` に書きます。
4. 右上の **Commit changes…** → もう一度 **Commit changes** を押す。
5. 1〜2 分後にページに反映されます。

研究発表（`presentations.yml`）、研究費（`grants.yml`）、プロジェクト（`projects.yml`）も同じ手順です。
それぞれのファイルの冒頭に、使えるフィールドの説明を書いてあります。

> 最終更新日（ページ右下の Last updated）はサイトが更新されるたびに自動で変わります。

---

## 4. うまく反映されないとき

- **Actions タブに赤い × が出ている**：たいていは YAML の書き間違いです。赤い項目を開くとエラーのある行番号が出るので、その行の次を確認してください。
  - インデントのずれ（スペースの数が違う、タブ文字が混じっている）
  - `"` の閉じ忘れ
  - 値の中に `"` を使っている → 曲線の引用符 `“ ”` か `‘ ’` に置き換える
- **元に戻したい**：ファイルを開き **History** から以前の版を開いて内容をコピーし、鉛筆アイコンで貼り付けて保存すれば元に戻ります。
- **表示が変わらない**：ブラウザのキャッシュのことが多いので、強制再読み込みしてください。

---

## 5. ラコニアの 3D モデル一覧の更新

3D モデルは Sketchfab 側で **Password-protected** に設定してあるので、リンクが公開されていても、パスワードを知らない人はモデルを表示できません。
プロジェクトページには「レビュー段階のためパスワードが必要」という注記を、冒頭と 3D Models 欄の 2 か所に出しています。

### モデルを追加する

1. Sketchfab でモデルを公開設定 **Password-protected** にしてアップロードする（既存モデルと同じパスワードにしておくと共同研究者が楽です）。
2. モデルの URL から 32 文字の ID（例：`https://sketchfab.com/3d-models/…-d76f0370b6fb405dafde8c16a92bf222` の末尾）を控える。
3. GitHub で `_data/laconia_models.yml` を開き、鉛筆アイコンで番号順の位置に追加する。

   ```yaml
   - code: "105"
     name: "Church Name"
     year: "2026"
     id: "0123456789abcdef0123456789abcdef"

   ```

4. **Commit changes** を押す。件数表示（例：21 models）も自動で変わります。

### 公開段階になったら

Sketchfab で各モデルの設定を Public（または Private）に戻し、`projects.html` の注記 2 か所（`class="notice"` の部分）を削除してください。必要なら文面の書き換えもお手伝いします。

---

## 6. （参考）手元のパソコンから git で更新する場合

```bash
git clone https://github.com/kmurata7496/kmurata7496.github.io.git   # 初回のみ
cd kmurata7496.github.io
git pull                     # 最新の状態を取り込む
# ……_data/*.yml をエディタで編集……
git add .
git commit -m "Add new publication"
git push
```

ブラウザでの編集だけで十分なので、この方法は使わなくても構いません。

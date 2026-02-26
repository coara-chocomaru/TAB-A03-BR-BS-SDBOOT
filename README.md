# SDBOOT作成及び利用手順
---

## 事前準備
0. windowsのPC
1. まず最初に下記URLからファイルをダウンロードして下さい。

```
https://github.com/coara-chocomaru/TAB-A03-BR-BS-SDBOOT/releases/download/TAB-A03-BR/TAB-A03-BR-02.04.000_SU+gapps.zip
```

2. ダウンロードした ZIP を展開します。

---

## ファイル内容
展開後

![展開後のファイル構成](https://raw.githubusercontent.com/coara-chocomaru/TAB-A03-BR-BS-SDBOOT/refs/heads/img/00.JPG)

---

## 使い方（簡易）
1. 展開したフォルダ内で `pack_menu.bat` を実行します。

```
pack_menu.bat
```

2. 正常に実行されると、メニューが表示されます

![pack_menu 実行後のメニュー](https://raw.githubusercontent.com/coara-chocomaru/TAB-A03-BR-BS-SDBOOT/refs/heads/img/01.JPG)

3. 目的の番号を入力します。

- `1` — su のみ
- `2` — su + GMS化
- `3` — バッチを終了

4. 番号を押すと進捗が `%` で表示されます

![進捗表示の例](https://raw.githubusercontent.com/coara-chocomaru/TAB-A03-BR-BS-SDBOOT/refs/heads/img/02.JPG)

5. 完了したら、任意のキーを押してバッチを終了します

![終了時の画面](https://raw.githubusercontent.com/coara-chocomaru/TAB-A03-BR-BS-SDBOOT/refs/heads/img/03.JPG)

---

## imgの確認
展開したフォルダ内に、選択したオプションに応じた `.img` ファイルが作成されているか確認してください。

![生成されたIMG](https://raw.githubusercontent.com/coara-chocomaru/TAB-A03-BR-BS-SDBOOT/refs/heads/img/04.JPG)

---

## SDカードへ書き込み
1. `Win32DiskImager` 等のツールを使って、4GB 以上（推奨: 4GB 〜 32GB）の SD カードへ `.img` を書き込みます。

2. 書き込み済みの SD を本体（BR）に差し込み、電源を入れると `sdboot` が実行されます。

3. 起動には通常より長めの時間がかかることがあります。10分ほど待ってください。

---

## 任意の追加作業（永続suを SD無しで得る方法）
実行すると本体のシステムを書き換え、データ消失・起動不能など重大なリスクがあるため、**必ず自己責任で**行ってください。

1. SD を挿入した状態で下記のように `mmcblk` のパーティションを本体にコピーします

```
/dev/block/mmcblk1p4  -> /dev/block/mmcblk0p14
/dev/block/mmcblk1p6  -> /dev/block/mmcblk0p16
# dd if=/dev/block/mmcblk1p4 of=/dev/block/mmcblk0p14
# dd if=/dev/block/mmcblk1p6 of=/dev/block/mmcblk0p16
```

2. dd が完了したら SD を抜き、端末を再起動します。
3. 正常に起動して初期化（必要に応じて）を行えば、SD が無くても永続的に `su` を使えるようになります。

**重要**: `boot` や `recovery` パーティションを誤って上書きすると端末が起動しなくなります。これらは絶対に書き換えないでください。

---

## トラブルシューティング
- 書き込みに失敗する・起動しない場合は別の SD カードや書き込みソフトで再試行してください。

---

## 免責・警告
- 本ガイドの操作は端末・データに損害を与える可能性があります。操作は自己責任で行ってください。
- 本ファイル中のコマンドは端末や環境によっては **致命的** な結果を招く可能性があります。実行前にコマンドの意味を理解し、必ずデバイス名やパスを確認してください。

---

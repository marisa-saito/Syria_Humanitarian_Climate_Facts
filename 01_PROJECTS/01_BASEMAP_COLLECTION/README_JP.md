# シリア・ベースマップ・コレクション

## 概要

このフォルダには、Python と Folium を用いて作成した 4 種類のシリアのインタラクティブ・ベースマップを収録しています。各 Jupyter Notebook は、同じ行政界データとラベル構成を使用し、背景地図のみを変更しています。

このコレクションは、本リポジトリに収録する人口、気候災害、避難・帰還などの分析において、ベクター・ラスター形式のデータを可視化するための地図基盤として作成しました。

## ベースマップ一覧

- 4 種類のベースマップを収録
- 各マップをインタラクティブ HTML として公開
- 各 Jupyter Notebook から HTML を再生成可能

| No. | インタラクティブ地図 | Jupyter Notebook | ベースマップ | 主な用途 |
|---:|---|---|---|---|
| 01 | [地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/01_syria_white_basemap.html) | [Notebook](01_Syria_White_basemap.ipynb) | CARTO Light — No Labels | 主題レイヤーを重ねるための白背景 |
| 02 | [地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/02_syria_dark_basemap.html) | [Notebook](02_Syria_Dark_basemap.ipynb) | CARTO Dark — No Labels | 明るいレイヤーデータを載せるための黒背景 |
| 03 | [地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/03_syria_satellite_basemap.html) | [Notebook](03_Syria_Satellite_basemap.ipynb) | Esri World Imagery | 地表の状況を確認するための衛星画像 |
| 04 | [地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/04_syria_physical_basemap.html) | [Notebook](04_Syria_Physical_basemap.ipynb) | Esri World Terrain | 地形を確認するための地形図 |

## 01 — ホワイト・ベースマップ

地名表記のない CARTO Light を背景に使用し、行政界と周辺国名をプロジェクト側で追加。主題データを視覚的に目立たせたい場合に適した、白いベースマップです。

[インタラクティブ地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/01_syria_white_basemap.html)

![Syria White Basemap](images/01_syria_white_basemap.png)

## 02 — ダーク・ベースマップ

地名表記のない CARTO Dark を背景に使用し、明るいカラーの行政界と周辺国名をプロジェクト側で追加。人口ラスターや比例円など、暗い背景上でコントラストを必要とするデータ表示に適しています。

[インタラクティブ地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/02_syria_dark_basemap.html)

![Syria Dark Basemap](images/02_syria_dark_basemap.png)

## 03 — 衛星ベースマップ

Esri World Imagery を背景に使用し、行政界と周辺国名をプロジェクト側で追加。土地被覆や地表の状況を確認しながら、行政区分との位置関係を把握できます。

[インタラクティブ地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/03_syria_satellite_basemap.html)

![Syria Satellite Basemap](images/03_syria_satellite_basemap.png)

## 04 — 地形ベースマップ

Esri World Terrain を背景に使用し、行政界と周辺国名をプロジェクト側で追加。標高や地形の起伏、地域的な位置関係を確認するための地図基盤として利用できます。

[インタラクティブ地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/01_BASEMAP_COLLECTION/04_syria_physical_basemap.html)

![Syria Physical Basemap](images/04_syria_physical_basemap.png)

## 共通仕様

- シリアの国境と 14 県の県境を表示
- 県名と周辺国名をプロジェクト側で追加
- Folium によるインタラクティブ地図
- HTML 形式での保存と Jupyter Notebook 上での表示
- 各 Jupyter Notebook で共通する地図範囲とラベル構成

## データ

行政界データ：

- `syr_admin0.geojson`
- `syr_admin1.geojson`

出典：HDX OCHA, Syria subnational administrative boundaries

## 使用技術

- Python
- Folium
- Jupyter Notebook
- HTML / CSS

## 実行方法

各 Jupyter Notebook を上から順に実行すると、対応するインタラクティブ地図が HTML ファイルとして保存され、Jupyter Notebook 上にも表示されます。

## 注意事項

- 背景タイルの利用にはインターネット接続が必要です。
- 背景地図と行政界データには、それぞれの提供元の利用条件と帰属表示が適用されます。
- 本コレクションは分析用の地図基盤であり、行政界の法的な位置づけを示すものではありません。

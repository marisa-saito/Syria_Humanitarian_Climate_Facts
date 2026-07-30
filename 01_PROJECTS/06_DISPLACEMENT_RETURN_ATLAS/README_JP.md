# シリア避難・帰還アトラス

## 概要

このフォルダには、IOM (International Organization for Migration)の 2026 年避難・帰還ベースラインデータと HOTOSM (Humanitarian OpenStreetMap Team) の集落ポイントを統合した、シリア避難・帰還アトラスの英語版と日本語版を収録しています。

IOM データには地点別の人口指標がありますが、地点ジオメトリは含まれていません。そのため、同一の ADM3 Pcode を持つ HOTOSM 集落ポイントを候補とし、正規化した地名と文字列類似度を用いて一対一で照合しています。定義した採用基準を満たす地点のみを地図へ表示し、候補、類似度、採用判定、除外理由を監査用データとして保存しています。

## アトラス一覧

- IOM の人口指標と HOTOSM の地点ジオメトリを統合
- ADM3 Pcode と地名類似度による地点照合
- 完全一致または類似度 85% 以上のみを自動採用
- 同一の HOTOSM ポイントを複数地点へ割り当てない一対一照合
- 5 種類の人口指標を共通の比例円スケールで表示
- 英語版と日本語版のインタラクティブ HTML を出力

| No. | インタラクティブ地図 | Jupyter Notebook | 表示言語 | 分析内容 |
|---:|---|---|---|---|
| 01 | [地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/06_DISPLACEMENT_RETURN_ATLAS/01_syria_displacement_and_return_atlas.html) | [Notebook](01_Syria_Displacement_and_Return_Atlas.ipynb) | 英語 | IOM・HOTOSM 地点照合と避難・帰還指標 |
| 02 | [地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/06_DISPLACEMENT_RETURN_ATLAS/02_syria_displacement_and_return_atlas_jp.html) | [Notebook](02_Syria_Displacement_and_Return_Atlas_JP.ipynb) | 日本語 | IOM・HOTOSM 地点照合と避難・帰還指標 |

## データ統合と地点照合

IOM の避難・帰還データを使用し、地点ジオメトリを持つ HOTOSM 集落データと統合します。同一の ADM3 Pcode 内で上位 3 件の候補を作成し、アラビア語地名の英字転写を含む表記揺れを、正規化した地名と文字列類似度によって評価します。

主な処理：

- IOM と HOTOSM の列、CRS、ジオメトリの検証
- IOM の行政区分列と人口指標列の標準化
- 人口値の欠損、非数値、無限値、負数の検証
- 2026 年の値が 2024 年 12 月以降の累計値を超えないことの検証
- 人口構成項目から総人口を再計算し、報告値と照合
- HOTOSM から Point 形式の集落地物のみを抽出
- IOM と HOTOSM の地名を正規化
- 同一の ADM3 Pcode 内で上位 3 件の候補を作成
- 直接比較と語順を揃えた比較による文字列類似度の計算
- 完全一致または類似度 85% 以上の候補を自動採用
- 同一の HOTOSM ポイントを重複使用しない決定的な一対一割当
- 採用、要確認、重複競合、候補なしの判定
- 監査 CSV と検証済み GeoPackage の保存
- 5 種類の人口指標を共通の比例円スケールで表示

[英語版インタラクティブ地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/06_DISPLACEMENT_RETURN_ATLAS/01_syria_displacement_and_return_atlas.html)

[日本語版インタラクティブ地図を表示](https://marisa-saito.github.io/Syria_Humanitarian_Climate_Facts/01_PROJECTS/06_DISPLACEMENT_RETURN_ATLAS/02_syria_displacement_and_return_atlas_jp.html)

## 照合結果

| 項目 | 件数 | 割合・内訳 |
|---|---:|---|
| IOM 元データ | 8,394 | 100% |
| HOTOSM 候補あり | 8,391 | 99.96% |
| 自動採用 | 2,455 | 29.25% |
| 完全一致 | 1,260 | 自動採用に含む |
| 高信頼度 | 1,195 | 類似度 85% 以上 |
| 要確認 | 5,922 | 監査データに保持 |
| 重複競合 | 14 | 監査データに保持 |
| 候補なし | 3 | 監査データに保持 |

自動採用した 2,455 地点では、IOM 地点コードと HOTOSM ID の重複、採用基準未満の照合、ADM3 Pcode の不一致がないことを検証しています。

## 表示指標

| 人口指標 | 表示地点 | 表示人数 | IOM 元データに対する割合 |
|---|---:|---:|---:|
| 居住者 | 2,180 | 6,094,064 | 32.73% |
| 国内避難民（IDP） | 809 | 2,568,776 | 43.76% |
| IDP 帰還者（2024 年 12 月以降） | 959 | 808,746 | 38.90% |
| IDP 帰還者（2026 年） | 415 | 67,992 | 42.37% |
| 総人口 | 2,353 | 9,921,264 | 35.55% |

5 種類の人口指標には共通の比例円スケールを使用しています。円の面積を人口に比例させ、極端に大きい値は全指標の 99 パーセンタイルを基準とする最大サイズに制限して、レイヤー間の比較可能性と地図上の視認性を保っています。

## 派生データ

- `outputs/iom_hotosm_location_matching_audit.csv`
  - 8,394 件すべての最良候補、類似度、採用判定、除外理由を保存
- `outputs/iom_displacement_return_locations_validated.gpkg`
  - 自動採用した 2,455 地点の IOM 人口指標と HOTOSM ジオメトリを保存

## データ

避難・帰還データ：

- `iom_displacement_return_2026.xlsx`

出典：International Organization for Migration（IOM）

集落ポイントデータ：

- `hotosm_populated_places.gpkg`

出典：Humanitarian OpenStreetMap Team（HOTOSM）/ OpenStreetMap contributors

行政界データ：

- `syr_admin0.geojson`
- `syr_admin1.geojson`

出典：HDX OCHA, Syria administrative boundaries

河川・水域データ：

- `syr_rivers_3857.geojson`
- `syr_lakes_4326.geojson`

出典：OpenStreetMap contributors

## 使用技術

- Python
- Pandas
- GeoPandas
- Folium
- difflib
- Branca
- GeoPackage

## 実行方法

`01_Syria_Displacement_and_Return_Atlas.ipynb` を上から順に実行すると、データ検証、地点照合、採用判定、監査データの保存、人口指標レイヤーの作成が行われます。英語版アトラスは `01_syria_displacement_and_return_atlas.html` として保存され、Jupyter Notebook 上にも表示されます。

`02_Syria_Displacement_and_Return_Atlas_JP.ipynb` を上から順に実行すると、同じ分析結果を使用した日本語版アトラスが `02_syria_displacement_and_return_atlas_jp.html` として保存され、Jupyter Notebook 上にも表示されます。

## 注意事項

- IOM 地点は、照合された HOTOSM 集落ポイントの座標を用いて表示しています。
- 地図上の座標は照合処理から得た参照地点であり、IOM が提供した元座標ではありません。
- 地名の類似度だけでは、2 つのレコードが同一集落を示すことを証明できません。
- 照合候補は、同一の ADM3 Pcode を持つ地点間に限定しています。
- 完全一致または類似度 85% 以上で、一意性基準を満たす地点のみを主要人口レイヤーに使用しています。
- 類似度 70% 以上 85% 未満は要確認とし、70% 未満、候補なし、重複競合を含めて監査用出力に残しています。
- 表示人数と割合は、自動採用した 2,455 地点のみを対象としており、IOM 元データ全体を表すものではありません。
- 人口指標は、IOM 元データの定義と報告期間に基づきます。
- 本アトラスは、リアルタイムの避難・帰還状況を示すものではありません。
- 背景タイルの利用にはインターネット接続が必要です。
- 背景地図、行政界、河川・水域データには、それぞれの提供元の利用条件と帰属表示が適用されます。
- 本アトラスは分析用の地図であり、行政界の法的な位置づけを示すものではありません。

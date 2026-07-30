# Syria_Humanitarian_Climate_Facts データカタログ

[English](DATA_CATALOG.md)

## 概要

このカタログには、`Syria_Humanitarian_Climate_Facts`ポートフォリオの6つのコレクションで使用する元データを記録し、プロジェクトから生成した派生データと区別して掲載しています。

`02_DATA/`以下の元データはローカル環境で管理し、ファイル容量と各提供元の利用条件を考慮して、公開GitHubリポジトリには収録していません。Jupyter Notebookを実行する場合は、それぞれの提供元から必要なデータを取得してください。小容量の派生成果物は各プロジェクトフォルダに収録し、再生成可能な大容量成果物はGitの対象外としています。

## 元データ一覧

| 分類 | ローカルファイル | 提供元 | 形式 | 使用コレクション |
|---|---|---|---|---|
| ラスタ | `worldpop_syria_2026.tif` | WorldPop | GeoTIFF | 02、04 |
| 表形式 | `climap_euphrates_flood_affected_locations.csv` | ユーザー管理のプロジェクトデータ | CSV | 05 |
| 表形式 | `iom_displacement_return_2026.xlsx` | International Organization for Migration（IOM） | XLSX | 06 |
| ベクター | `hotosm_populated_places.gpkg` | Humanitarian OpenStreetMap Team（HOTOSM）/ OpenStreetMap contributors | GeoPackage | 06 |
| ベクター | `syr_admin0.geojson`〜`syr_admin3.geojson` | HDX OCHA | GeoJSON | 01〜06 |
| ベクター | `syr_admincapitals.geojson` | HDX OCHA | GeoJSON | 参照データ |
| ベクター | `syr_adminlines.geojson` | HDX OCHA | GeoJSON | 参照データ |
| ベクター | `syr_adminpoints.geojson` | HDX OCHA | GeoJSON | 03 |
| ベクター | `syr_rivers_3857.geojson` | OpenStreetMap contributors | GeoJSON | 03、05、06 |
| ベクター | `syr_lakes_4326.geojson` | OpenStreetMap contributors | GeoJSON | 03、05、06 |

## ラスタ元データ

### `worldpop_syria_2026.tif`

- ローカルパス：`02_DATA/RASTER/worldpop_syria_2026.tif`
- 提供元：WorldPop
- データセット：Syrian Arab Republic — Spatial Distribution of Population、2026年推計
- 元資料名：`syr_pop_2026_CN_100m_R2025A_v1`
- バージョン：R2025A v1
- 形式：単一バンドGeoTIFF、`float32`
- CRS：EPSG:4326
- グリッド：7,992 × 6,011セル
- 解像度：3秒角、赤道付近で約100 m
- 単位：グリッドセルごとの推計人口
- NoData：`-99999`
- WorldPop出典ページの作成日：2025年9月1日
- ファイル内メタデータのライセンス：CC BY 4.0
- 使用コレクション：02 人口分析、04 ラスタ解析
- 出典ページ：[WorldPopデータセット概要](https://hub.worldpop.org/geodata/summary?id=75632)
- DOI：[10.5258/SOTON/WP00839](https://doi.org/10.5258/SOTON/WP00839)

## 表形式元データ

### `climap_euphrates_flood_affected_locations.csv`

- ローカルパス：`02_DATA/TABULAR/climap_euphrates_flood_affected_locations.csv`
- 提供元：人道支援報告を基に作成したユーザー管理のプロジェクトデータ
- 形式：CSV
- レコード数：6地点
- 列数：12
- 現在記録している事象日：2026年5月25日
- 空間情報：WGS 84の緯度・経度
- 使用コレクション：05 気候災害マッピング
- 出典資料：
  - [UNFPA — Euphrates Floods Flash Update（25 May–6 June 2026）](https://reliefweb.int/report/syrian-arab-republic/unfpa-syria-flash-update-euphrates-floods-raqqa-and-deir-ez-zor-25-may-6-june-2026)
  - [WFP — Euphrates River Flood Assessment（June 2026）](https://reliefweb.int/report/syrian-arab-republic/wfp-satellite-based-flood-extent-agricultural-impact-assessment-euphrates-river-flood-deir-ez-zor-governorate-june-2026)
  - [Oxfam — Euphrates River Flood Rapid Needs Assessment: Deir ez-Zor Irrigation Sites（May 2026）](https://reliefweb.int/report/syrian-arab-republic/rapid-needs-assessment-euphrates-river-flood-deir-ez-zor-rrigations-sites-may-2026)
  - [IFRC — Euphrates River Floods DREF Operation（MDRSY019）](https://reliefweb.int/report/syrian-arab-republic/syrian-arab-republic-euphrates-river-floods-2026-dref-operation-mdrsy019)
- 閲覧日：2026年7月1日

### `iom_displacement_return_2026.xlsx`

- ローカルパス：`02_DATA/TABULAR/iom_displacement_return_2026.xlsx`
- 提供元：International Organization for Migration（IOM）、Displacement Tracking Matrix（DTM）
- 元ファイル名：`Baseline April 2026_public.xlsx`
- 形式：XLSX
- シート：`Short Baseline`、`Dataset`
- `Short Baseline`：8,394行 × 20列
- `Dataset`：8,394行 × 137列
- プロジェクトで使用するシート：`Short Baseline`
- データ範囲：集落単位の人口、避難、帰還指標
- 使用コレクション：06 避難・帰還アトラス
- 公式ページ：[IOM DTM — Syrian Arab Republic](https://dtm.iom.int/syrian-arab-republic)

このExcelには人口指標が含まれていますが、アトラスで使用する地点ジオメトリは含まれていません。プロジェクトでは、定義したPCODE、地名類似度、一対一割当の基準によって、IOM地点をHOTOSM集落ポイントと照合しています。

## ベクター元データ

### シリア行政界データ

- ローカルディレクトリ：`02_DATA/VECTOR/`
- 提供元：HDX OCHA
- データセット：Syria subnational administrative boundaries
- 形式：GeoJSON
- ファイルに記録されたCRS：OGC CRS84
- ファイルに記録された行政界バージョン：v02
- ADM0〜ADM3に記録された有効日：2020年12月17日
- 出典ページ：[HDX — Syrian Arab Republic administrative boundaries](https://data.humdata.org/dataset/cod-ab-syr)

| ローカルファイル | ジオメトリ | 地物数 | 主な用途 |
|---|---|---:|---|
| `syr_admin0.geojson` | MultiPolygon | 1 | 国境 |
| `syr_admin1.geojson` | Polygon / MultiPolygon | 14 | 県境 |
| `syr_admin2.geojson` | Polygon / MultiPolygon | 62 | 郡境とPCODE |
| `syr_admin3.geojson` | Polygon | 272 | 地区境とPCODE |
| `syr_admincapitals.geojson` | Point | 266 | 行政中心地点の参照データ |
| `syr_adminlines.geojson` | LineString | 811 | 行政界線の参照データ |
| `syr_adminpoints.geojson` | Point | 349 | Spatial Joinで使用する行政地点 |

### `hotosm_populated_places.gpkg`

- ローカルパス：`02_DATA/VECTOR/hotosm_populated_places.gpkg`
- 提供元：Humanitarian OpenStreetMap Team（HOTOSM）/ OpenStreetMap contributors
- ローカルレイヤー：`populated_places`
- 形式：GeoPackage
- CRS：EPSG:4326
- 元データの全地物数：29,863
- ジオメトリ構成：Point 8,995、Polygon 20,840、MultiPolygon 27、LineString 1
- 06で使用するPoint地物：8,995
- 主な属性：OSM ID、多言語地名、集落種別、人口、ADM0〜ADM4 PCODE
- 使用コレクション：06 避難・帰還アトラス
- データセットページ：[HDX — HOTOSM Syria populated places](https://data.humdata.org/dataset/hotosm_syr_populated_places)
- ライセンスと帰属表示：[OpenStreetMapの著作権とライセンス](https://www.openstreetmap.org/copyright)

### `syr_rivers_3857.geojson`

- ローカルパス：`02_DATA/VECTOR/syr_rivers_3857.geojson`
- 提供元：OpenStreetMap contributors
- 形式：GeoJSON
- CRS：EPSG:3857
- 地物数：12,034
- ジオメトリ：LineString / MultiLineString
- 使用コレクション：03 ベクター解析、05 気候災害マッピング、06 避難・帰還アトラス
- ライセンスと帰属表示：[OpenStreetMapの著作権とライセンス](https://www.openstreetmap.org/copyright)
- 元データの取得URLと閲覧日：未記録

### `syr_lakes_4326.geojson`

- ローカルパス：`02_DATA/VECTOR/syr_lakes_4326.geojson`
- 提供元：OpenStreetMap contributors
- 形式：GeoJSON
- プロジェクトで使用するCRS：EPSG:4326
- 地物数：2,925
- ジオメトリ：Polygon / MultiPolygon
- 使用コレクション：03 ベクター解析、05 気候災害マッピング、06 避難・帰還アトラス
- ライセンスと帰属表示：[OpenStreetMapの著作権とライセンス](https://www.openstreetmap.org/copyright)
- 元データの取得URLと閲覧日：未記録

## プロジェクト派生データ

次のファイルはJupyter Notebookから生成する成果物であり、独立した元データではありません。

| プロジェクト | 派生成果物 | 用途 | 公開リポジトリ |
|---:|---|---|---|
| 02 | `outputs/worldpop_idleb_2026.tif` | Idleb県でマスク処理したWorldPopラスタ | 収録 |
| 03 | `outputs/syr_river_buffer_10km.gpkg` | 全解像度の河川10 kmバッファ | 未収録、再生成可能 |
| 03 | `outputs/syr_custom_analytical_regions.gpkg` | 独自の4分析地域のDissolve結果 | 未収録、再生成可能 |
| 03 | `outputs/syr_adminpoints_with_governorate.gpkg` | 検証済み県属性を付与した行政地点 | 未収録、再生成可能 |
| 03 | `outputs/syr_hydrography_aligned_4326.gpkg` | EPSG:4326へ統一した全解像度の河川・水域データ | 未収録、再生成可能 |
| 04 | `outputs/worldpop_syria_2026_aggregated_approx_1km.tif` | 約1 kmへ集約した人口ラスタ | 未収録、再生成可能 |
| 04 | `outputs/worldpop_syria_2026_reprojected_3857.tif` | EPSG:3857へ再投影した人口ラスタ | 未収録、再生成可能 |
| 05 | `outputs/euphrates_flood_affected_locations_validated.gpkg` | 検証済み洪水被害報告地点 | 収録 |
| 06 | `outputs/iom_hotosm_location_matching_audit.csv` | IOM 8,394件すべての候補、類似度、判定、理由 | 収録 |
| 06 | `outputs/iom_displacement_return_locations_validated.gpkg` | HOTOSMジオメトリを付与した自動採用2,455地点 | 収録 |

## リポジトリと再現方法

- `02_DATA/`は`.gitignore`によって除外し、GitHubでは公開していません。
- Notebook内のパスを変更しない場合は、上記のローカルファイル名とディレクトリ構成を維持してください。
- レビューと監査に使用する小容量の派生成果物は公開リポジトリへ収録しています。
- 大容量の派生成果物は、対応するNotebookから再生成できるため公開リポジトリには収録していません。

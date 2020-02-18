---
title: クエリ
kind: documentation
aliases:
  - /ja/graphing/using_graphs/
description: データを問い合わせてインサイトを得る
further_reading:
  - link: 'https://learn.datadoghq.com/course/view.php?id=8'
    tag: ラーニングセンター
    text: ダッシュボードをより効果的に活用する
---
## 概要

Datadog では、メトリクス、モニター、ダッシュボード、ノートブックなどのすべてのグラフで同じ基本機能は使用しています。このページでは、グラフエディターのクエリについて説明します。上級レベルのユーザーは、JSON を使用したグラフの作成や編集が可能です。 詳細については、[JSON を使用したグラフ作成][1]をご参照ください。

## グラフエディター

ウィジェットで、右上隅の鉛筆アイコンをクリックしてグラフエディターを開きます。グラフエディターには以下のタブがあります。

* **Share**: 任意の外部 Web ページにグラフを埋め込みます。
* **JSON**: より柔軟性の高いエディター。グラフ定義言語の知識が必要です。
* **Edit**: グラフ作成オプションのデフォルトの UI タブ。

初めてグラフエディターを開くと、**Edit** タブが表示されます。UI からほとんどの設定を選択できます。以下に例を示します。

{{< img src="dashboards/querying/references-graphing-edit-window-with-y.png" alt="グラフエディターの Edit タブ"  style="width:75%;" >}}

## グラフを構成する

ダッシュボードでグラフを構成するには、次のプロセスに従ってください。

1. [可視化に使用するウィジェットを選択する](#select-your-visualization)
2. [グラフ化するメトリクスを選択する](#choose-the-metric-to-graph)
3. [フィルター](#filter)
4. [集計、ロールアップする](#aggregate-and-rollup)
5. [追加の関数を適用する](#advanced-graphing)
6. [グラフのタイトルを決める](#create-a-title)

### 可視化に使用するウィジェットを選択する

利用可能な[ウィジェット][2]から視覚化に使用するウィジェットを選択します。

### グラフ化するメトリクスを選択する

グラフ化するメトリクスを検索するか、**Metric** の横のドロップダウンから選択して決定します。使用するメトリクスが不明な場合は、[メトリクスエクスプローラー][3]か[ノートブック][4]で開始するとよいでしょう。[Metrics Summary ページ][5]のメトリクス一覧を参考にすることもできます。

### フィルター

選択したメトリクスには、メトリクスの右側にある **from** ドロップダウンからホストまたはタグによるフィルターを設定することができます。デフォルトでは *(everywhere)* に設定されています。タグの詳細情報については、[タグ付け][6]ドキュメントをご参照ください。

### 集計、ロールアップする

#### 集計の方法

集計方法は、フィルターのドロップダウンの隣に表示されます。デフォルトでは `avg by` に設定されていますが、`max by`、`min by`、`sum by` に変更できます。ほとんどの場合、メトリクスは多数のホストやインスタンスから集計されるため、時間間隔ごとに多数の値が含まれています。選択した集計方法によって、メトリクスを 1 本の線に集計する方法が決まります。

#### 集計グループ

集約方法のドロップダウンの隣から、グラフ上で線またはグループを構成する要素を選択します。たとえば、`host` を選択すると、各 `host`  につき 1 本の線が表示されます。各線は、特定の `host` に関する選択されたメトリクスで構成されており、選択した方法により集約されます。

#### ロールアップして長期にわたる集計を表示する

前述の手順で選択したオプションに関係なく、グラフの表示ウィンドウに物理的なサイズ制約があることから、データは常にある程度集約されています。メトリクスが毎秒更新され、4 時間分のデータを表示する場合、全データを表示するには 14,400 ポイントが必要です。この期間内に各グラフで表示できるポイント数は 300 です。そのため、画面上の 1 ポイントは 48 データポイントに相当します。

実際には、メトリクスは Agent によって 15～20 秒ごとに収集されます。そのため、1 日分のデータは 4,320 データポイントとなります。1 つのグラフで 1 日分のデータを表示する場合、Datadog は自動的にデータをロールアップします。詳細については、[メトリクスのはじめに][7]をご参照ください。

データを手動でロールアップするには、[丸め関数][8] を使用します。集計グループの右側にあるプラス記号をクリックして、ドロップダウンから `rollup` を選択します。次に、データの集計方法と間隔 (秒) を選択します。

このクエリにより、60 秒のバケットでマシン全体の合計空きディスク容量の平均値を平均でロールアップしたことを表す 1  本の線を作成します。

{{< img src="dashboards/querying/references-graphing-rollup-example.png" alt="ロールアップの例"  style="width:90%;">}}

JSON ビューに切り替えると、以下のようなクエリが表示されます。

```text
"q": "avg:system.disk.free{*}.rollup(avg, 60)"
```

JSON ビューの使用方法については、[JSON を使用したグラフ作成][1]をご参照ください。

### 高度なグラフの作成

分析のニーズに応じて、割合、微分係数、平滑化など、他の数学関数をクエリに適用することもできます。詳細については、[使用可能な関数のリスト][9]をご参照ください。

また、Datadog では、さまざまな算術演算によりメトリクスをグラフ化できます。グラフに表示される 値を変更するには、`+`、`-`、`/`、`*` を使用します。この構文では、整数値、および複数のメトリクスを使用した演算の両方を使用できます。

#### 整数を使用したメトリクスの演算

グラフでメトリクス値の表示方法を変更するには、算術演算を実行します。たとえば、特定のメトリクスの 2 倍の値を視覚化するには、グラフエディターで **Advanced...** リンクをクリックします。次に、`Formula` ボックスに計算式 (この例では `a * 2`) を入力します。

{{< img src="dashboards/querying/arithmetic_2.png" alt="計算式 2"  style="width:75%;" >}}

#### 2 つのメトリクス間の計算

メトリクスの割合を視覚化するには、1 つのメトリクスをもう 1 つのメトリクスで除算します。以下に例を示します。

```text
jvm.heap_memory / jvm.heap_memory_max
```

グラフエディターの **Advanced...** オプションから **Add Query** を選択します。クエリにはアルファベット順に文字が割り当てられ、最初のメトリクスは `a` 、2 番目のメトリクスは `b` のように表示されます。

次に、`Formula` ボックスに計算式 (この例では `a / b`) を入力します。

{{< img src="dashboards/querying/arithmetic_3.png" alt="計算式 3"  style="width:75%;" >}}

計算式のみをグラフで表示するには、メトリクス `a` と `b` の横のチェックマークをクリックします。

**注**: 数式に文字は割り当てられません。数式間では演算できません。

### タイトルの作成

タイトルを入力しなくても、選択内容に基づいてタイトルが自動的に生成されますが、グラフの内容を表すタイトルをご自身で作成することをお勧めします。

### 保存

作業内容を保存してエディターを終了するには **Done** をクリックします。いつでもエディターに戻ってグラフを変更できます。変更を加えた一方で、その内容を保存しない場合は、**Cancel** をクリックします。

## その他のオプション

### イベントオーバーレイ

グラフエディターの **Event Overlays** セクションを使用すると、イベントの相関性を表示できます。検索フィールドにテキストまたは構造化された検索クエリを入力します。検索の詳細については、Datadog [イベントクエリ言語][10]をご参照ください。

## その他の参考資料

{{< partial name="whats-next/whats-next.html" >}}

[1]: /ja/dashboards/graphing_json
[2]: /ja/dashboards/widgets
[3]: https://app.datadoghq.com/metric/explorer
[4]: https://app.datadoghq.com/notebook/list
[5]: https://app.datadoghq.com/metric/summary
[6]: /ja/tagging
[7]: /ja/metrics/introduction
[8]: /ja/dashboards/functions/rollup
[9]: /ja/dashboards/functions/#apply-functions-optional
[10]: /ja/events/#event-query-language
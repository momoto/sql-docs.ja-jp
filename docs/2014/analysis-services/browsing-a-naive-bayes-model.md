---
title: Naive Bayes モデルの参照 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b8bb26a72903644b5985d69efc8adb362fe412
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088478"
---
# <a name="browsing-a-naive-bayes-model"></a>Naive Bayes モデルの参照
  使用して、単純ベイズ モデルを開くときに**参照**、4 つの異なるウィンドウの対話型ビューアーでモデルが表示されます。 ビューアーを使用して、相関関係を調査し、モデルと基になるデータに関する情報を取得します。  
  
-   [依存関係ネットワーク](#bkmk_DepNet)  
  
-   [属性のプロファイル](#bkmk_AttProf)  
  
-   [属性の特性](#bkmk_AttChar)  
  
-   [属性の識別](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a> モデルを調査します。  
 ビューアーの目的は、[!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes モデルで検出された入力属性と出力属性 (入力と従属変数) の相互作用を調査することです。  
  
 単純ベイズ ビューアーを使用した実験する場合は、使用、[分類ウィザード&#40;Excel 用データ マイニング アドインで&#41;](classify-wizard-data-mining-add-ins-for-excel.md)データ マイニング リボンで、ウィザードをクリックして、**詳細**オプション、および変更単純ベイズ アルゴリズムを使用するアルゴリズム  
  
 これらの例については、ソース データをサンプル ブックで使用され、列をグループ化**Yearly Income**、5 つの収入グループにから**Very Low**に**非常に高い**します。 その後、Naïve Bayes モデルを使って、各収入カテゴリと相関関係を持つ要因を分析しました。  
  
###  <a name="bkmk_DepNet"></a> 依存関係ネットワーク  
 最初のウィンドウを使用しますが、**依存関係ネットワーク**します。 どの入力が選択した結果と密接に関連しているかがひとめでわかります。  
  
 ![Naive Bayes ビューアーに依存関係ネットワーク](media/dm13-nb.gif "Naive Bayes ビューアーに依存関係ネットワーク")  
  
##### <a name="explore-the-dependency-network"></a>依存関係ネットワークの調査  
  
1.  まず、目標の結果をクリックして**Yearly Income**、これは、グラフ内のノードとして表されます。  
  
     目標の変数を囲む強調表示されたノードは、この結果と統計的に相関関係のあるノードです。 関係の特性を理解するには、ビューアーの下部にある凡例を使用します。  
  
2.  ビューアーの左側にあるスライダーをクリックして下へドラッグします。  
  
     このコントロールは、依存関係の強さに基づいて、独立変数をフィルター処理します。 スライダーをドラッグして下げると、関係が最も強いリンクだけがグラフに表示されます。  
  
3.  グラフをフィルター処理した後、ボタンをクリックします。**グラフ ビューのコピー**します。 Excel でワークシートを選択し、Ctrl キーを押しながら V キーを押します。  
  
     これで、選択したビューが、フィルターと強調表示も含めて、コピーされます。  
  
 [ページのトップへ](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a> 属性のプロファイル  
 **属性のプロファイル**ウィンドウには他の方法は、すべての変数は、個々 の結果に関連するかが表示されます。  
  
##### <a name="explore-the-profiles"></a>プロファイルの調査  
  
1.  結果を簡単に比較できるように、いくつかの値を非表示にするには、列見出しを別の列にドラッグします。  
  
     ![Naive Bayes ビューアーにプロファイル属性](media/dm13-nb-attprof.gif "Naive Bayes ビューアーにプロファイル属性")  
  
2.  値の分布を表示するセルをクリックして、**マイニング凡例**します。  
  
     異なる結果に関連付けられた属性は異なる表示になるため、地域別の収入の分布など、興味のある相関関係をすばやく見つけることができます。  
  
3.  このビューを基になるデータを取得するには、次のようにクリックします。 **Excel にコピー**します。 個々の属性と結果との相関関係を示す新しいテーブルがワークシートに生成されます。 この Excel テーブルでは、簡単に列の非表示やフィルター処理ができます。  
  
 [ページのトップへ](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a> 属性の特性  
 **属性の特性**ビューは、特定の結果の変数と、関連する要素の詳細な調査の役立ちます。  
  
 ![Naive Bayes ビューアーに特性を属性](media/dm13-nb-viewer.gif "Naive Bayes ビューアーに特性を属性")  
  
##### <a name="explore-the-attribute-characteristics"></a>属性の特性の調査  
  
1.  クリックして**値**から項目を選択し、**値**します。  
  
     目標の結果を選択すると、グラフが更新されて、その結果との関連性が最も強い要素が重要度順に表示されます。  
  
     使用してモデルを作成する場合、[分析の主要な影響元&#40;Excel 用テーブル分析ツール&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)オプション、1 つ以上の予測可能な属性を持つモデルを作成することができます。 ただし、データ マイニング アドインのその他のウィザードはすべて、予測可能な属性が 1 つに制限されています。  
  
2.  クリックして**Excel にコピー**選択した対象となる結果に関連するすべての属性のスコアを一覧表示、新しいワークシートに、テーブルを作成します。  
  
 [ページのトップへ](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a> 属性の識別  
 **属性の識別**ビューでは、2、2 つの結果またはその他のすべての結果との比較結果が 1 つ。  
  
 ![Naive Bayes ビューアーでの識別属性](media/dm13-nb-attdisc.gif "Naive Bayes ビューアーでの識別属性")  
  
##### <a name="explore-attribute-discrimination"></a>属性の識別の調査  
  
1.  コントロールを使用**値 1**と**値 2**結果を比較するを選択します。  
  
     たとえば、このモデルでいくつか興味深い属性にあった、低収入グループので、最初のドロップダウン リストで、最下位の収入グループを選択し、選択**他のすべての状態**2 番目のドロップダウン リスト。  
  
     属性は、重要度順に並べ替えられます (重要度はトレーニング データに基づいて計算)。 したがって、職業が最も密接に収入との相関関係がある要因です (少なくともこの対象グループの場合)。  
  
     正確な数値を表示するには、色分けされたバーとビューをクリックします。、**マイニング凡例**します。  
  
2.  低収入は、ヨーロッパ地域とも相関関係があります。  
  
     Naïve Bayes モデルではドリルダウンはサポートされていません。ただし、この結果グループに関連付けられたケースを調査する場合は、クエリを使用できます。 この種類のモデルに対するクエリについては、次を参照してください。 [Naive Bayes モデルのクエリ例](data-mining/naive-bayes-model-query-examples.md)します。  
  
 [ページのトップへ](#BKMK_Tabs)  
  
## <a name="see-also"></a>参照  
 [Excel におけるモデルの参照&#40;SQL Server データ マイニング アドイン&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  

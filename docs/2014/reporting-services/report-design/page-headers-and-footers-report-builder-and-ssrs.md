---
title: ページ ヘッダーとページ フッター (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.pagefooter.fill.f1
- "10125"
- "10121"
- "10120"
- "10122"
- "10123"
- sql12.rtp.rptdesigner.pageheader.border.f1
- sql12.rtp.rptdesigner.pageheader.general.f1
- sql12.rtp.rptdesigner.pagefooter.border.f1
- sql12.rtp.rptdesigner.pageheader.fill.f1
- sql12.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b746f27653f5e8d1c24a584ac19c8fbac05a57c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105530"
---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>ページ ヘッダーとページ フッター (レポート ビルダーおよび SSRS)
  レポートには、各ページの上部と下部にヘッダーとフッターを含めることができます。 ヘッダーとフッターには、静的テキスト、画像、線、四角形、罫線、背景色、背景画像、式などを含めることができます。 式には、データセットが 1 つしかないレポートでのデータセット フィールド参照と、スコープとしてデータセットを指定する集計関数呼び出しが含まれます。  
  
> [!NOTE]  
>  表示拡張機能の種類によって、ページの処理方法が異なります。 レポートの改ページおよび表示拡張機能の詳細については、「[Reporting Services の改ページ (レポート ビルダーおよび SSRS)](pagination-in-reporting-services-report-builder-and-ssrs.md)」を参照してください。  
  
 既定では、レポートにはページ フッターは含まれますが、ページ ヘッダーは含まれません。 追加または削除する方法の詳細については、「[ページ ヘッダーまたはページ フッターの追加および削除 (レポート ビルダーおよび SSRS)](add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)」を参照してください。  
  
 ヘッダーおよびフッターには、通常、ページ番号、レポート タイトル、およびその他のレポート プロパティが含まれます。 レポート ヘッダーまたはフッターにこれらの項目を追加する方法の詳細については、「[ページ番号またはその他のレポート プロパティの表示 (レポート ビルダーおよび SSRS)](display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)」を参照してください。  
  
 ページ ヘッダーまたはページ フッターを作成すると、各レポート ページに表示されます。 最初のページと最後のページでページ ヘッダーとページ フッターを非表示にする方法の詳細については、「[最初のページまたは最後のページでページ ヘッダーまたはページ フッターを非表示にする (レポート ビルダーおよび SSRS)](hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>レポートのヘッダーとフッター  
 ページ ヘッダーとページ フッターは、レポート ヘッダーとレポート フッターとは異なります。 レポートには、レポート ヘッダーやレポート フッターの特別な領域がありません。 レポート ヘッダーは、レポート デザイン画面でレポート本文の一番上に配置されるレポート アイテムで構成されます。 これらはレポートの最初のコンテンツとして 1 回だけ表示されます。 レポート フッターは、レポート本文の一番下に配置されるレポート アイテムで構成されます。 これらはレポートの最後のコンテンツとして 1 回だけ表示されます。  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>ページ ヘッダーまたはページ フッターへの変数データの表示  
 ページ ヘッダーおよびページ フッターには静的なコンテンツを含めることもできますが、一般的にはページ番号やページのコンテンツに関する情報などの動的なコンテンツを表示します。 ページごとに異なる変数データを表示するには、式を使用する必要があります。  
  
 レポートで定義されているデータセットが 1 つだけの場合は、 `[FieldName]` のような単純な式をページ ヘッダーまたはページ フッターに追加できます。 レポート データ ペインのデータセット フィールド コレクションまたは組み込みフィールド コレクションからページ ヘッダーまたはページ フッターにフィールドをドラッグします。 適切な式が含まれたテキスト ボックスが自動的に追加されます。  
  
 ページの値の合計やその他の集計を計算するには、ReportItems またはデータセット名を指定する集計式を使用できます。 ReportItems コレクションは、レポートが表示された後の各ページにあるテキスト ボックスのコレクションです。 データセット名がレポート定義に存在する必要があります。 次の表に、各集計式タイプでサポートされているアイテムを示します。  
  
|式でサポート|ReportItems の集計|データセットの集計 (スコープがデータセット名であること)|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|レポート本文のテキスト ボックス|はい|いいえ|  
|&PageNumber|はい|いいえ|  
|&TotalPages|はい|いいえ|  
|集計関数|可能。 例を次に示します。<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|可能。 例を次に示します。<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|ページ上のアイテムのフィールド コレクション|間接的。 例を次に示します。<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|可能。 例を次に示します。<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|データバインド画像|間接的。 例を次に示します。 `=ReportItems!TXT_Photo.Value`|可能。 例を次に示します。<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 このトピックの以下のセクションでは、ヘッダーおよびフッターで一般的に使用される変数データを取得するための、すぐに使用できる式を示します。 また、Excel 表示拡張機能でヘッダーおよびフッターが処理される方法についても説明します。 式の詳細については、「[式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>ヘッダーまたはフッターへの計算された合計ページ数の追加  
 レポートの種類によっては、各レポートのヘッダーまたはフッターに計算値 (たとえば、ページに数値が含まれている場合はページごとの合計) を含めると便利です。 フィールドを直接参照することはできないので、ヘッダーまたはフッターに配置する式は、次の例のように、データ フィールドではなく、レポート アイテム (たとえばテキスト ボックス) の名前を参照する必要があります。  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 データ行の繰り返しを含むテーブルまたは一覧内にテキスト ボックスがある場合、実行時にヘッダーまたはフッターに表示される値は、現在のページのテーブルまたは一覧のすべての `TextBox1` インスタンス データのすべての値の合計になります。  
  
 ページ合計を計算する場合、異なる表示拡張機能を使用してレポートを表示すると、合計に相違が生じる可能性があります。 ページ割り当てされた出力は、表示拡張機能の種類によって、異なった方法で計算されます。 HTML で表示したページと同じページを PDF で表示した場合、PDF ページ上のデータ量が異なると、表示される合計も異なる可能性があります。 詳しくは、「[レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)」をご覧ください。  
  
### <a name="for-reports-with-multiple-datasets"></a>複数のデータ ソースがあるレポートの場合  
 複数のデータセットがあるレポートの場合は、ヘッダーまたはフッターにフィールドやデータバインド画像を追加することはできません。 ただし、ヘッダーまたはフッターで使用するフィールドやデータバインド画像を間接的に参照する式を記述することはできます。  
  
 ヘッダーまたはフッターに変数データを配置するには  
  
-   ヘッダーまたはフッターにテキスト ボックスを追加します。  
  
-   テキスト ボックスに、表示する変数データを生成する式を記述します。  
  
-   その式に、ページ上のレポート アイテムへの参照を含めます (たとえば、特定のフィールドのデータが格納されているテキスト ボックスを参照できます)。 データセット内のフィールドへの直接参照を含めることはできません。 たとえば、式 `[LastName]`は使用できません。 `TXT_LastName`テキスト ボックスの最初のインスタンスの内容を表示するには、次の式を使用します。  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 ページ ヘッダーまたはページ フッターのフィールドには集計関数を使用できません。 集計関数はレポート本文のレポート アイテムにのみ使用できます。 ページ ヘッダーとページ フッターの一般的な式については、「[式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)」を参照してください。  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>ヘッダーまたはフッターへのデータバインド画像の追加  
 ヘッダーまたはフッターで、データベースに格納された画像データを使用できます。 ただし、画像レポート アイテムからデータベース フィールドを直接参照することはできません。 代わりに、レポートの本文にテキスト ボックスを追加し、そのテキスト ボックスを画像が格納されているデータ フィールドに設定します (値は base64 でエンコードされている必要があります)。 base64 でエンコードされた画像が表示されないように、レポートの本文でテキスト ボックスを非表示にできます。 次に、ページ ヘッダーまたはページ フッターの画像レポート アイテムから、非表示のテキスト ボックスの値を参照します。  
  
 たとえば、製品情報のページから成るレポートがあるとします。 各ページのヘッダーには、製品の写真を表示します。 保存されている画像をレポート ヘッダーに出力するには、データベースから画像を取得する `TXT_Photo` という非表示のテキスト ボックスをレポートの本文に定義し、次の式を使用してそのボックスに値を渡します。  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 ヘッダーで、 `TXT_Photo` テキスト ボックスを使用する画像レポート アイテムを追加し、デコードして画像を表示します。  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>ヘッダーおよびフッターを使用したテキストの配置  
 ヘッダーおよびフッターを使用して、ページ上にテキストを配置できます。 たとえば、顧客に郵送するレポートを作成しているとします。 顧客の住所をヘッダーまたはフッターを使用して配置することで、レポートを折りたたんだ時に、その住所が封筒の窓から見えるようにすることができます。  
  
 テキスト ボックスを使用してヘッダーまたはフッターのみに値を設定する場合は、レポートの本文でそのテキスト ボックスを非表示にすることができます。 レポートの本文にテキスト ボックスを配置すると、ヘッダーやフッターに表示する値が、レポートの最初と最後のどちらのページに表示されるかに影響する可能性があります。 たとえば、レポートが 1 ページに収まらないテーブル、マトリックス、一覧がある場合、非表示のテキスト ボックスの値は最後のページに表示されます。 これを最初のページに表示する必要がある場合は、非表示のテキスト ボックスをレポート本文の先頭に配置します。  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>特定のレンダラー用のページ ヘッダーおよびページ フッターを使用したレポートのデザイン  
 レポートが処理されると、データとレイアウトの情報は結合されます。 レポートを表示すると、結合された情報がレンダラーに渡され、各レポート ページに収まるレポート データの量が決まります。  
  
 ブラウザーを使用してレポート サーバーでレポートを表示する場合は、表示されるレポート ページの内容を HTML レンダラーがコントロールします。 表示に使用する形式とは異なる形式でレポートを配信する場合や、特定の形式でレポートを印刷する場合は、最終的なレポート形式に使用するレンダラーに合わせてレポート レイアウトを最適化することをお勧めします。 レポートの改ページの詳細については、「[Reporting Services の改ページ (レポート ビルダーおよび SSRS)](pagination-in-reporting-services-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>Excel でのページ ヘッダーおよびページ フッターの使用  
 Excel の表示拡張機能を対象とするレポートにページ ヘッダーおよびページ フッターを定義する場合は、次のガイドラインに従うことで、最も良い結果を得ることができます。  
  
-   ページ フッターは、ページ番号を表示するために使用します。  
  
-   ページ ヘッダーは、画像、タイトル、またはその他のテキストを表示するために使用します。 ヘッダーには、ページ番号を配置しないようにします。  
  
 Excel では、ページ フッターのレイアウトに制限があります。 ページ フッターに複雑なレポート アイテムを含むレポートを定義した場合、そのレポートを Excel で表示すると、ページ フッターの処理は期待どおりには行われません。  
  
 Excel の表示拡張機能は、ページ ヘッダー内の画像、および単純または複雑なレポート アイテムの絶対位置に対応しています。 よりリッチなページ ヘッダー レイアウトをサポートする副作用として、ヘッダーでのページ番号の計算に制限が生じます。 Excel の表示拡張機能では、既定の設定で、ページ番号がワークシートの数に基づいて計算されます。 レポートの定義の仕方によっては、ページ番号に誤りが生じる可能性があります。 たとえば、印刷すると 4 ページになる単一の大きなワークシートとして表示されるレポートがあるとします。 ヘッダーにページ番号情報を含めると、印刷された各ページのヘッダーには、"Page 1 of 1" と表示されます。  
  
 より正確なページ数は、印刷されたページの寸法に相関する論理ページに基づいて計算されます。 Excel のページ フッターでは、論理ページ番号が自動的に使用されます。 ページ ヘッダーに論理ページ数を配置するには、単純なヘッダーを使用するようにデバイス情報設定を構成する必要があります。 単純なヘッダーを使用する場合は、ヘッダー領域で複雑なレポート レイアウトを処理する機能を削除してください。  
  
 詳細については、「 [Microsoft Excel へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)で操作できます。  
  
## <a name="see-also"></a>関連項目  
 [レポートへの画像の埋め込み (レポート ビルダーおよび SSRS)](embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [四角形と線 (レポート ビルダーおよび SSRS)](rectangles-and-lines-report-builder-and-ssrs.md)  
  
  

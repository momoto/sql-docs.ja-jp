---
title: レポートへのゲージの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 92b068b4bfa7f8b61b5be0904bc47cf080afc861
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106838"
---
# <a name="add-a-gauge-to-a-report-report-builder-and-ssrs"></a>レポートへのゲージの追加 (レポート ビルダーおよび SSRS)
  データをビジュアル形式でまとめるにはゲージ データ領域を使用します。 ゲージ データ領域をデザイン画面に追加すると、ゲージのデータ ペインにレポート データセット フィールドをドラッグできるようになります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-gauge-to-your-report"></a>レポートにゲージを追加するには  
  
1.  レポートを作成するか、既存のレポートを開きます。  
  
2.  [挿入] タブの [ゲージ] をダブルクリックします。 **[ゲージの種類の選択]** ダイアログ ボックスが開きます。  
  
3.  追加するゲージの種類を選択します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  グラフと異なり、ゲージの種類は線形と放射状だけです。 **[ゲージの種類の選択]** ダイアログ ボックスには、この 2 種類のゲージがテンプレートとして表示されます。 そのため、ゲージをレポートに追加した後にゲージの種類を変更することはできません。 ゲージの種類を変更するには、一度ゲージを削除してから再度追加する必要があります。  
  
     レポートにデータ ソースとデータセットがない場合は、 **[データ ソースのプロパティ]** ダイアログ ボックスが表示され、手順に従ってそれらの両方を作成できます。 詳細については、「[データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](../report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)します。  
  
     レポートにデータ ソースがありデータセットがない場合は、 **[データセットのプロパティ]** ダイアログ ボックスが表示され、手順に従ってデータセットを作成できます。 詳細については、「 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](../report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)」を参照してください。  
  
4.  ゲージをクリックしてデータ ペインを表示します。 既定では、1 つの値に対応する単一のポインターが存在します。 必要に応じて、ポインターを追加することもできます。  
  
5.  1 つのフィールドをデータセットからデータ フィールドのドロップ ゾーンに追加します。 追加できるフィールドは 1 つだけです。 複数のフィールドを表示する場合は、各フィールドに 1 つずつポインターを追加する必要があります。  
  
     ゲージ スケールを右クリックし、 **[スケールのプロパティ]** を選択します。 スケールの **[最小]** および **[最大]** の値を入力します。 詳細については、「[ゲージへの最小値または最大値の設定 &#40;レポート ビルダーおよび SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](nested-data-regions-report-builder-and-ssrs.md)   
 [ゲージ (レポート ビルダーおよび SSRS)](gauges-report-builder-and-ssrs.md)  
  
  

---
title: クエリ エディターでのコードの色分け | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], color coding
- color coding [Query Editor]
ms.assetid: 802882dc-c997-4e3f-8a01-994bb43169ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e939270edd53189f9d8ba77411b8916e94a5ba8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064168"
---
# <a name="color-coding-in-query-editors"></a>クエリ エディターでのコードの色分け
  コード エディターで入力されたテキストにはカテゴリが割り当てられ、それぞれのカテゴリが色分けされます。 色分けによってコード内のテキストをすばやく見つけることができます。 たとえば、濃い緑を使用してコメントが目立つようにします。 次の表では、最も一般的な色を示します。 **[ツール]** の **[オプション]** メニューを使用して、色とカテゴリの完全な一覧を表示して、独自の配色を構成できます。 既定の色を変更する方法の詳細については、「 [フォントの色、サイズ、およびスタイルを変更する方法](change-font-color-size-and-style.md)」を参照してください。  
  
## <a name="default-code-colors"></a>コードの既定の色分け  
  
|色|カテゴリ|  
|-----------|--------------|  
|[赤]|SQL 文字列|  
|緑|解説|  
|黒 (背景は銀色)|SQLCMD コマンド|  
|赤紫|システム関数|  
|[緑]|システム テーブル、ビュー、またはテーブル値関数。 sys および INFORMATION_SCHEMA のすべてのシステム スキーマ。|  
|[青]|Keyword|  
|青緑|行番号またはテンプレート パラメーター|  
|茶色|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャ (stored procedure)|  
|灰色|演算子|  
  
## <a name="status-bar"></a>ステータス バー  
 オブジェクト エクスプローラーで、登録済みサーバーまたは [!INCLUDE[ssDE](../../includes/ssde-md.md)] サーバーが [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターのステータス バーに別の色で表示されるように構成することができます。 そうすることで、多くのウィンドウを同時に開いているときに、各エディター ウィンドウがどのサーバーに接続しているかを識別しやすくなります。 ステータス バーの色の設定の詳細については、「[ステータス バー &#40;データベース エンジン クエリ エディター&#41;](status-bar-database-engine-query-editor.md)」を参照してください。  
  
 エディターの種類によっては、ステータス バーが表示されない場合や、複数の色がサポートされていない場合があります。  
  
  

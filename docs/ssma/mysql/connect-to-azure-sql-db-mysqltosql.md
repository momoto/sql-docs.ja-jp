---
title: Azure SQL DB (MySQLToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 12da1aa42f468b92e1833410e635183aabf3a384
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103242"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Azure SQL DB への接続 (MySQLToSQL)
SQL Azure ダイアログ ボックスに、Connect を使用して、移行する SQL Azure データベースに接続します。  
  
このダイアログ ボックスにアクセスする、**ファイル**メニューの  **SQL Azure への接続**します。 以前接続した場合、コマンドは**SQL Azure に再接続します。**  
  
## <a name="options"></a>および  
**[サーバー名]**  
  
選択するか、SQL Azure に接続するためのサーバー名を入力します。  
  
**[データベース]**  
  
選択、入力または**参照**データベース名。  
  
> [!IMPORTANT]  
> SSMA for MySQL は、SQL Azure で master データベースへの接続をサポートしていません。  
  
**ユーザー名**  
  
SSMA が SQL Azure データベースへの接続に使用するユーザー名を入力します。  
  
**Password**  
  
ユーザー名に対応するパスワードを入力します。  
  
**Encrypt**  
  
SSMA では、SQL Azure に暗号化された接続をお勧めします。  
  
## <a name="create-azure-database"></a>Azure のデータベースを作成します。  
SQL Azure アカウントには、データベースがない場合、は、最初のデータベースを作成できます。  
  
非常に最初に新しいデータベースを作成するには、次の手順に従います  
  
1.  SQL Azure ダイアログ ボックスに、Connect に表示される参照ボタンをクリックします  
  
2.  データベースがない場合は、次の 2 つのメニュー項目が表示されます。  
  
    1.  **(データベースが見つかりません)** は無効であるすべての時間が淡色表示になりますが  
  
    2.  **新しいデータベースの作成**SQL Azure アカウントにデータベースがない場合にのみ有効になっています。 このメニュー項目をクリックするとは、Azure データベースの作成 ダイアログ ボックスはデータベース名とサイズで存在します。  
  
3.  データベースの作成時に、次の 2 つのパラメーターは入力として指定します。  
  
    1.  **データベース名:** データベース名を入力します。  
  
    2.  **データベースのサイズ:** SQL Azure アカウントに作成する必要があるデータベースのサイズを選択します。  
  

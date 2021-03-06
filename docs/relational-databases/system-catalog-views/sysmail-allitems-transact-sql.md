---
title: sysmail_allitems (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_allitems_TSQL
- sysmail_allitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_allitems database mail view
ms.assetid: 21fb8432-7677-4435-902f-64a58bba4cbb
author: stevestein
ms.author: sstein
ms.openlocfilehash: be5c74e58e5c107a804903ab09de38b931f676e1
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745452"
---
# <a name="sysmail_allitems-transact-sql"></a>sysmail_allitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  データベース メールで処理されたメッセージごとに 1 行のデータを格納します。 このビューは、すべてのメッセージの状態を確認するときに使用できます。  
  
 失敗した状態のメッセージだけを表示するには、 [ &#40;sysmail_faileditems&#41;transact-sql](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)を使用します。 未送信のメッセージだけを表示するには、 [sysmail_unsentitems &#40;&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)を使用します。 送信されたメッセージだけを表示するには、 [ &#40;sysmail_sentitems&#41;transact-sql](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|メール キュー内のメール アイテムの識別子。|  
|**profile_id**|**int**|メッセージの送信に使用されるプロファイルの識別子。|  
|**recipients**|**varchar(max)**|メッセージ受信者の電子メール アドレス。|  
|**copy_recipients**|**varchar(max)**|CC としてメッセージのコピーを受け取る受信者の電子メール アドレス。|  
|**blind_copy_recipients**|**varchar(max)**|BCC としてメッセージのコピーを受け取る受信者の電子メール アドレス。この受信者の名前は、メッセージ ヘッダーには表示されません。|  
|**subject**|**nvarchar(510)**|メッセージの件名。|  
|**body**|**varchar(max)**|メッセージの本文。|  
|**body_format**|**varchar(20)**|メッセージの本文の書式。 可能な値は TEXT と HTML です。|  
|**importance**|**varchar(6)**|メッセージの**重要度**パラメーター。|  
|**sensitivity**|**varchar(12)**|メッセージの**感度**パラメーター。|  
|**file_attachments**|**varchar(max)**|電子メール メッセージに添付されたファイル名の、セミコロン区切りの一覧。|  
|**attachment_encoding**|**varchar(20)**|添付ファイルの種類。|  
|**query**|**varchar(max)**|メール プログラムによって実行されたクエリ。|  
|**execute_query_database**|**sysname**|メール プログラムによってクエリが実行されたデータベース コンテキスト。|  
|**attach_query_result_as_file**|**bit**|値が 0 の場合、クエリの結果が電子メール メッセージ本文内に取り込まれ、本文内容の後に追加されていることを示します。 値が 1 の場合、結果が添付ファイルとして返されたことを示します。|  
|**query_result_header**|**bit**|値が 1 の場合、クエリの結果に列のヘッダーが含まれていることを示します。 値が 0 の場合、クエリの結果に列のヘッダーが含まれていないことを示します。|  
|**query_result_width**|**int**|メッセージの**query_result_width**パラメーター。|  
|**query_result_separator**|**char(1)**|クエリの出力で列の区切りに使用された文字。|  
|**exclude_query_output**|**bit**|メッセージの**exclude_query_output**パラメーター。 詳細については、「 [sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)」を参照してください。|  
|**append_query_error**|**bit**|メッセージの**append_query_error**パラメーター。 0 は、クエリにエラーがあった場合、データベース メールで電子メール メッセージが送信されないことを示します。|  
|**send_request_date**|**datetime**|メッセージがメール キューに挿入された日時。|  
|**send_request_user**|**sysname**|メッセージを送信したユーザー。 これはメッセージの [差出人] フィールドに表示されるユーザーではなく、データベース メール プロシージャのユーザー コンテキストです。|  
|**sent_account_id**|**int**|メッセージの送信に使用されたデータベース メール アカウントの識別子。|  
|**sent_status**|**varchar(8)**|メールの状態。 有効な値は次のとおりです。<br /><br /> **送信**済み-メールが送信されました。<br /><br /> **未送信**-データベースメールはまだメッセージの送信を試みています。<br /><br /> データベースメール**再試行**しています。メッセージを送信できませんでしたが、もう一度送信しようとしています。<br /><br /> **失敗しました**-データベースメールはメッセージを送信できませんでした。|  
|**sent_date**|**datetime**|メッセージが送信された日時。|  
|**last_mod_date**|**datetime**|行が最後に変更された日時。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。|  
  
## <a name="remarks"></a>コメント  
 データベースメールによって処理されるすべてのメッセージの状態を確認するには、 **sysmail_allitems**ビューを使用します。 データベース メールのトラブルシューティングを行うとき、このビューでは送信済みとそれ以外のメッセージの属性を比較できるので、問題の性質を特定するのに役立ちます。  
  
 このビューによって公開されるシステムテーブルにはすべてのメッセージが含まれているため、 **msdb**データベースのサイズが大きくなる可能性があります。 古いメッセージをビューから定期的に削除して、テーブルのサイズを縮小するようにしてください。 詳細については、「[データベースメールメッセージとイベントログをアーカイブするための SQL Server エージェントジョブの作成](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールおよび**databasemailuserrole**データベースロールに付与されます。 **Sysadmin**固定サーバーロールのメンバーによって実行されると、このビューにはすべてのメッセージが表示されます。 他のすべてのユーザーには、送信したメッセージのみが表示されます。  
  
  

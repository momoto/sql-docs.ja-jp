---
title: パーセント文字 (ワイルドカード - 一致する文字列) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
author: rothja
ms.author: jroth
ms.openlocfilehash: af956b153aadc660de4a0b440bc07467888e136b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121858"
---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>パーセント文字 (ワイルドカード - 一致する文字列) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  0 個以上の文字で構成される文字列に一致します。 このワイルドカード文字は、プレフィックスとしてもサフィックスとしても使用できます。  
  
## <a name="examples"></a>使用例  
 次の例では、`Person` の `AdventureWorks2012` テーブルに登録されている人のうち、`Dan` で始まるすべての名前を返します。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91; &#93; (ワイルドカード - 一致する文字列)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91;^&#93; (ワイルドカード - 一致しない文字列)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (ワイルドカード - 一致する 1 文字)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  

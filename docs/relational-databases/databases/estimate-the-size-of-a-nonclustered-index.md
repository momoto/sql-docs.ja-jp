---
title: 非クラスター化インデックスのサイズの算出 | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: c183b0e4-ef4c-4bfc-8575-5ac219c25b0a
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f63cb12399efd7417f9b00695d54b1356f681fb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934463"
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>非クラスター化インデックスのサイズの算出

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  非クラスター化インデックスを格納するために必要な領域を算出するには、次の手順に従います。  
  
1.  手順 2. および 3. で使用する変数を計算します。  
  
2.  非クラスター化インデックスのリーフ レベルのインデックス情報の格納に使用する領域を計算します。  
  
3.  非クラスター化インデックスの非リーフ レベルのインデックス情報の格納に使用する領域を計算します。  
  
4.  計算した値を合計します。  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>手順 1. 手順 2. および 3. で使用する変数を計算する  
 上位レベルのインデックスの格納に必要な領域を算出するために使用する変数は、次の手順で算出することができます。  
  
1.  次のように、テーブル内の行数を指定します。  
  
     ***Num_Rows***  = テーブル内の行数  
  
2.  次のように、インデックス キーの固定長列と可変長列の数を指定し、それらの列の格納に必要な領域を計算します。  
  
     インデックスのキー列には、固定長列と可変長列を含めることができます。 内部レベルのインデックス行サイズを見積もるには、これらの各列グループによってインデックス行内で占有される領域を計算します。 列のサイズは、データ型と長さの指定によって異なります。  
  
     ***Num_Key_Cols***  = キー列 (固定長および可変長) の総数  
  
     ***Fixed_Key_Size***  = すべての固定長キー列の合計バイト サイズ  
  
     ***Num_Variable_Key_Cols***  = 可変長キー列の数  
  
     ***Max_Var_Key_Size***  = すべての可変長キー列の最大バイト サイズ  
  
3.  インデックスが一意ではない場合に必要なデータ行ロケーターの領域を、次のように計算します。  
  
     非クラスター化インデックスが一意ではない場合、データ行ロケーターと非クラスター化インデックス キーを組み合わせて、各行に一意のキー値が生成されます。  
  
     非クラスター化インデックスがヒープ上にある場合は、データ行ロケーターはヒープ RID になります。 このサイズは 8 バイトです。  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 8  
  
     非クラスター化インデックスがクラスター化インデックス上にある場合は、データ行ロケーターはクラスター化キーになります。 非クラスター化インデックス キーと組み合わせる必要がある列は、非クラスター化インデックスのキー列のセットに含まれていないクラスター化キーの列です。  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 非クラスター化インデックスのキー列のセットに含まれていないクラスター化キー列数 (クラスター化インデックスが一意でない場合は + 1)  
  
     ***Fixed_Key_Size***  = ***Fixed_Key_Size*** + 非クラスター化インデックスのキー列のセットに含まれていない固定長クラスター化キー列の合計バイト サイズ  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 非クラスター化インデックスのキー列のセットに含まれていない可変長クラスター化キー列数 (クラスター化インデックスが一意でない場合は + 1)  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 非クラスター化インデックスのキー列のセットに含まれていない可変長クラスター化キー列の最大バイト サイズ (クラスター化インデックスが一意でない場合は + 4)  
  
4.  NULL ビットマップと呼ばれる行の一部が、列に NULL 値を許容するかどうかを管理するために予約されている場合があります。 このサイズは次のように計算します。  
  
     手順 1.3. で説明している必要なクラスター化キー列を含め、インデックス キーに NULL 値を許容する列が存在する場合には、インデックス行の一部が NULL ビットマップ用に予約されます。  
  
     ***Index_Null_Bitmap***  = 2 + ((インデックス行の列数 + 7) / 8)  
  
     上記の式の計算結果は、整数部分だけを使用します。 小数部分は無視してください。  
  
     NULL 値を許容するキー列が存在しない場合は、 ***Index_Null_Bitmap*** を 0 に設定します。  
  
5.  可変長データ サイズを計算します。  
  
     必要なクラスター化インデックスのキー列を含め、インデックス キーに可変長列が存在する場合は、インデックス行内に可変長列を格納するのに使用する領域を次の式で計算します。  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     ***Max_Var_Key_Size*** に追加されたバイトは、それぞれの可変長列を追跡するためのものです。この式は、すべての可変長列がいっぱいになることを前提としています。 可変長列の格納領域の使用率が少ないことが予想される場合、その使用率に基づいて ***Max_Var_Key_Size*** の値を調整し、テーブルの全体サイズをより正確に見積もることができます。  
  
     可変長列が存在しない場合は、 ***Variable_Key_Size*** に 0 を設定します。  
  
6.  次の式でインデックス行のサイズを計算します。  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (インデックス行の行ヘッダー オーバーヘッド) + 6 (子ページ ID のポインター)  
  
7.  次の式で、1 ページあたりのインデックス行数を計算します (1 ページあたりの空きバイト数は 8,096 です)。  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     インデックス行は複数のページにまたがらないため、計算結果の端数は切り捨ててください。 上の式の 2 という値は、ページのスロット配列内にある行の入力用です。  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>手順 2. リーフ レベルのインデックス情報の格納に使用する領域を計算する  
 インデックスのリーフ レベルを格納するために必要な領域は、次の手順で算出することができます。 この手順を完了するには、手順 1. で控えた値が必要になります。  
  
1.  次のように、リーフ レベルの固定長列と可変長列の数を指定し、それらの列の格納に必要な領域を計算します。  
  
    > [!NOTE]  
    >  インデックス キー列の他に非キー列を含めることにより、非クラスター化インデックスを拡張できます。 このように追加された列は、非クラスター化インデックスのリーフ レベルにしか格納されません。 詳細については、「 [付加列インデックスの作成](../../relational-databases/indexes/create-indexes-with-included-columns.md)」を参照してください。  
  
    > [!NOTE]  
    >  定義済みのテーブルの合計サイズが 8,060 バイトを超える **varchar**、 **nvarchar**、 **varbinary**、または **sql_variant** 列の連結が可能です。 この場合も、 **varchar**、 **varbinary**、または **sql_variant** 列の場合は 8,000 バイトの制限内に、 **nvarchar** 列の場合は 4,000 バイトの制限内に、各列のサイズを収める必要があります。 ただし、これらの列を連結したサイズは、テーブルの制限である 8,060 バイトを超過してもかまいません。 これは、既に付加列を含んでいる非クラスター化インデックスのリーフ行にも当てはまります。  
  
     非クラスター化インデックスに付加列が含まれていない場合は、手順 1.3. での変更を含め、手順 1. の値を使用します。  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols***  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size***  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols***  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size***  
  
     非クラスター化インデックスに付加列が含まれている場合は、手順 1.3. での変更を含め、手順 1. の値に適切な値を加えます。 列のサイズは、データ型と長さの指定によって異なります。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols*** + 付加列の数  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size*** + 固定長付加列の合計バイト サイズ  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols*** + 可変長付加列の数  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size*** + 可変長付加列の最大バイト サイズ  
  
2.  データ行ロケーターに必要な領域を次のように計算します。  
  
     非クラスター化インデックスが一意でない場合は、既に手順 1.3. でデータ行ロケーターのオーバーヘッドが考慮されているので、他の変更は必要ありません。 次の手順に進みます。  
  
     非クラスター化インデックスが一意の場合は、リーフ レベルのすべての行のデータ行ロケーターに必要な領域を計算します。  
  
     非クラスター化インデックスがヒープ上にある場合は、データ行ロケーターはヒープ RID (8 バイト) になります。  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 1  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 1  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 8  
  
     非クラスター化インデックスがクラスター化インデックス上にある場合は、データ行ロケーターはクラスター化キーになります。 非クラスター化インデックス キーと組み合わせる必要がある列は、非クラスター化インデックスのキー列のセットに含まれていないクラスター化キーの列です。  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 非クラスター化インデックスのキー列のセットに含まれていないクラスター化キー列数 (クラスター化インデックスが一意でない場合は + 1)  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Leaf_Size*** + 非クラスター化インデックスのキー列のセットに含まれていない固定長クラスター化キー列数  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 非クラスター化インデックスのキー列のセットに含まれていない可変長クラスター化キー列数 (クラスター化インデックスが一意でない場合は + 1)  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 非クラスター化インデックスのキー列のセットに含まれていない可変長クラスター化キー列のバイト サイズ (クラスター化インデックスが一意でない場合は + 4)  
  
3.  次のように、NULL ビットマップのサイズを計算します。  
  
     ***Leaf_Null_Bitmap***  = 2 + ((***Num_Leaf_Cols*** + 7) / 8)  
  
     上記の式の計算結果は、整数部分だけを使用します。 小数部分は無視してください。  
  
4.  可変長データ サイズを計算します。  
  
     上記の手順 2.2. で説明した必要なクラスター化キー列を含め、インデックス キーに可変長列が存在する場合は、インデックス行内の可変長列を格納するのに使用する領域を次の式で計算します。  
  
     ***Variable_Leaf_Size***  = 2 + (***Num_Variable_Leaf_Cols*** x 2) + ***Max_Var_Leaf_Size***  
  
     ***Max_Var_Key_Size*** に追加されたバイトは、それぞれの可変長列を追跡するためのものです。この式は、すべての可変長列がいっぱいになることを前提としています。 可変長列の格納領域の使用率が少ないことが予想される場合、その使用率に基づいて ***Max_Var_Leaf_Size*** の値を調整し、テーブルの全体サイズをより正確に見積もることができます。  
  
     可変長列が存在しない場合は、 ***Variable_Leaf_Size*** に 0 を設定します。  
  
5.  次の式でインデックス行のサイズを計算します。  
  
     ***Leaf_Row_Size***  = ***Fixed_Leaf_Size*** + ***Variable_Leaf_Size*** + ***Leaf_Null_Bitmap*** + 1 (インデックス行の行ヘッダー オーバーヘッド)  
  
6.  次の式で、1 ページあたりのインデックス行数を計算します (1 ページあたりの空きバイト数は 8,096 です)。  
  
     ***Leaf_Rows_Per_Page***  = 8096 / (***Leaf_Row_Size*** + 2)  
  
     インデックス行は複数のページにまたがらないため、計算結果の端数は切り捨ててください。 上の式の 2 という値は、ページのスロット配列内にある行の入力用です。  
  
7.  指定した [FILL FACTOR](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) に基づいて、1 ページあたりの予約済みの空き行数を次の式で計算します。  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Leaf_Row_Size*** + 2)  
  
     計算で使用する FILL FACTOR は、パーセンテージではなく整数値です。 行は複数のページにまたがらないので、計算結果の端数は切り捨ててください。 FILL FACTOR の値が大きくなるほど、各ページに格納できるデータの量が多くなり、ページ数は少なくなります。 上の式の 2 という値は、ページのスロット配列内にある行の入力用です。  
  
8.  次の式で、すべての行を格納するために必要なページ数を計算します。  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Leaf_Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     算出したページ数の端数は切り上げてください。  
  
9. 次の式で、インデックスのサイズを計算します (1 ページあたりの総バイト数は 8,192 です)。  
  
     ***Leaf_Space_Used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>手順 3. 非リーフ レベルのインデックス情報の格納に使用する領域を計算する  
 インデックスの中間レベルおよびルート レベルを格納するために必要な領域を算出するには、次の手順に従います。 この手順を完了するには、手順 2. および 3. で控えた値が必要になります。  
  
1.  次の式で、インデックス内の非レベル数を計算します。  
  
     ***Non-leaf Levels***  = 1 + log( Index_Rows_Per_Page) (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     この値を最も近い整数に切り上げます。 この値には、非クラスター化インデックスのリーフ レベルは含まれません。  
  
2.  次の式で、インデックス内の非リーフ ページ数を計算します。  
  
     ***Num_Index_Pages***  = ∑Level (***Num_Leaf_Pages/Index_Rows_Per_Page***^Level) ここで 1 <= Level <= ***Levels*** になります。  
  
     それぞれの値を最も近い整数に切り上げます。 簡単な例として、 ***Num_Leaf_Pages*** = 1000、 ***Index_Rows_Per_Page*** = 25 のインデックスを例に取ります。 リーフ レベルより上位の最初のインデックス レベルでは、1000 行のインデックス行が格納されます。リーフ ページあたり 1 行のインデックス行で、1 ページあたり 25 行のインデックス行を納めることができます。 つまり、1,000 行のインデックス行を格納するために 40 ページが必要になります。 次のレベルのインデックスでは、40 行のインデックス行を格納する必要があります。 つまり、2 ページが必要になります。 最上位レベルのインデックスでは、2 行のインデックス行を格納する必要があります。 つまり、1 ページが必要になります。 その結果、非リーフ インデックス ページは 43 ページとなります。 このような数値を前の式で使用すると、次のような結果になります。  
  
     ***Non-leaf_Levels***  = 1 + log(25) (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43 が、例で説明したページ数です。  
  
3.  次の式で、インデックスのサイズを計算します (1 ページあたりの総バイト数は 8,192 です)。  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-4-total-the-calculated-values"></a>手順 4. 計算した値を合計します。  
 次の式で、上記の 2 つの手順から取得した値を合計します。  
  
 非クラスター化インデックス サイズ (バイト) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 この計算では、次のことは考慮されていません。  
  
-   [パーティション分割]  
  
     パーティション分割による領域のオーバーヘッドはわずかですが、計算が複雑になります。 これは、計算に含めるほど重要なことではありません。  
  
-   アロケーション ページ  
  
     ヒープに割り当てられたページの追跡に使用する IAM ページが少なくとも 1 ページありますが、使用される IAM ページ数を正確に計算できるアルゴリズムはなく、領域のオーバーヘッドはわずかです。  
  
-   ラージ オブジェクト (LOB) の値  
  
     LOB データ型の **varchar(max)** 、 **varbinary(max)** 、 **nvarchar(max)** 、 **text**、 **ntext**、 **xml**、および **image** の値を格納するのに使用する領域を正確に特定するためのアルゴリズムは複雑です。 LOB データ型の値で使用される領域の計算は、想定される LOB 値の平均サイズを合計し、 ***Num_Rows***で乗算し、非クラスター化インデックスの合計サイズに加算するだけで十分です。  
  
-   圧縮  
  
     圧縮されたインデックスのサイズを事前に計算することはできません。  
  
-   スパース列  
  
     スパース列の領域要件については、「 [スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [クラスター化インデックスと非クラスター化インデックスの概念](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [非クラスター化インデックスの作成](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [クラスター化インデックスの作成](../../relational-databases/indexes/create-clustered-indexes.md)   
 [テーブル サイズの見積もり](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [クラスター化インデックスのサイズの見積もり](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [ヒープ サイズの見積もり](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [データベース サイズの見積もり](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  

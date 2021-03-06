---
title: サーバーの容量を読み込み、Analytics Platform System の計画 |Microsoft Docs
description: この容量の計画ワークシート、読み込みサーバー Analytics Platform System Parallel Data Warehouse にデータを読み込むための要件を決定できます。"
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0bb15fdd3b20c538237b3e012df4217ad5568bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960663"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>Analytics Platform System のサーバー容量の計画ワークシートの読み込み
この容量の計画ワークシートを使用して、SQL Server PDW にデータを読み込むための読み込みサーバーの要件を決定するのに役立ちます。 購入または既存のサーバーに負荷をプロビジョニングするための計画を作成するのにには、これを使用します。  
  
## <a name="worksheet-notes"></a>ワークシートのノート
  
1.  このワークシートを使用してデータを読み込むことがサーバーに適用されます、 **dwloader**コマンドライン読み込みツールです。  
  
2.  Integration Services またはサード パーティの読み込みツールを使用してデータを読み込むため、読み込みプロセスの違いに応じて、要件は異なります。  
  
3.  いずれかまたは非圧縮データ ファイルの読み込みに、要件のほとんどが適用されます。要件の違いは、太字で記載されています。  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![クリップボード](media/clipboard-icon.png "クリップボード")の容量計画ワークシート  
  
このワークシートを印刷し、独自の要件を使用してこれを入力します。  
  
|コンポーネント|要件|この列は、独自の要件に入力します。|推奨事項|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|ストレージ|一定の期間で読み込みサーバーに格納する予定の最大バイト数。|![鉛筆アイコン](media/pencil-icon.png "鉛筆のアイコン")|記憶域の要件を確認するのには、一定の期間で読み込みサーバーに格納するデータの量を算出します。  容量の要件はファイルの読み込みだけです。オペレーティング システムとファイルの読み込みは、別のディスク アレイになければなりません。<br /><br />以下に例を示します。3 回ディスクから 100 GB のデータを読み込む予定の場合、各日が週の最後までのデータのファイルを削除データ ファイルを保存する最小 2.1 TB が必要です。 保守的なとについて概要をお勧めの差異と成長に対応する記憶域を 30% 増加します。  この例では、記憶域スペースの 2.73 TB が良いでしょう。|  
|読み込みレート|PDW へ読み込むデータの 1 時間あたりの最大バイト数。|![鉛筆アイコン](media/pencil-icon.png "鉛筆のアイコン")|これは、推定値です。 この要件を計算するときに、ファイルが既に読み込みサーバーであると、その他の読み込みの条件ができるだけ良いことを想定しています。<br /><br />例:PDW にデータ圧縮されていない dwloader は常に送信するためのデータ圧縮率を考慮する必要がありません。 データ型変換と変換先テーブルのサイズを考慮する必要はありません。|  
|ネットワーク|ネットワーク接続の種類。|![鉛筆アイコン](media/pencil-icon.png "鉛筆のアイコン")|読み込みレート要件に合わせて最適なネットワーク接続の種類を決定します。<br /><br />以下に例を示します。InfiniBand または 10 ギガ ビット イーサネットは最適な読み込みレートを提供します。 1 ギガ ビット イーサネットは、読み込みレート 360 GB に 1 時間以内に制限されます。|  
|I/O|読み取りと書き込みに対して 1 時間あたりのバイト数。|![鉛筆アイコン](media/pencil-icon.png "鉛筆のアイコン")|データを読み込む dwloader する必要がありますすべてのデータ ディスクから読み取られた PDW に送信する前にします。<br /><br />読み込みの各サーバーでは、アプライアンスは、読み込みのすべてのソースからデータを受信できるよりも速くデータを読み込むことができません。 コストを削減するには、I/O の読み取り、アプライアンスのロード容量を超えないようにを読み込むための容量を計画します。<br /><br />例:<br />PDW では、受信し、1 時間あたりの 1.8 TB の最大レートで 1 ラック アプライアンスにデータを読み込みます。 2 つ以上のラックにアプライアンスの場合、最大負荷率は 3.6 TB を 1 時間ごとです。<br /><br />同時に複数のサーバーの読み込みから読み込む場合は、1 つのサーバーがすべての読み込みを実行する場合よりも小さいを各読み込み server の I/O 要件になります。<br /><br />以下に例を示します。読み込みの 1 つのサーバーには、1-ラック マウント型アプライアンスに対して 1 時間あたり最大 1.8 TB を読み込むことができます。 2 つのサーバーの読み込みでしたそれぞれ同時に読み込む 900 GB 1 時間あたり 1 ラック アプライアンスです。 高いレベルの同時実行には、効率性と最大のスループットを減らすことができます。<br /><br />I/O の容量をすべて読み込み、サーバー上で実行される I/O のアカウントします。 読み込みサーバーだけでなく、ETL サーバーから受信したデータ ファイルなどのデータを読み込むには、その他の I/O トラフィックがある場合は、I/O 要件が増加します。<br /><br />圧縮されたデータは、I/O の要件は、データ圧縮率に依存します。 dwloader のでは、圧縮されたデータを読み取り、PDW に送信する前に圧縮を解除します。 高いほど、圧縮率、小さいデータ読み込みサーバーがディスクから読み取る必要があります。<br /><br />以下に例を示します。必要な負荷速度、1 時間あたりの 1.8 TB は、2:1 の圧縮で読み込みサーバーのデータが格納される場合は、読み込みのサーバーを 1.8 TB ではなくディスクから 1 時間あたり 900 GB を読み取る場合にのみ必要があります。 3:1 の圧縮比率は、読み込みサーバーは、ディスクから 1 時間あたり 600 GB を読み取る必要があるを意味します。|  
|CPU|ソケットの数。|![鉛筆アイコン](media/pencil-icon.png "鉛筆のアイコン")|非圧縮データを読み込み、dwloader は CPU 負荷の高いアプリケーションではありません。  最小要件として、最近製造された 2 つのソケット サーバーを使用してをお勧めします。<br /><br />圧縮されたデータを読み込み、PDW に送信する前に、データの圧縮を解除するための十分な CPU パワーが必要です。 dwloader のでは、一度に 10 個のアクティブなスレッドを実行できます。 同時に 10 個の圧縮されたファイルを読み込む場合は、サーバーが、少なくとも 10 コアの CPU または 2 つの 6 コア Cpu をお勧めします。|  
|RAM|GB の中にファイルをキャッシュする Windows は、メモリに読み込みます。|![鉛筆アイコン](media/pencil-icon.png "鉛筆のアイコン")|dwloader は、読み込みサーバーのほとんどの RAM を使用します。 パフォーマンスは、Windows は、メモリを使用して、ディスクからの読み取り後に読み込みファイルをキャッシュします。<br /><br />RAM の要件を確認するのには、Windows Server のインストールと、サード パーティ製アプリケーションの要件を参照してください。 32 GB の最小値は、他のソースからの要件を持たない場合お勧めします。<br /><br />圧縮されたデータは、高速の RAM は、圧縮解除を速くので便利です。|  
  
## <a name="see-also"></a>関連項目  
[読み込みサーバーの取得と構成](acquire-and-configure-loading-server.md)  
[dwloader のコマンドラインのローダー](dwloader.md)  
  

---
title: Database Experimentation Assistant の概要
description: Database Experimentation Assistant の概要
ms.custom: seo-lt-2019
ms.date: 11/16/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 79caf961208287e1482efe780d2d0e335bbdd16d
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165555"
---
# <a name="overview-of-database-experimentation-assistant"></a>Database Experimentation Assistant の概要

Database Experimentation Assistant (DEA) は SQL Server アップグレードの実験ソリューションです。 DEA は、特定のワークロードの対象となるバージョンの SQL Server を評価するのに役立ちます。 以前の SQL Server バージョン (2005 以降) から新しいバージョンの SQL Server にアップグレードするお客様は、ツールで提供される分析メトリックを使用できます。

分析メトリックは次のとおりです。

- 互換性エラーがあるクエリ
- 低下したクエリとクエリプラン
- その他のワークロード比較データ

比較データを使用すると、信頼性が高く、アップグレードが正常に実行される可能性があります。

## <a name="get-dea"></a>DEA を取得する

DEA をインストールするには、最新バージョンのツールを[ダウンロード](https://www.microsoft.com/download/details.aspx?id=54090)します。 次に、 **DatabaseExperimentationAssistant**ファイルを実行します。

## <a name="solution-architecture-for-comparing-workloads"></a>ワークロードを比較するためのソリューションアーキテクチャ

次の図は、ワークロード比較のソリューションアーキテクチャを示しています。 ワークロードの比較では、SQL Server 2008 から SQL Server 2016 へのアップグレード時に DEA と分散再生を使用します。

![ワークロード比較ソリューションのアーキテクチャ](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>前提条件を排除する

DEA を実行するための前提条件を次に示します。

- 最小ハードウェア要件: 3.5 GB の RAM を搭載したシングルコアコンピューター。
- 理想的なハードウェア要件: 8 コア CPU (3.5 GB 以上の RAM)。 8個を超えるコアを持つプロセッサは、DEA ランタイムを向上させません。
- 、B、およびレポート分析データベースを格納するには、さらに33% のパフォーマンストレースサイズが必要です。

## <a name="configure-dea"></a>DEA の構成

前提条件となる環境アーキテクチャでは、DEA を*分散再生コントローラーと同じコンピューターに*インストールすることをお勧めします。 これにより、コンピューター間の呼び出しが回避され、構成が簡単になります。

### <a name="required-configuration-for-workload-comparison-using-dea"></a>DEA を使用したワークロード比較のために必要な構成

DEA は、Windows 認証を使用してデータベースサーバーに接続します。 DEA を実行しているユーザーが Windows 認証を使用してデータベースサーバー (ソース、ターゲット、および分析) に接続できることを確認してください。

**構成要件のキャプチャ**

トレースをキャプチャするには、次のものが必要です。

- DEA を実行するユーザーは、Windows 認証を使用してソースデータベースサーバーに接続できます。
- DEA を実行しているユーザーには、ソースデータベースサーバーに対する sysadmin 権限があります。
- ソースデータベースサーバーを実行しているサービスアカウントには、トレースフォルダーパスへの書き込みアクセス権があります。

詳細については、「[トレースキャプチャに関してよく寄せられる質問](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)」を参照してください。

**再生構成の要件**

トレースを再生するには、次のものが必要です。

- DEA を実行するユーザーは、Windows 認証を使用してターゲットデータベースサーバーに接続できます。
- DEA を実行しているユーザーには、ターゲットデータベースサーバーに対する sysadmin 権限があります。
- ターゲットデータベースサーバーを実行しているサービスアカウントには、トレースフォルダーパスへの書き込みアクセス権があります。
- 分散再生クライアントを実行しているサービスアカウントは、Windows 認証を使用してターゲットデータベースサーバーに接続できます。
- 分散再生コントローラーで受信した要求に対して TCP ポートが開かれています。 DEA は、COM インターフェイスを使用して、分散再生コントローラーと通信します。

詳細については、「[トレースの再生に関してよく寄せられる質問](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)」を参照してください。

**分析の構成要件**

分析を実行するには、次のものが必要です。

- DEA を実行するユーザーは、Windows 認証を使用して分析データベースサーバーに接続できます。
- DEA を実行しているユーザーには、ソースデータベースサーバーに対する sysadmin 権限があります。

詳細については、「[分析レポートに関してよく寄せられる質問](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)」を参照してください。

## <a name="set-up-telemetry"></a>テレメトリの設定

DEA にはインターネット対応の機能があり、製品のエクスペリエンスを向上させるために利用できるテレメトリ情報を Microsoft に送信できます。 収集された情報は、ローカル監査のためにコンピューターにも保存されるので、収集された情報を常に確認できます。 すべての DEA ログファイルは% temp%\\DEA フォルダーに保存されます。

テレメトリデータは、次の4種類のイベントで収集できます。

- **Traceevent**: アプリケーションの使用状況イベント (たとえば、"トリガーされたキャプチャ停止")。
- **例外**: アプリケーションの使用中に例外がスローされました。
- **DiagnosticEvent**: 問題が発生した場合の診断を支援するイベントログ (Microsoft に送信さ*れません*)。
- **FeedbackEvent**: アプリケーションを通じて送信されるユーザーフィードバック。

テレメトリデータの収集と送信は任意です。 収集されるイベントと収集されるイベントを指定するには、次の手順を実行します。

1. DEA がインストールされている場所に移動します (たとえば、C:\\Program Files (x86)\\Microsoft Corporation\\Database Experimentation Assistant)。
2. 必要に応じて、**構成ファイル (** アプリケーションの場合) と**DEACMD .exe** (CLI の場合) を開いて変更し、シナリオに対処します。
    - イベントの種類の収集を停止するには、*イベント*の値 ( **traceevent**など) を**false**に設定します。 イベントの収集を再開するには、値を**true**に設定します。
    - イベントのローカルコピーの保存を停止するには、 **TraceLoggerEnabled**の値を**false**に設定します。 ローカルコピーの保存を再び開始するには、値を**true**に設定します。
    - Microsoft へのイベントの送信を停止するには、 **AppInsightsLoggerEnabled**の値を**false**に設定します。 再度 Microsoft へのイベント送信を開始するには、値を**true**に設定します。

DEA は、Microsoft の[プライバシー](https://aka.ms/dea-privacy)に関する声明によって管理されます。

## <a name="see-also"></a>参照

2つの環境のワークロードの比較に関連するプロセスについて説明する、[ワークロード比較プロセスの概要](database-experimentation-assistant-get-started.md)。

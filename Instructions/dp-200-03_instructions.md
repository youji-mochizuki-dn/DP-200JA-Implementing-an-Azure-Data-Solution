﻿# DP 200 - データ プラットフォーム ソリューションの実装
# ラボ 3 - Azure Databricks を使用したチーム ベースのデータ サイエンスの有効化 

**予想時間**: 75 分

**前提条件**: この課題のケース スタディは既に確認していることを前提としています。モジュール 1 のコンテンツとラボは次のとおりです：データ エンジニア向け Azure も完了済みであること

**ラボ ファイル**: この課題のファイルは、_Allfiles\Labfiles\Starter\DP-200.3_ フォルダーにあります。

## ラボの概要

この課題の終わりまでに、学生は  Azure Databricks を使用してデータ サイエンスを支援できる理由を説明できるようになる。受講者は、Azure Databricks インスタンスをプロビジョニングし、Data Lake Store Gen II ストアから簡単なデータ準備タスクを実行するために使用されるワークスペースを作成します。最後に、学生は Azure Databricks を使用して変換を実行するチュートリアルを実行します。

## 課題の目的
  
この課題を完了すると、次のことができるようになります。

1. Azure Databricks について説明する
2. Azure Databricks の使用
3. Azure Databricks を使用してデータを読み取る
4. Azure Databricks を使用して変換を実行する

## シナリオ
  
情報サービス (IS) 部署に対応して、このテクノロジを使用する利点を列挙して、予測分析プラットフォームを構築するプロセスを開始します。この部署にはデータ サイエンティストが加わり、新しいチームメンバーが予測分析環境を利用できるようにしたいと考えている。

あなたは、Azure Databricks 環境を立ち上げてプロビジョニングし、既存の Data Lake Storage Gen 2 アカウントからデータを取り込むことで、サービス上で単純なデータ準備ルーチンを実行して、この環境が機能することをテストします。データ エンジニアとして、データ サイエンティストがデータ準備演習を実行するのを支援する必要がある場合があることが示されている。そのためには、基本的な変換を実行するのに役立つノートブックを通しで確認することをお勧めします。

このラボを完了すると:

1. Azure Databricks について説明した
2. Azure Databricks を使用しました
3. Azure Databricks を使用してデータを読み取る
4. Azure Databricks を使用して変換を実行した

> **重要**: このラボを進めるにつれ、プロビジョニングまたは構成タスクで発生した問題を書き留め、_\Labfiles\DP-200-Issues-Docx_にあるドキュメントの表に記録してください。課題番号を文書化し、テクノロジを記述し、問題とその解決を説明します。このドキュメントは、後のモジュールで参照できるように保存します。

## 演習 1: Azure Databricks について説明する 

>**重要**: **最初にエクササイズ 2** を実行し、エクササイズ 2 で Databricks クラスターの作成を開始した後 (プロビジョニングに10 分間かかるため) にエクササイズ 1 に戻ります。

推定時間: 15 分

個別エクササイズ
  
このエクササイズの主なタスクは、以下の通りです。

1. このコースでこれまでに学習した内容から、Azure Databricks が満たすデジタル環境の変革要件と、Azure Databricks の候補データ ソースを特定します。

2. インストラクターは、検出結果についてグループと話し合います。

### タスク 1: デジタル変革と候補データ ソースを定義します。

1. 課題の仮想マシンから **Microsoft Word** を起動し、**Allfiles\Labfiles\Starter\DP-200.3** フォルダーからファイル **DP-200-Lab03-Ex01.docx** を開きます。

2. この課題のケース スタディとシナリオの概説に従って、**10 分間** でデジタル環境の変革要件と候補データ ソースを文書化します。

### タスク 2: 検出結果についてインストラクターと話し合う

1. インストラクターは、検出結果について話し合うためにグループを中断させます。

> **結果**: このエクササイズを完了すると、Azure Databricks が満たすデジタル環境の変革要件と候補データ ソースを識別する Microsoft Word ドキュメントが作成されます。

## 演習 2: Azure Databricks を使用
  
推定時間: 20 分

個別エクササイズ
  
このエクササイズの主なタスクは次のとおりです。

1. リソース グループに Azure Databricks Premium 層インスタンスを作成する。

2. Azure Databricks を開く

3. Databricks ワークスペースを起動し、Spark クラスターを作成する

### タスク 1: Azure Databricks インスタンスを作成して構成する。

1. スクリーンの左上にある Azure portal で、「**ホーム**」 ハイパーリンクをクリックします 。

2. Azure portal で、「**+ リソースの作成**」 アイコンをクリックします。

3. 新規のスクリーンで、**マーケットプレースの検索** テキスト ボックスに移動し、**databricks** という単語を入力します。表示される一覧で「**Azure Databricks**」 をクリックします。

4. **Azure Databricks** ブレードで **作成** をクリックします。

5. **Azure Databricks のサービス** ブレードから、次の設定を使用してAzure Databricks ワークスペースを作成します。

    - **「ワークスペース名」**：**Warehousexx**、 (**xx** は、お客様のイニシャルです)

    - **Subscription**: このラボで使用するサブスクリプションの名前

    - **リソース グループ**: **awrgstudxx** (**xx** は自分のイニシャル)。

    - **場所**: ラボの場所に最も近い Azure リージョンの名前と、Azure VM をプロビジョニングできる場所。

    - **価格レベル**: **Premium (+ ロールベースのアクセス制御)**。


        ![Azure portal で Azure Databricks を作成します](Linked_Image_Files/M03-E02-T01-img01.png)

6. **Azure Databricks サービス** ブレードで、**作成** をクリックします。

   > **注**: プロビジョニングの所要時間は約 3 分です。Databricks ランタイムは、Apache Spark を基盤として、Azure クラウドにネイティブに対応するように構築されています。Azure Databricks は、インフラストラクチャの複雑性を完全に排除しており、データ インフラストラクチャの設定と構成に関する専門知識も必要ありません。運用ジョブのパフォーマンスに気を掛けるデータ エンジニアに対しては、Azure Databricks は、I/O レイヤーと処理レイヤー (Databricks I/O) でのさまざまな最適化によって、高速で高性能な Spark エンジンを提供します。
   
### タスク 2: Azure Databricks を開く

1. Azure Databricks サービスが作成されたことを確認します。

2. Azure portal で、**リソース グループ** スクリーンに移動します。

3. リソース グループ スクリーンで、****awrgstudxx** リソース グループ (**xx** はお客様のイニシャル) をクリックします。

4. **awrgstudxx** スクリーンで、**awdbwsstudxx** (**xx** お客様のイニシャル) をクリックして、Azure Databricks を開きます。これで、Azure Databricks サービスが開きます。

    ![Azure portal での Azure Databricks サービス](Linked_Image_Files/M03-E02-T02-img01.png)

### タスク 3: Databricks ワークスペースを起動し、Spark クラスターを作成する。

1. Azure portal の **awdbwsstudxx** スクリーンで、**ワークスペースの起動**ボタンをクリックします。

    > **注**: Microsoft Edge の別のタブで、Azure Databricks ワークスペースにサインインします。

2. **Azure Databricks" 画面の左側にある "Clusters" をクリック します。

3. **Clusters** スクリーンの "**+ Create Cluster**"  で、次の設定を使って Databricks クラスターを作成し、「**クラスターの作成**」 をクリックします。

    - **クラスター名**: **awdbclstudxx** (**xx** はお客様のイニシャル)

    - **クラスター モード**: **Standard**

    - **プール**：**None**

    - **Databricks ランタイムのバージョン**: **ランタイム：7.4 (Scala 2.12、Spark 3.0.1)**
    
    - 「**Terminate after 120 minites of inactivity**」 チェック ボックスをオンにします。クラスターが使われていない場合は、クラスターを終了するまでの時間 (分単位) を指定します。

    - **Min Workers**：**1**

    - **Max Workers**：**2**

    - 残りのオプションはすべて現在の設定のままにしておきます。

        ![Azure portal で Azure Databricks クラスターを作成する](Linked_Image_Files/M03-E02-T03-img01.png)

4. **Create Cluster** をクリックし、Microsoft Edge スクリーンを開いたままにします。

> **注**: グラフィカル ユーザー インターフェイスを使用して Spark クラスターの作成が簡略化されるため、Azure Databricks インスタンスの作成には約 10 分かかります。クラスターの作成中は、**状態**が**保留中**になります。クラスターが作成されると、**実行中**に変わります。

> **注**: クラスターの作成中に、**エクササイズ 1に戻って実行します**。

## 演習 3: Azure Databricks を使用してデータを読み取る

推定時間: 30 分

個別エクササイズ

このエクササイズの主なタスクは次のとおりです。

1. Databricks クラスターが作成されたことを確認します。

2. Azure Data Lake Store Gen II アカウント名を収集します

3. Databricks インスタンスを有効にして、Data Lake Gen II Store にアクセスする。

4. Databricks ノートブック を作成し、Data Lake Store に接続する。

5. Azure Databricks でデータを読み取る。

### タスク 1: Databricks クラスターの作成を確認する

1. Microsoft Edge に戻り、「**Clusters**」 で **awdbclstudxx** という名前のクラスター (**xx** はお客様のイニシャル) の 「State」 が 「**Running**」 になっていることを確認します。

### タスク 2: Azure Data Lake Store Gen II アカウント名を取得します

1. **Azure portal** で、 「**リソース グループ**」 、**awrgstudxx** の順にクリックします。

2. 「**awdlsstudxx**」 スクリーンで 「**アクセス キー**」 をクリックし、「**ストレージアカウント名**」 の横にあるコピー アイコンをクリックして、メモ帳に貼り付けます。 

    ![Azure portal での Data Lake Storage アカウント名へのアクセス](Linked_Image_Files/M03-E03-T02-img01.png)

### タスク 3: Databricks インスタンスを有効にして、Data Lake Gen II Store にアクセスする。

1. Azure portal で、「**ホーム**」 ハイパーリンクをクリックし、「**Azure Active Directory**」 アイコンをクリックします。

2. 「**Microsoft - 概要**」 スクリーンで、「**アプリの登録**」 をクリックします。

3. 「**Microsoft - アプリの登録**」 スクリーンで、「**+ 新規登録**」 ボタンをクリックします。

4. アプリケーションの登録画面で、**DLAccess** の **名前** を入力し、**リダイレクトURI（オプション）** セクションで、**ウェブ** が選択され、アプリケーションの値に **http://localhost** が入力されていることを確認します。値を設定した後。

    ![Azure portal でアプリを登録します。](Linked_Image_Files/M03-E03-T03-img01.png)

5. **登録** をクリックします。DLAccess 画面が表示されます。

6. **DLAccess** 登録アプリ画面で、**アプリケーション（クライアント） ID** と **ディレクトリ（テナント ID）** をコピーしてメモ帳 にペーストします。

7. **DLAccess** 登録済みアプリ画面で、 **証明書とシークレット**をクリックして、**+ 新しいクライアント シークレット**をクリックします。

8. 「クライアント シークレットを追加する」 の画面で、 **説明** にシークレットの名前を入力し、キーの **期間** を **1 年間** に指定します。完了したら、「**追加**」 をクリックします。

    ![Azure portal でのクライアント シークレットの追加しています](Linked_Image_Files/M03-E03-T03-img02.png)

    >**重要**: 「**追加**」 をクリックすると、キーは下の図のように表示されます。このキー値をノートパッドにコピーできるのは 1 度だけです

    ![DL アクセス キーの場所](Linked_Image_Files/M03-E03-T03-img03.png)

9. 「**アプリケーション キーの値**」 をコピーしてメモ帳 に貼り付けます。

10. リソース グループにストレージ BLOB データ共同作成者のアクセス許可を割り当てます。Azure portalで、**ホーム** をクリックしてから、**リソースグループ** アイコンをクリックして、リソース グループ **awrgstudxx** をクリックします。ここで **xx** はイニシャルです。

11. 「**awrgstudxx**」 スクリーンで、「**アクセスの制御 (IAM)**」 をクリックします。 

12. 「**ロールの割り当て**」 タブをクリックします。 

13. **「+追加」** をクリックして、**「ロールの割り当てを追加する」** をクリックします

14. 「**ロールの割り当てを追加**」 ブレードの 「ロール」 で、「**ストレージ BLOB データ 共同作成者**」 を選択します。

15. 「**ロールの割り当てを追加**」 ブレードの 「選択」 で、「**DLAccess**」 を選択し、「**保存**」 をクリックします。

16. Azure ポータルで、 「**ホーム**」 ハイパーリンクをクリックし、「**Azure Active Directory**」 に移動します。概要ページで、テナント情報に表示されている自身の「**ロール**」 に注意してください。もしグローバル管理者ではなく「ユーザー」ロールである場合は、管理者以外がアプリケーションを登録できることを確認する必要があります。

17. 「**ユーザー**」 をクリックし、「**ユーザー - すべてのユーザー**」 ブレードの 「**ユーザー設定**」 をクリックし、「**アプリの登録**」 を確認します。規定では、この値は管理者だけが設定できます。「はい」 に設定すると、Azure AD テナント内の任意のユーザーがアプリを登録することができます。 

18. 「**ユーザー - すべてのユーザー**」 画面を閉じます。

19. 「Azure Active Directory」 ブレードで、「**プロパティ**」 をクリックします。

20. **ディレクトリ ID** の横にある 「コピー」 アイコンをクリックし、テナント ID を取得したら、メモ帳 に貼り付けます。

21. メモ帳ドキュメントを、フォルダー **Allfiles\Labfiles\Starter\DP-200.3** に **DatabricksDetails.txt** として保存します。

### タスク 4: Databricks ノートブック を作成し、Data Lake Store に接続する。

1. Microsoft Edge で、「**クラスター - Databricks**」 タブ をクリックします。

    > **注**: クラスター ページが表示されます。

2. Microsoft Edge の左側にある 「Azure Databricks」 ブレードで、「**Workspace**」をクリックします。次に、「**Workspace**」の横にあるドロップダウンをクリックし、「**Create**」 をクリックして 「**Notebook**」 をクリックします。

3. 「**Notebook の作成**」 画面で、「**Name**」の横に 「**My Notebook**」 を入力します。

4. 「**Default Language**」 ドロップダウン リストの横にある 「**Scala**」 を選択します。

5. 以前に作成したクラスターの名前がクラスターに表示されていることを確認し、「**作成**」 をクリックします。

    ![Azure Databricks でのノートブックの作成](Linked_Image_Files/M03-E03-T04-img01.png)

     > **注記**: これにより、「My  Notebook (Scala)」 というタイトルのノートブックが開きます。

6. Notebook のセル **Cmd 1** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Connect to Azure Data Lake Storage Gen2 account

    spark.conf.set("fs.azure.account.auth.type", "OAuth")
    spark.conf.set("fs.azure.account.oauth.provider.type", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")
    spark.conf.set("fs.azure.account.oauth2.client.id.<storage-account-name>.dfs.core.windows.net", "<application-id>")
    spark.conf.set("fs.azure.account.oauth2.client.secret.<storage-account-name>.dfs.core.windows.net", "<authentication-key>")
    spark.conf.set("fs.azure.account.oauth2.client.endpoint.<storage-account-name>.dfs.core.windows.net", "https://login.microsoftonline.com/<tenant-id>/oauth2/token")
    ```

7. このコード ブロックでは、このコード ブロック内の **application-id**、**authentication-id**、**tenant-id**、**file-system-name** および **storage-account-name** のプレースホルダー値を、以前に収集した値で置き換えます。これらの値は メモ帳 に保持されます。

8. ノートブック内の 「**Cmd 1**」 の下のセルで、右側の「**実行**」 アイコンをクリックし、次の図形でハイライトされているように 「**Run Cell**」 をクリックします。 

    ![Azure Databricks でノートブックで cvode を実行する](Linked_Image_Files/M03-E03-T04-img02.png)

    > **注 **「Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx」 というメッセージがセルの下部に表示される。 

### タスク 5: Azure Databricks でデータを読み取る。

1. ノートブックで、**Cmd 1** セルの右上にマウスを移動し、**+** アイコンをクリックします。**Cmd2** という名前の新しいセルが表示される。

    ![Azure Databricks のノートブックでのセルの追加](Linked_Image_Files/M03-E03-T04-img03.png)

2. Notebook のセル **Cmd 2** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    // Azure Data Lake Storage Gen2 ファイルシステムで JSON データを読み取る

    val df = spark.read.json("abfss://<file-system-name>@<storage-account-name>.dfs.core.windows.net/preferences.json")
    ```

3. このコード ブロックでは、**file-system-name** を **logs** という単語で、またこのコード ブロック内の **storage-account-name** プレースホルダー値を以前に収集した値で置き換え、メモ帳 に保持します。

4. ノートブック内の **Cmd 2** の下のセルで、「**実行**」 アイコンをクリックし、「**Run Cell**」 をクリックします。 

    >**注** Spark ジョブが実行されたこと、および「Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx」を示すメッセージが、セルの下部に戻ります。 

5. ノートブックで、**Cmd 2** セルの右上にマウスを移動し、**+** アイコンをクリックします。**Cmd3** という名前の新しいセルが表示される。

6. Notebook のセル **Cmd 3** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Show result of reading the JSON file
  
    df.show()
    ```

    ![Azure Databricks での Notebook の結果の実行](Linked_Image_Files/M03-E03-T04-img04.png)

7. ノートブック内の **Cmd 3** の下のセルで、「**実行**」 アイコンをクリックし、「**Run Cell**」 をクリックします。

    >**注 **Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、「Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx」 と表示されます。 

8. Azure Databricks Notebook を開いたままにします

>**結果** このエクササイズでは、Azure Databricks が Azure Data Lake Store Gen2 のデータにアクセスするためのアクセス許可を設定する上で必要なステップを実行しました。次に、scala を使用して Data Lake Store に接続し、データを読み取り、ユーザーの好みを示すテーブル出力を作成しました。

## 演習 4: Azure Databricksを使用して基本的な変換を実行する

推定時間: 10 分

個別エクササイズ

このエクササイズの主なタスクは次のとおりです。

1. データセットの特定の列を取得する

2. データセットで列の名前の変更を実行する

3. コメントを追加する

4. 時間がある場合: その他の変換

### タスク 1: データセットの特定の列を取得する

1. ノートブックで、**Cmd 3** セルの右上にマウスを移動し、**+** アイコンをクリックします。**Cmd4** という名前の新しいセルが表示される。

2. Notebook のセル **Cmd 4** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    // Azure Data Lake Storage Gen2 ファイル システムの JSON データセットから特定の列を取得する
    
    val specificColumnsDf = df.select("firstname", "lastname", "gender", "location", "page")
    specificColumnsDf.show()
    ```

3. ノートブック内の **Cmd 4** の下のセルで、「**実行**」 アイコンをクリックし、「**セルの実行**」 をクリックします。 

    > **注 **Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、「Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx」 と表示されます。

    ![Azure Databricks のノートブックでのスカラ クエリの実行](Linked_Image_Files/M03-E04-T01-img01.png)

### タスク 2: データセットで列の名前の変更を実行する

1. ノートブックで、**Cmd 4** セルの右上にマウスを移動し、**+** アイコンをクリックします。**Cmd5** という名前の新しいセルが表示される。

2. Notebook のセル **Cmd 5** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //ページ列の名前をbike_preferenceに変更する

    val renamedColumnsDF = specificColumnsDf.withColumnRenamed("page", "bike_preference")
    renamedColumnsDF.show()
    ```

3. ノートブック内の **Cmd 5** の下のセルで、「**実行**」 アイコンをクリックし、「**セルの実行**」 をクリックします。 

    > **注 **Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、「Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx」 と表示されます。

    ![Azure Databricks のノートブックのクエリの列の名前を変更する](Linked_Image_Files/M03-E04-T02-img01.png)

### タスク 3: コメントを追加する

1. ノートブックで、**Cmd 5** セルの右上にマウスを移動し、**+** アイコンをクリックします。**Cmd6** という名前の新しいセルが表示される。

2. Notebook のセル **Cmd 6** で、次のコードをコピーし、セルに貼り付けます。

    ```text
    このコードは、「Data」という名前の Data Lake Storage ファイルシステムに接続し、その Data Lake に保存されている preference.json ファイルのデータを読み取ります。次に、データを取得する為の簡単なクエリが作成され、「ページ」列の名前が「bike_preference」に変更された。
    ```

3. ノートブック内の **Cmd 6** の下のセルで、 **下向きの矢印** アイコンをクリックし、「**Move Up**」 をクリックします。セルがノートブックの上部に表示されるまで繰り返します。

4. Azure Databricks Notebook を開いたままにします

    > **注** この後ラボでは、このデータを別のデータ プラットフォーム テクノロジーにエクスポートする方法を検討します。

> **結果**: この演習を完了したら、ノートブック内にコメントを作成しました。

### タスク 4: 時間に余裕がある場合、又はレビューの後の場合

この課題が早く終わった場合、次のセクションのリンクを参照して、Azure の基本的な変換及び詳細な変換について学べます。

URL にアクセスできない場合、ノートブックのコピーが _Allfiles\Labfiles\Starter\DP-200.3\Post Course Review_フォルダーにあります。

**基本的な変換**

1. ワークスペース内で、左側のコマンド バーを使用して、「**ワークスペース**」 、「**ユーザー**」 を 選択し、 「**ユーザー名**」 (家のアイコンのエントリ) を選択する。

2. ブレードが表示されるので、**名前の横にある下向きのシェブロン** を選択し、「**インポート**」 を選択します。

3. 「Notebooks のインポート」 ダイアログ ボックスで、**下の URL** を選択し、次の URL に貼り付けます。 

```url
    https://github.com/MicrosoftDocs/mslearn-perform-basic-data-transformation-in-azure-databricks/blob/master/DBC/05.1-Basic-ETL.dbc?raw=true
```

4. 「**インポート**」 を選択します。

5. インポート後に **05.1-Basic-ETL** という名前のフォルダーが表示されるはずです。そのフォルダーを選択します。

6. フォルダーには、**scala** または **python** を使用して基本的な変換を学習するために使用できる 1 つ以上のノートブックが含まれます。

ノートブック内の指示に従い、ノートブック全体を完了します。次に残りのノートブックを順番に続行します。

- **01-Course-Overview-and-Setup** (01-コースの概要とセットアップ)  - このノートブックは、Databricks ワークスペースに関するものである。
- **02-ETL-Process-Overview** - (02-ETL プロセスの概要) このノートブックには、クエリ、大きなデータ ファイル、及び結果の視覚化に役立つエクササイズが含まれています。
- **03-Connecting-to-Azure-Blob-Storage** - (03-Azure Blob Storage への接続) このノートブックでは、基本的な集計と結合を実行する。
- **04-Connecting-to-JDBC** - (04-JDBC への接続) このノートブックは、Databricks を使用してさまざまなソースからデータにアクセスするためのステップを示している。
- **05-Applying-Schemas-to-JSON** - (05-スキーマから JSON への適用) このノートブックでは、DataFrames を使用して JSON と階層データをクエリする方法を学習する。
- **06-Corrupt-Record-Handling** - このノートブックには、ADLSを作成し、Databricks DataFramesを使用して、このデータをクエリ及び分析する方法を理解するのに役立つ演習がリストされている。
- **07-Loading-Data-and-Productionalizing** -  ここでは、Databricks を使用して、Azure Data Lake Storage Gen2 のデータストアをクエリ、分析します。
- **Parsing-Nested-Data** -  このノートブックは、オプション サブフォルダーにあり、後で都合の良い時に試してみるためのサンプル プロジェクトが含まれています。

> 「注」 Solutionsサブフォルダー内に対応するNotebooksがある。これらには、1 つまたは複数の課題を完了するよう求める演習用の完了したセルが含まれます。行き詰まった場合、または解決方法を確認したいだけの場合は、これらを参照してください。 

**詳細な変換**

1. ワークスペース内で、左側のコマンド バーを使用して、「**ワークスペース**」 、「**ユーザー**」 を 選択し、 「**ユーザー名**」 (家のアイコンのエントリ) を選択する。

2. ブレードが表示されるので、**名前の横にある下向きのシェブロン** を選択し、「**インポート**」 を選択します。

3. 「Notebooks のインポート」 ダイアログ ボックスで、**下の URL** を選択し、次の URL に貼り付けます。 

```url
    https://github.com/MicrosoftDocs/mslearn-perform-advanced-data-transformation-in-azure-databricks/blob/master/DBC/05.2-Advanced-ETL.dbc?raw=true
```

4. 「**インポート**」 を選択します。

5. インポート後に **05.2-Advanced-ETL** という名前のフォルダーが表示されます。そのフォルダーを選択します。

6. フォルダーには、**scala** または **python** を使用して基本的な変換を学習するために使用できる 1 つ以上のノートブックが含まれます。

ノートブック内の指示に従い、ノートブック全体を完了します。次に残りのノートブックを順番に続行します。

- **01-Course-Overview-and-Setup** (01-コースの概要とセットアップ)  - このノートブックは、Databricks ワークスペースに関するものである。
- **02-Common-Transformations** -  (一般的な変換) このノートブックでは、Spark 組み込み関数を使用して一般的なデータ変換を実行します。
- **03-User-Defined-Functions** (03-ユーザ定義関数) - このノートブックでは、ユーザ定義関数を使用したカスタム変換を実行します。
- **04-Advanced-UDFs** -  (04-高度な UDF) このノートブックでは、高度なユーザー定義関数を使用して複雑なデータ変換を実行します。
- **05-Joins-and-Lookup-Tables** -  (05-結合とルックアップテーブル) このノートブックでは、テーブルに標準結合とブロードキャスト結合を使用する方法を学習します。
- **06-Database-Writes** - このノートブックには、ETLジョブから変換されたデータを保存し、多数のターゲットデータベースにデータを並行して書き込む為の演習が含まれている。
- **07-Table-Management** - ここでは、管理テーブルと非管理テーブルを処理して、保存スペースを最適化する。
- **Custom-Transformations** - このノートブックは、オプションのサブフォルダーにあり、後で自分の時間で探索する為のサンプルプロジェクトが含まれている。

> 「注」 Solutionsサブフォルダー内に対応するNotebooksがある。これらには、1 つまたは複数の課題を完了するよう求める演習用の完了したセルが含まれます。行き詰まった場合、または解決方法を確認したいだけの場合は、これらを参照してください。

---

copyright:
  years: 2014, 2017
lastupdated: "2017-07-17"

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}

# 開始使用 Db2 Warehouse on Cloud（先前為 dashDB for Analytics）
{: #getting_started}

{{site.data.keyword.IBM}} Db2 Warehouse on Cloud 受管理服務是在雲端中為您所佈建的 SQL Database。您就像使用任何資料庫軟體一般的使用 Db2 倉儲，但沒有硬體設置或軟體安裝及維護的額外負荷與費用。
{: shortdesc}

## 介面
{: #interfaces}

您可以透過下列方式來使用倉儲資料庫：
{: shortdesc}

   * 從 Web 主控台
   * REST API
   * 連接本端電腦的應用程式或您最愛的工具
   * 將 Db2 Warehouse on Cloud 用作 Bluemix 應用程式或服務的資料來源

### Web 主控台
{: #web_console}

Web 主控台為您使用資料庫所需的所有項目提供一個圖形介面，包括：負載機能、SQL 編輯器、驅動程式下載等等。
{: shortdesc}

![Web 主控台儀表板頁面的視圖](images/console_v2.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour "External link icon"){:new_window}. -->

您可以透過下列方式來存取 Web 主控台：
   * 從 {{site.data.keyword.Bluemix_notm}} 儀表板 - 您可以從 Db2 Warehouse on Cloud 服務的「服務詳細資料」頁面中開啟 Web 主控台。
   * 直接 URL - 您可以對 Db2 Warehouse on Cloud 服務的 Web 主控台 URL 加上書籤。

### REST API
{: #api}

使用 Db2 Warehouse on Cloud 服務方案，您可以執行檔案管理、載入資料等相關作業，以及透過使用 [Db2 Warehouse on Cloud REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://ibm.biz/dashdb-api "外部鏈結圖示"){:new_window} 來執行 R Script。
{: shortdesc}

### 連接本端電腦的應用程式或您最愛的工具
{: #connect_apps}

請完成下列步驟，配置本端環境以連接至 Db2 倉儲資料庫：
{: shortdesc}

1. 從 Db2 Warehouse on Cloud Web 主控台下載[驅動程式套件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package.html "外部鏈結圖示"){:new_window}。
2. 在您的應用程式或工具執行所在的電腦上，[安裝驅動程式套件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_install.html "外部鏈結圖示"){:new_window}。
3. 為您的 Db2 倉儲資料庫[配置驅動程式檔案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html "外部鏈結圖示"){:new_window}。

### 將 Db2 Warehouse on Cloud 用作 Bluemix 應用程式或服務的資料來源
{: #data_src}

將 {{site.data.keyword.Bluemix_notm}} 上管理的應用程式連接至 Db2 Warehouse on Cloud 資料庫的方式，與將您的本端應用程式連接至 Db2 Warehouse on Cloud 資料庫的方式完全相同。
{: shortdesc}

當您的應用程式使用 {{site.data.keyword.Bluemix_notm}} 平台時，您可以充分運用 `VCAP _SERVICES` 環境變數，以簡化指定資料庫詳細資料及認證的作業。
1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板上，於 Db2 Warehouse on Cloud 服務的「服務詳細資料」頁面的**連線**標籤中，按一下**建立連線**按鈕。
2. 選取要與 Db2 Warehouse on Cloud 資料庫搭配使用作為資料來源的 {{site.data.keyword.Bluemix_notm}} 應用程式，然後按一下**連接**按鈕。
3. 更新應用程式碼，擷取 `VCAP_SERVICES` 環境變數中的資料庫詳細資料及認證：

    **不含 `VCAP_SERVICES` 的範例**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Get these database details from
    $hostname    = "<Host-name>";   # the Connection info page of the
    $port        = 50000;           # web console.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **含有 `VCAP_SERVICES` 的範例**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## 範例
{: #samples}

以下鏈結範例示範如何從不同語言的應用程式連接至 Db2 Warehouse on Cloud 資料庫：
{: shortdesc}

   * [.NET ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html "外部鏈結圖示"){:new_window}
<!-- * [JAVA ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_java.html "External link icon"){:new_window} -->
   * [JDBC ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html "外部鏈結圖示"){:new_window}
<!-- * [Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_nodejs.html "External link icon"){:new_window} -->
   * [PHP ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html "外部鏈結圖示"){:new_window}
<!-- * [Python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_python.html "External link icon"){:new_window} -->
   * [GitHub 上的 Db2 Warehouse on Cloud 範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/dashdb-nodejs-helloworld "外部鏈結圖示"){:new_window}



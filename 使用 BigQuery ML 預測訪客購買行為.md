### 使用 BigQuery ML 預測訪客購買行為

### 總覽
運用 BigQuery 的 BigQuery ML (BigQuery 機器學習) 功能，資料分析師只需編寫少量程式碼，就可以建立、訓練、評估機器學習模型，並將模型用於預測結果。

BigQuery 中已載入 Google Analytics (分析) 樣本電子商務資料集^1，其中包含數百萬筆 Google Analytics (分析) ^2的 Google 商品網路商店記錄。在本研究室中，您將使用這些資料執行查詢，解答企業想瞭解消費者購物習慣時，通常會提出的問題。

https://blog.google/products/marketingplatform/analytics/introducing-google-analytics-sample/

https://shop.merch.google/


### 目標
在本研究室中，您會瞭解如何執行下列工作：

使用 BigQuery 尋找公開資料集
查詢及探索電子商務資料集
建立訓練和評估資料集，供批次預測使用
在 BigQuery ML 中建立分類 (邏輯迴歸) 模型
評估機器學習模型的成效
對訪客購買商品的可能性進行預測及排名

### 設定環境

#### 設定研究室
在每個研究室中，您都能在固定時間內免付費建立新的 Google Cloud 專案，並使用一組資源。

請透過無痕式視窗登入 Qwiklabs。

請記下研究室的存取時間 (例如 1:15:00)，並確保自己能在時間限制內完成作業。
研究室不提供暫停功能。如有需要，您可以重新開始，但原先的進度恕無法保留。

準備就緒後，請按一下「Start lab」。

請記下研究室憑證 (使用者名稱和密碼)，這組資訊將用於登入 Google Cloud 控制台。

按一下「Open Google Console」。

按一下「Use another account」，然後複製這個研究室的憑證，並貼入提示訊息。
如果使用其他憑證，系統會顯示錯誤或向您收取費用。

接受條款，然後略過資源復原頁面。

### 開啟 BigQuery 控制台
1. 在 Google Cloud 控制台中，依序選取「導覽選單」>「BigQuery」。
接著，畫面中會顯示「歡迎使用 Cloud 控制台中的 BigQuery」訊息方塊，當中會列出快速入門指南的連結和使用者介面更新內容。

2. 按一下「完成」。


### 存取課程資料集
開啟 BigQuery 後，在新的瀏覽器分頁中開啟 data-to-insights 專案，就能將這項專案導入 BigQuery 專案窗格。

https://console.cloud.google.com/bigquery?p=data-to-insights&d=ecommerce&t=web_analytics&page=table

data-to-insights 電子商務資料集的欄位定義可於 [通用 Analytics (分析)] BigQuery Export 結構定義頁面查詢。您可以在新分頁中開啟該頁面，方便隨時參考。

https://support.google.com/analytics/answer/3437719?hl=zh-Hant

### 工作 1：探索電子商務資料

情境：資料分析師團隊已將電子商務網站的 Google Analytics (分析) 記錄匯出至 BigQuery 並建立新資料表，內含所有原始電子商務訪客工作階段的資料。您可以試著根據這些資料回答幾個問題。

問題：我們網站的所有訪客當中，購買商品的人占多少百分比？

點選查詢「編輯器」。
在「新查詢」欄位中，加入下列內容：

```
#standardSQL
WITH visitors AS(
SELECT
COUNT(DISTINCT fullVisitorId) AS total_visitors
FROM `data-to-insights.ecommerce.web_analytics`
),

purchasers AS(
SELECT
COUNT(DISTINCT fullVisitorId) AS total_purchasers
FROM `data-to-insights.ecommerce.web_analytics`
WHERE totals.transactions IS NOT NULL
)

SELECT
  total_visitors,
  total_purchasers,
  total_purchasers / total_visitors AS conversion_rate
FROM visitors, purchasers
```

3. 點選「執行」。
結果：2.69%

問題：銷售量前 5 名的產品是哪些？

4. 在查詢「編輯器」中加入下列內容，點選「執行」：

```
SELECT
  p.v2ProductName,
  p.v2ProductCategory,
  SUM(p.productQuantity) AS units_sold,
  ROUND(SUM(p.localProductRevenue/1000000),2) AS revenue
FROM `data-to-insights.ecommerce.web_analytics`,
UNNEST(hits) AS h,
UNNEST(h.product) AS p
GROUP BY 1, 2
ORDER BY revenue DESC
LIMIT 5;
```

結果：

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/ace8e07f-fe00-4705-8af6-683f44f646d1)

問題：有多少訪客在後續造訪網站時購買商品？

5. 執行下列查詢來找出答案：

```
# visitors who bought on a return visit (could have bought on first as well
WITH all_visitor_stats AS (
SELECT
  fullvisitorid, # 741,721 unique visitors
  IF(COUNTIF(totals.transactions > 0 AND totals.newVisits IS NULL) > 0, 1, 0) AS will_buy_on_return_visit
  FROM `data-to-insights.ecommerce.web_analytics`
  GROUP BY fullvisitorid
)

SELECT
  COUNT(DISTINCT fullvisitorid) AS total_visitors,
  will_buy_on_return_visit
FROM all_visitor_stats
GROUP BY will_buy_on_return_visit
```
結果：

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/6c32f18e-ee4d-435b-abc6-8f49c625e279)

您可以看到所有訪客當中，有 (11873 / 729848) = 1.6% 會回訪並在網站上購買商品，當中包括首次造訪時就已購買商品，回訪時又再購買的訪客。

以高單價商品而言，這種行為極為常見，因為消費者通常得做足功課、貨比三家，才能做出決定 (如購買汽車)，而這個網站上的商品 (T 恤、配件等) 也稍微反映出相同傾向。

在線上行銷領域，根據首次造訪時展現的特徵，辨識潛在客戶並向他們行銷，不僅能提高轉換率，還能降低他們流向競爭對手網站的可能性。

### 工作 2：選取特徵並建立訓練資料集


現在，您要在 BigQuery 中建立一個機器學習模型，用以預測新使用者日後是否可能購買商品。辨識出這些高價值使用者，有助於行銷團隊鎖定目標，推出特惠和廣告活動。

Google Analytics (分析) 會對使用者造訪這個電子商務網站的行為，擷取各種維度和度量。請瀏覽 [通用 Analytics (分析)] BigQuery Export 結構定義指南中的完整欄位清單，接著預覽示範資料集找出實用特徵，協助機器學習模型瞭解下列資料的關聯性：訪客首次造訪網站，以及他們是否會回訪並購買商品。

https://support.google.com/analytics/answer/3437719?hl=zh-Hant

https://bigquery.cloud.google.com/table/data-to-insights:ecommerce.web_analytics?tab=preview

您的團隊決定以這兩個欄位做為分類模型的輸入資料，看看能否取得理想結果：

* totals.bounces (訪客是否立即離開網站)
* totals.timeOnSite (訪客在網站上停留的時間)

機器學習的成效取決於輸入的訓練資料是否完備。如果資訊不足，導致模型無法判斷及學習輸入特徵和標籤之間的關聯性 (在本例中，指的是消費者日後是否會購買商品)，您就無法建立準確的模型。雖然使用這兩個欄位訓練模型只是第一步，但您會看到這兩個欄位是否足以產生精確 的模型。

*在查詢「編輯器」中加入下列內容，點選「執行」：

```
SELECT
  * EXCEPT(fullVisitorId)
FROM

  # features
  (SELECT
    fullVisitorId,
    IFNULL(totals.bounces, 0) AS bounces,
    IFNULL(totals.timeOnSite, 0) AS time_on_site
  FROM
    `data-to-insights.ecommerce.web_analytics`
  WHERE
    totals.newVisits = 1)
  JOIN
  (SELECT
    fullvisitorid,
    IF(COUNTIF(totals.transactions > 0 AND totals.newVisits IS NULL) > 0, 1, 0) AS will_buy_on_return_visit
  FROM
      `data-to-insights.ecommerce.web_analytics`
  GROUP BY fullvisitorid)
  USING (fullVisitorId)
ORDER BY time_on_site DESC
LIMIT 10;
```

結果：

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/291e1ba3-9b31-4506-ab46-77ff48ebe2bd)

討論：在使用者首次造訪後，還無法得知 will_buy_on_return_visit。別忘了，您的預測對象是回訪網站並購買商品的那一群使用者。您在預測時不知道未來的情況，因此無法確定新訪客是否會回訪並購買商品。我們希望根據訪客首次造訪期間的資料，瞭解消費者日後購買商品的可能性，這也是建構機器學習模型的價值所在。

問題：以初步資料結果而言，time_on_site 和 bounces 是否為理想指標，有助於預測使用者回訪並購買商品的可能性？

回答：在訓練及評估模型前，通常無法下定論，但目前看來，排名前 10 的 time_on_site 中，只有 1 位消費者回訪並購買商品，準確度並不高。接著看看這個模型的成效。

###工作 3：建立 BigQuery 資料集來儲存模型

接著請建立新的 BigQuery 資料集，這個資料集也會用於儲存機器學習模型。

1.  在左側窗格中，依序點選專案名稱 >「查看動作」(三點) 圖示，選取「建立資料集」。


![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/b2b19a6b-2e0b-499d-bc9e-b65c85fd72cd)

2. 在「建立資料集」對話方塊中：
 
在「資料集 ID」部分，輸入 ecommerce。

其他設定均保留預設值。

5. 點選「建立資料集」。

### 在 BigQuery 中建立第一個機器學習模型。

有兩種模型可供選擇：

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/55aefcf3-c86a-4924-9457-93eba9fc4139)

1. 輸入下列查詢來建立模型，並指定模型選項：

```
CREATE OR REPLACE MODEL `ecommerce.classification_model`
OPTIONS
(
model_type='logistic_reg',
labels = ['will_buy_on_return_visit']
)
AS

#standardSQL
SELECT
  * EXCEPT(fullVisitorId)
FROM

  # features
  (SELECT
    fullVisitorId,
    IFNULL(totals.bounces, 0) AS bounces,
    IFNULL(totals.timeOnSite, 0) AS time_on_site
  FROM
    `data-to-insights.ecommerce.web_analytics`
  WHERE
    totals.newVisits = 1
    AND date BETWEEN '20160801' AND '20170430') # train on first 9 months
  JOIN
  (SELECT
    fullvisitorid,
    IF(COUNTIF(totals.transactions > 0 AND totals.newVisits IS NULL) > 0, 1, 0) AS will_buy_on_return_visit
  FROM
      `data-to-insights.ecommerce.web_analytics`
  GROUP BY fullvisitorid)
  USING (fullVisitorId)
;
```

2. 接著點選「執行」，開始訓練模型。
等模型訓練完成 (5 至 10 分鐘)。

注意：因為需保留部分資料點用於模型評估及測試，您無法在訓練期間將所有可用資料輸入模型。為了達成這個目標，請新增 WHERE 子句條件，在 12 個月的資料集中，只篩選出前 9 個月的工作階段資料來訓練模型。
模型訓練完成後，畫面上會顯示下列訊息：「This statement created a new model named qwiklabs-gcp-xxxxxxxxx:ecommerce.classification_model」。

點選「前往模型」。
查看並確認電子商務資料集中現在是否出現 classification_model。

接下來，您將使用新資料評估模型成效。
















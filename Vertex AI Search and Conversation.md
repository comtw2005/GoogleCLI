Vertex AI Search and Conversation
https://console.cloud.google.com/gen-app-builder/start?hl=zh-TW&project=unified-runner-411615

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/be9aa936-7391-4871-846a-bb6a8430a91c)

選取應用程式類型

搜尋
立即取得優質結果，並輕鬆自訂引擎

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/6359e744-bcee-4a8b-8c83-85dbb3d30c29)

設定

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/774459c3-190d-4d81-8f4e-626fbfcbcf95)

資料

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/36cddeb0-b879-4c49-9a53-ac4b6cfb10a5)
ㄏ
建立新的資料儲存庫

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/ca7ae10a-56c2-4906-a6fa-6c7472887a40)

網站網址

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/66f59eda-7524-4e4f-b9f1-3ffb0ad01a35)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/b760edbb-7d06-40cb-a35b-6da611e89c2e)

資料儲存庫

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/842006bb-360a-4590-8689-4718e173d927)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/b13266fd-93cc-4216-9224-98001d624d9f)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/b1d06c1a-9978-4dd2-afe6-e65b8fc7cf41)



![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/f3c7d968-3612-4a48-bcce-fc81c316c9ca)

```
import com.google.cloud.discoveryengine.v1.SearchRequest;
import com.google.cloud.discoveryengine.v1.SearchResponse;
import com.google.cloud.discoveryengine.v1.SearchServiceClient;
import com.google.cloud.discoveryengine.v1.SearchServiceSettings;
import com.google.cloud.discoveryengine.v1.ServingConfigName;
import java.io.IOException;
import java.time.LocalDateTime;
import java.util.concurrent.ExecutionException;

public class Search {
    public static void main(String[] args) throws IOException, ExecutionException {
        System.out.println("Search Start: " + LocalDateTime.now());
        // TODO(developer): Replace these variables before running the sample.
        // Project ID or project number of the Cloud project you want to use.
        String projectId = "unified-runner-411615";
        // Location of the data store. Options: "global", "us", "eu"
        String location = "global";
        // Collection containing the data store.
        String collectionId = "default_collection";
        // Data store ID.
        String dataStoreId = "test-ctbc-search_1711552364203";
        // Serving configuration. Options: "default_search"
        String servingConfigId = "default_search";
        // Search Query for the data store.
        String searchQuery = "Google";
        search(projectId, location, collectionId, dataStoreId, servingConfigId, searchQuery);
    }

    /** Performs a search on a given datastore. */
    public static void search(
            String projectId,
            String location,
            String collectionId,
            String dataStoreId,
            String servingConfigId,
            String searchQuery)
            throws IOException, ExecutionException {
        // For more information, refer to:
        // https://cloud.google.com/generative-ai-app-builder/docs/locations#specify_a_multi-region_for_your_data_store
        String endpoint = (location.equals("global"))
                ? String.format("discoveryengine.googleapis.com:443", location)
                : String.format("%s-discoveryengine.googleapis.com:443", location);
        SearchServiceSettings settings =
                SearchServiceSettings.newBuilder().setEndpoint(endpoint).build();
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the `searchServiceClient.close()` method on the client to safely
        // clean up any remaining background resources.
        try (SearchServiceClient searchServiceClient = SearchServiceClient.create(settings)) {
            SearchRequest request =
                    SearchRequest.newBuilder()
                            .setServingConfig(
                                    ServingConfigName.formatProjectLocationCollectionDataStoreServingConfigName(
                                            projectId, location, collectionId, dataStoreId, servingConfigId))
                            .setQuery(searchQuery)
                            .setPageSize(10)
                            .build();
            SearchResponse response = searchServiceClient.search(request).getPage().getResponse();
            for (SearchResponse.SearchResult element : response.getResultsList()) {
                System.out.println("Response content: " + element);
            }
        }
    }
}
```



























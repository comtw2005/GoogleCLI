

# Cloud Run

Cloud Run 是 Google Cloud 的全代管式 Serverless 服務

    Cloud Functions

    App Engine

    Cloud Run

    Cloud Functions 快速建置小批量的工作流程或單一 Function-based 的服務 適用於原型設計（Prototyping）

    App Engine 使用 Web 或 API 後端建置 Serverless App 且希望可以在單一應用程式中運行多個不同的服務 App-based 服務

    Cloud Run 希望能並行運作 Containers 來處理大量的服務或作業，則建議使用 Cloud Run



1. Cloud Run
   https://console.cloud.google.com/run?cloudshell=true&hl=zh-tw&project=unified-runner-411615

4. 上傳jar
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/0d27723a-800d-4713-800d-e610bc29ab0f)


5. 把檔案從storage複製到當前目錄
   gsutil cp gs://people_tw_2401/SearchWithIamKey1.1.jar .
   gsutil cp gs://people_tw_2401/unified-runner-411615-21002d0e9195.json .
   ```
   comtw2006@cloudshell:~ (unified-runner-411615)$ gsutil cp gs://people_tw_2401/SearchWithIamKey1.0.jar .
Copying gs://people_tw_2401/SearchWithIamKey1.0.jar...
- [1 files][ 54.1 MiB/ 54.1 MiB]                                                
Operation completed over 1 objects/54.1 MiB.  
   ```



2. 建立一個docker build 測試用的image
   docker build . --tag=test0418
```
comtw2006@cloudshell:~ (unified-runner-411615)$ docker build . --tag=test0418
[+] Building 9.9s (7/7) FINISHED                                                                                                                    docker:default
 => [internal] load build definition from Dockerfile                                                                                                          0.1s
 => => transferring dockerfile: 319B                                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/openjdk:17-jdk                                                                                             2.7s
 => [internal] load .dockerignore                                                                                                                             0.0s
 => => transferring context: 2B                                                                                                                               0.0s
 => [internal] load build context                                                                                                                             2.7s
 => => transferring context: 59.05MB                                                                                                                          2.7s
 => [1/2] FROM docker.io/library/openjdk:17-jdk@sha256:528707081fdb9562eb819128a9f85ae7fe000e2fbaeaf9f87662e7b3f38cb7d8                                       4.6s
 => => resolve docker.io/library/openjdk:17-jdk@sha256:528707081fdb9562eb819128a9f85ae7fe000e2fbaeaf9f87662e7b3f38cb7d8                                       0.0s
 => => sha256:a7203ca35e75e068651c9907d659adc721dba823441b78639fde66fc988f042f 187.53MB / 187.53MB                                                            1.7s
 => => sha256:528707081fdb9562eb819128a9f85ae7fe000e2fbaeaf9f87662e7b3f38cb7d8 1.04kB / 1.04kB                                                                0.0s
 => => sha256:98f0304b3a3b7c12ce641177a99d1f3be56f532473a528fda38d53d519cafb13 954B / 954B                                                                    0.0s
 => => sha256:5e28ba2b4cdb3a7c3bd0ee2e635a5f6481682b77eabf8b51a17ea8bfe1c05697 4.45kB / 4.45kB                                                                0.0s
 => => sha256:38a980f2cc8accf69c23deae6743d42a87eb34a54f02396f3fcfd7c2d06e2c5b 42.11MB / 42.11MB                                                              1.0s
 => => sha256:de849f1cfbe60b1c06a1db83a3129ab0ea397c4852b98e3e4300b12ee57ba111 13.53MB / 13.53MB                                                              0.4s
 => => extracting sha256:38a980f2cc8accf69c23deae6743d42a87eb34a54f02396f3fcfd7c2d06e2c5b                                                                     1.5s
 => => extracting sha256:de849f1cfbe60b1c06a1db83a3129ab0ea397c4852b98e3e4300b12ee57ba111                                                                     0.3s
 => => extracting sha256:a7203ca35e75e068651c9907d659adc721dba823441b78639fde66fc988f042f                                                                     1.6s
 => [2/2] COPY GoogleTranslate.jar /GoogleTranslate.jar                                                                                                       2.4s
 => exporting to image                                                                                                                                        0.1s
 => => exporting layers                                                                                                                                       0.1s
 => => writing image sha256:41ab0c9020abaf1b8b9ac100fec6dba1e13009e1293cbdb26ebfd9f75dd089fe                                                                  0.0s
 => => naming to docker.io/library/test0418                                                         
```
3. 建立容器 




![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/29ed49fa-b1b2-4c6e-96c0-ec8a1c0366aa)

3.1 要先登入 gcloud auth login

```
comtw2006@cloudshell:~ (unified-runner-411615)$ gcloud auth login

You are already authenticated with gcloud when running
inside the Cloud Shell and so do not need to run this
command. Do you wish to proceed anyway?

Do you want to continue (Y/n)?  Y

Go to the following link in your browser:

    https://accounts.google.com/o/oauth2/auth?response_type=code&client_id=32555940559.apps.googleusercontent.com&redirect_uri=https%3A%2F%2Fsdk.cloud.google.com%2Fauthcode.html&scope=openid+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fsqlservice.login+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Faccounts.reauth&state=oBPXLZfIG3pBOgjZby6Tz1XyZ3XUNn&prompt=consent&token_usage=remote&access_type=offline&code_challenge=pjW-lnm7HeKgw8gsd3MKaDBP0yjx27W43UBNbhEAZyg&code_challenge_method=S256

Enter authorization code: 4/0AeaYSHBI_Fdx4_LQZFrmcg38RQKVSjZEVpHZTZiKAINiTpWHocULWFjbyRl3NyMMNQsQZw

You are now logged in as [comtw2006@gmail.com].
Your current project is [unified-runner-411615].  You can change this setting by running:
  $ gcloud config set project PROJECT_ID
```

3.2 建立 Dockerfile
```
FROM openjdk:17-jdk
```
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/a8b500f1-a655-4b18-bbee-7389f537b311)

可能會出現
```
ERROR: (gcloud.config.set) The project property must be set to a valid project ID, [=unified-runner-411615] is not a valid project ID.
To set your project, run:

  $ gcloud config set project PROJECT_ID
```
執行 gcloud config set project unified-runner-411615 設定環境變數

3.3 提交一個包含 Dockerfile 的目錄，並建立一個 Docker 映像。

gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/dockerimage20240418

指令解析
將image建置到Registry

    gcloud: Google Cloud SDK 的命令列工具
    builds: Cloud Build 服務相關的命令
    submit: 提交一個建置工作
    --tag: 指定 Docker 映像的標籤
    gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:1.0.0: Docker 映像的完整路徑，包括專案 ID、映像名稱和版本號
    .: 指定當前的目錄作為建置工作的原始碼來源

指令功能

    掃描當前目錄中的 Dockerfile
    使用 Dockerfile 建置一個 Docker 映像
    將 Docker 映像推送到 Google Cloud Container Registry (GCR) 中
    指定 Docker 映像的標籤為 gcr.io/${GOOGLE_CLOUD_PROJECT}/dockerimage20240418


```
comtw2006@cloudshell:~ (unified-runner-411615)$ gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/dockerimage20240418
Creating temporary tarball archive of 117 file(s) totalling 223.0 MiB before compression.
Uploading tarball of [.] to [gs://unified-runner-411615_cloudbuild/source/1713375680.151767-b77d5bbf689b447eb0ab3b946351b951.tgz]
Created [https://cloudbuild.googleapis.com/v1/projects/unified-runner-411615/locations/global/builds/83bb0540-613c-4e0e-b3a7-55fa2d4fce1b].
Logs are available at [ https://console.cloud.google.com/cloud-build/builds/83bb0540-613c-4e0e-b3a7-55fa2d4fce1b?project=661587143193 ].
----------------------------------------------------------------------- REMOTE BUILD OUTPUT -----------------------------------------------------------------------
starting build "83bb0540-613c-4e0e-b3a7-55fa2d4fce1b"

FETCHSOURCE
Fetching storage object: gs://unified-runner-411615_cloudbuild/source/1713375680.151767-b77d5bbf689b447eb0ab3b946351b951.tgz#1713375708671957
Copying gs://unified-runner-411615_cloudbuild/source/1713375680.151767-b77d5bbf689b447eb0ab3b946351b951.tgz#1713375708671957...
- [1 files][192.0 MiB/192.0 MiB]                                                
Operation completed over 1 objects/192.0 MiB.
BUILD
Already have image (with digest): gcr.io/cloud-builders/docker
Sending build context to Docker daemon    234MB
Step 1/3 : FROM openjdk:17-jdk
17-jdk: Pulling from library/openjdk
38a980f2cc8a: Pulling fs layer
de849f1cfbe6: Pulling fs layer
a7203ca35e75: Pulling fs layer
de849f1cfbe6: Verifying Checksum
de849f1cfbe6: Download complete
38a980f2cc8a: Verifying Checksum
38a980f2cc8a: Download complete
a7203ca35e75: Verifying Checksum
a7203ca35e75: Download complete
38a980f2cc8a: Pull complete
de849f1cfbe6: Pull complete
a7203ca35e75: Pull complete
Digest: sha256:528707081fdb9562eb819128a9f85ae7fe000e2fbaeaf9f87662e7b3f38cb7d8
Status: Downloaded newer image for openjdk:17-jdk
 5e28ba2b4cdb
Step 2/3 : COPY "GoogleTranslate.jar" /GoogleTranslate.jar
 17269eb5b020
Step 3/3 : CMD ["java", "-jar", "/GoogleTranslate.jar"]
 Running in fa26c7a5c177
Removing intermediate container fa26c7a5c177
 d147dfeb102f
Successfully built d147dfeb102f
Successfully tagged gcr.io/unified-runner-411615/dockerimage20240418:latest
PUSH
Pushing gcr.io/unified-runner-411615/dockerimage20240418
The push refers to repository [gcr.io/unified-runner-411615/dockerimage20240418]
a6530323a0a5: Preparing
dc9fa3d8b576: Preparing
27ee19dc88f2: Preparing
c8dd97366670: Preparing
c8dd97366670: Layer already exists
dc9fa3d8b576: Layer already exists
27ee19dc88f2: Layer already exists
a6530323a0a5: Pushed
latest: digest: sha256:efaa98464d1010a9201ce94905e06985e0ea800c3b30bfbad0806ab63f138e0e size: 1166
DONE
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
ID: 83bb0540-613c-4e0e-b3a7-55fa2d4fce1b
CREATE_TIME: 2024-04-17T17:41:49+00:00
DURATION: 32S
SOURCE: gs://unified-runner-411615_cloudbuild/source/1713375680.151767-b77d5bbf689b447eb0ab3b946351b951.tgz
IMAGES: gcr.io/unified-runner-411615/dockerimage20240418 (+1 more)
STATUS: SUCCESS
```

    ![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/4031465d-07a4-4d3f-b486-6c67fda7bd6d)





4. 執行
gcloud run deploy --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/dockerimage20240418 --platform managed


這段指令是用於 Google Cloud Run 的 gcloud run deploy 指令，用於部署一個 Docker 映像到 Cloud Run 上。

指令解析

    gcloud: Google Cloud SDK 的命令列工具
    run: Cloud Run 服務相關的命令
    deploy: 部署一個 Cloud Run 服務
    --image: 指定要部署的 Docker 映像
    gcr.io/${GOOGLE_CLOUD_PROJECT}/dockerimage20240418: Docker 映像的完整路徑，包括專案 ID、映像名稱和版本號
    --platform managed: 指定使用 Cloud Run 的完全託管平台

指令功能

    將位於 gcr.io/${GOOGLE_CLOUD_PROJECT}/dockerimage20240418 的 Docker 映像拉取到 Cloud Run 中
    建立一個 Cloud Run 服務
    將 Docker 映像設定為該 Cloud Run 服務的容器映像
    啟動 Cloud Run 服務

```

```

   

2. 建立服務
   ![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/62db5da5-056e-40bf-bc58-cb60bd2a55fa)


   










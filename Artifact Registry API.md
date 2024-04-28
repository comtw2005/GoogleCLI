Artifact Registry API

啟用

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/25937d46-0a5e-449e-a361-fe312a0aaebf)


啟用安全漏洞掃描功能
您的登錄庫並未啟用已知安全漏洞的監控功能。GCP 會自動為過去 30 天內推送或提取的所有映像檔監控安全漏洞，每個映像檔的費用為 $0.26。
Ref: https://cloud.google.com/artifact-analysis/docs/container-scanning-overview?authuser=1&_gl=1*16fz0da*_ga*MTQzODk3OTU2OS4xNzAyNDgxMzU0*_ga_WH2QY8WWF5*MTcxNDMxNzIxMC41Ni4xLjE3MTQzMTc1OTcuMC4wLjA.&_ga=2.186007337.-1438979569.1702481354&_gac=1.56175961.1714312319.CjwKCAjw57exBhAsEiwAaIxaZqFz6u7grthXkt5vVtaWeRJCAj_9SuBOc_OVzw4pzT04yI-MsrJQ7hoCgOQQAvD_BwE

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/d71917e4-6626-4a6b-9e5e-af8554907447)

建立Repository 
建置完 Repository 後，為了讓使用者能透過這個 Repository 推送及提取套件

建立存放區

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/8a9949e9-1b0a-4af6-89d9-907880fcfccb)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/94d09a7e-0a2b-4760-a53e-914240cbe263)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/e71cfcc2-de9e-4191-9876-8d196bfe1244)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/69efe6a9-7c2a-4d1c-9917-b8a414884540)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/c3a9b1bc-0751-497d-8ba7-315d3720c7e7)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/3799f89b-15d9-4fb1-9dc5-e8242d81644c)

```
gcloud auth configure-docker \
    asia-east1-docker.pkg.dev
```
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/43f519d7-9b34-4a6c-a8de-bec6ad4929a4)

顯示 Credential helper 的相關資訊，代表指令執行成功，身份驗證完成。


用Google的Sample image做舉例, 透過 docker pull 指令，將 Image 下載到我們自己的環境中。

要認證, 但是沒理他好像也沒差

```
docker pull us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
```

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/27bc6784-75be-4cf0-966a-4ef9daa40d02)

Artifact Registry 中的映像路径包含多个部分：

us 是代码库的位置。
docker.pkg.dev 是存储在 Artifact Registry Docker 代码库中的容器映像的主机名。
google-samples 是代码库 ID。
containers/gke/ 是 google-samples 下的映像路径。

将映像添加到代码库中
docker tag 指令，將下載的 Image 在自己的環境內訂定標籤 tag1，若沒有指定則 docker 會預設為 latest

```
docker tag us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0 \
us-central1-docker.pkg.dev/big-dynamo-421713/quickstart-docker-repo/quickstart-image:tag1
```
查看 doker image

```
 docker image list
```

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/8564857a-0c93-4d5e-8bc7-7592851f70af)


将映像推送到 Artifact Registry  






























ref: https://blog.cloud-ace.tw/application-modernization/serverless/cloud-run-overview-and-tutorial/

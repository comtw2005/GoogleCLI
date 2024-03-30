![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/23a864d2-b5f1-4b1c-96c0-818edaa45ea8)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/14079986-ed6f-46af-afb0-079c25a52519)


![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/3faf6f27-22cb-40e2-9b12-eda521c59d5c)
Cloud storage
值區詳細資料
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/ea9455bc-7d8f-4a98-9634-315c3a7c81bc)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/c5cad58c-707a-43a8-8b95-437dcf964890)


Cloud storage
授予存取權
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/1ee4d10c-121c-4a90-be9c-1536e702465a)


Cloud shell列出storage所有檔案
gsutil ls gs://people_tw_2401

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/fde5867c-1895-4079-80b2-fc9ef3810a97)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/4527f132-54a7-4ea0-b0cf-da418b303980)

gsutil cp gs://people_tw_2401/GoogleTranslate.jar .

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/accae8d1-7570-45f5-8756-e0f2c4a9c762)


Dockerfile
```
FROM openjdk:17-jdk

#COPY gs://people_tw_2401/GoogleTranslate.jar /GoogleTranslate.jar

CMD ["java", "-jar", "/GoogleTranslate.jar"]
```

docker build . --tag=search

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/bf0b584e-90c7-4810-a44f-eedb304c5300)

gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/search_builds

```
Creating temporary tarball archive of 67 file(s) totalling 56.4 MiB before compression.
Uploading tarball of [.] to [gs://unified-runner-411615_cloudbuild/source/1711816102.96094-7fc7336ef3d44db68de778eab1354b77.tgz]
Created [https://cloudbuild.googleapis.com/v1/projects/unified-runner-411615/locations/global/builds/571172e6-9ba6-4de3-938b-3e2a90c1eff3].
Logs are available at [ https://console.cloud.google.com/cloud-build/builds/571172e6-9ba6-4de3-938b-3e2a90c1eff3?project=661587143193 ].
----------------------------------------------------------------------------------- REMOTE BUILD OUTPUT ------------------------------------------------------------------------------------
starting build "571172e6-9ba6-4de3-938b-3e2a90c1eff3"

FETCHSOURCE
Fetching storage object: gs://unified-runner-411615_cloudbuild/source/1711816102.96094-7fc7336ef3d44db68de778eab1354b77.tgz#1711816112922364
Copying gs://unified-runner-411615_cloudbuild/source/1711816102.96094-7fc7336ef3d44db68de778eab1354b77.tgz#1711816112922364...
/ [1 files][ 51.7 MiB/ 51.7 MiB]                                                
Operation completed over 1 objects/51.7 MiB.
BUILD
Already have image (with digest): gcr.io/cloud-builders/docker
Sending build context to Docker daemon  59.17MB
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
 51d7235d2fbd
Step 3/3 : CMD ["java", "-jar", "/GoogleTranslate.jar"]
 Running in b5eb688bc403
Removing intermediate container b5eb688bc403
 880a4bda8377
Successfully built 880a4bda8377
Successfully tagged gcr.io/unified-runner-411615/search_builds:latest
PUSH
Pushing gcr.io/unified-runner-411615/search_builds
The push refers to repository [gcr.io/unified-runner-411615/search_builds]
a6530323a0a5: Preparing
dc9fa3d8b576: Preparing
27ee19dc88f2: Preparing
c8dd97366670: Preparing
c8dd97366670: Layer already exists
dc9fa3d8b576: Layer already exists
27ee19dc88f2: Layer already exists
a6530323a0a5: Pushed
latest: digest: sha256:62b9013024b8dd690395f6196fe615eb747d1e27012e97529d93dc99ec48eb0b size: 1166
DONE
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
ID: 571172e6-9ba6-4de3-938b-3e2a90c1eff3
CREATE_TIME: 
```

gcloud run deploy --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/searchbuilds --platform managed

```

```







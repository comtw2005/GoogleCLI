https://joehuang-pop.github.io/2020/05/01/GCP-Cloud-Run-%E5%85%AD%E5%80%8B%E5%AF%A6%E4%BD%9C-%E8%A7%A3%E6%9E%90%E9%BA%BB%E9%9B%80%E9%9B%96%E5%B0%8F%E4%BA%94%E8%87%9F%E4%BF%B1%E5%85%A8-Cloud-Run-is-Small-but-Complete/

https://medium.com/@blaze0207/google-cloud-build-%E6%95%99%E5%AD%B8-%E4%B8%80-ed7103d3fb62


comtw2006@cloudshell:~ (unified-runner-411615)$ docker build . --tag=test1
```
[+] Building 2.3s (7/7) FINISHED                                                                                                                    docker:default
 => [internal] load build definition from Dockerfile                                                                                                          0.0s
 => => transferring dockerfile: 93B                                                                                                                           0.0s
 => [internal] load metadata for docker.io/library/alpine:latest                                                                                              1.5s
 => [internal] load .dockerignore                                                                                                                             0.0s
 => => transferring context: 2B                                                                                                                               0.0s
 => [internal] load build context                                                                                                                             0.0s
 => => transferring context: 92B                                                                                                                              0.0s
 => [1/2] FROM docker.io/library/alpine:latest@sha256:c5b1261d6d3e43071626931fc004f70149baeba2c8ec672bd4f27761f8e1ad6b                                        0.6s
 => => resolve docker.io/library/alpine:latest@sha256:c5b1261d6d3e43071626931fc004f70149baeba2c8ec672bd4f27761f8e1ad6b                                        0.0s
 => => sha256:c5b1261d6d3e43071626931fc004f70149baeba2c8ec672bd4f27761f8e1ad6b 1.64kB / 1.64kB                                                                0.0s
 => => sha256:6457d53fb065d6f250e1504b9bc42d5b6c65941d57532c072d929dd0628977d0 528B / 528B                                                                    0.0s
 => => sha256:05455a08881ea9cf0e752bc48e61bbd71a34c029bb13df01e40e3e70e0d007bd 1.47kB / 1.47kB                                                                0.0s
 => => sha256:4abcf20661432fb2d719aaf90656f55c287f8ca915dc1c92ec14ff61e67fbaf8 3.41MB / 3.41MB                                                                0.4s
 => => extracting sha256:4abcf20661432fb2d719aaf90656f55c287f8ca915dc1c92ec14ff61e67fbaf8                                                                     0.1s
 => [2/2] COPY quickstart.sh /                                                                                                                                0.0s
 => exporting to image                                                                                                                                        0.0s
 => => exporting layers                                                                                                                                       0.0s
 => => writing image sha256:e5c4fb3d5a85e5295bbaf55ac8cc9b57cddef953fa49f1286cfb17d3309b8471                                                                  0.0s
 => => naming to docker.io/library/test1                     
```

gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:1.0.0 .

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/202a05ec-2819-4214-96b1-85f6af25de63)


comtw2006@cloudshell:~ (unified-runner-411615)$ gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:1.0.0 .
```
Creating temporary tarball archive of 31 file(s) totalling 33.7 KiB before compression.
Uploading tarball of [.] to [gs://unified-runner-411615_cloudbuild/source/1711471485.134728-896700bb46fd42a7bf3222a65d01d77d.tgz]
API [cloudbuild.googleapis.com] not enabled on project [unified-runner-411615]. Would you like to enable and retry (this will take a few minutes)? (y/N)?  y

Enabling service [cloudbuild.googleapis.com] on project [unified-runner-411615]...
Operation "operations/acf.p2-661587143193-d6c583fb-1586-4869-b5f5-81b39da703de" finished successfully.
Created [https://cloudbuild.googleapis.com/v1/projects/unified-runner-411615/locations/global/builds/21379cfd-a5db-4f05-a0c1-c92e19d635f5].
Logs are available at [ https://console.cloud.google.com/cloud-build/builds/21379cfd-a5db-4f05-a0c1-c92e19d635f5?project=661587143193 ].
----------------------------------------------------------------------- REMOTE BUILD OUTPUT -----------------------------------------------------------------------
starting build "21379cfd-a5db-4f05-a0c1-c92e19d635f5"

FETCHSOURCE
Fetching storage object: gs://unified-runner-411615_cloudbuild/source/1711471485.134728-896700bb46fd42a7bf3222a65d01d77d.tgz#1711471487656459
Copying gs://unified-runner-411615_cloudbuild/source/1711471485.134728-896700bb46fd42a7bf3222a65d01d77d.tgz#1711471487656459...
/ [1 files][  7.9 KiB/  7.9 KiB]                                                
Operation completed over 1 objects/7.9 KiB.
BUILD
Already have image (with digest): gcr.io/cloud-builders/docker
Sending build context to Docker daemon  67.58kB
Step 1/3 : FROM alpine
latest: Pulling from library/alpine
Digest: sha256:c5b1261d6d3e43071626931fc004f70149baeba2c8ec672bd4f27761f8e1ad6b
Status: Downloaded newer image for alpine:latest
 05455a08881e
Step 2/3 : COPY quickstart.sh /
 b2a24229cfbe
Step 3/3 : CMD ["/quickstart.sh"]
 Running in c1768d1b1550
Removing intermediate container c1768d1b1550
 4e2fa8d7763a
Successfully built 4e2fa8d7763a
Successfully tagged gcr.io/unified-runner-411615/monolith:1.0.0
PUSH
Pushing gcr.io/unified-runner-411615/monolith:1.0.0
The push refers to repository [gcr.io/unified-runner-411615/monolith]
8997af9e23a3: Preparing
d4fc045c9e3a: Preparing
8997af9e23a3: Pushed
d4fc045c9e3a: Layer already exists
1.0.0: digest: sha256:caef3e42ee6901a95da514e8ca43a08720de3d66a1ed323662b775288ad1bb0d size: 735
DONE
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
ID: 21379cfd-a5db-4f05-a0c1-c92e19d635f5
CREATE_TIME: 2024-03-26T16:45:32+00:00
DURATION: 25S
SOURCE: gs://unified-runner-411615_cloudbuild/source/1711471485.134728-896700bb46fd42a7bf3222a65d01d77d.tgz
IMAGES: gcr.io/unified-runner-411615/monolith:1.0.0
STATUS: SUCCESS
```



comtw2006@cloudshell:~ (unified-runner-411615)$ gcloud run deploy --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:1.0.0 --platform managed
```
Service name (monolith):  monolith
Please specify a region:
 [1] africa-south1
 [2] asia-east1
 [3] asia-east2
 [4] asia-northeast1
 [5] asia-northeast2
 [6] asia-northeast3
 [7] asia-south1
 [8] asia-south2
 [9] asia-southeast1
 [10] asia-southeast2
 [11] australia-southeast1
 [12] australia-southeast2
 [13] europe-central2
 [14] europe-north1
 [15] europe-southwest1
 [16] europe-west1
 [17] europe-west10
 [18] europe-west12
 [19] europe-west2
 [20] europe-west3
 [21] europe-west4
 [22] europe-west6
 [23] europe-west8
 [24] europe-west9
 [25] me-central1
 [26] me-central2
 [27] me-west1
 [28] northamerica-northeast1
 [29] northamerica-northeast2
 [30] southamerica-east1
 [31] southamerica-west1
 [32] us-central1
 [33] us-east1
 [34] us-east4
 [35] us-east5
 [36] us-south1
 [37] us-west1
 [38] us-west2
 [39] us-west3
 [40] us-west4
 [41] cancel
Please enter numeric choice or text value (must exactly match list item):  2

To make this the default region, run `gcloud config set run/region asia-east1`.

Allow unauthenticated invocations to [monolith] (y/N)?  y

Deploying container to Cloud Run service [monolith] in project [unified-runner-411615] region [asia-east1]
X  Deploying new service...                                                                                                                                       
  -  Creating Revision...                                                                                                                                         
  .  Routing traffic...                                                                                                                                           
  OK Setting IAM Policy...                                                                                                                                        
Deployment failed                                                                                                                                                 
ERROR: (gcloud.run.deploy) Revision 'monolith-00001-sb7' is not ready and cannot serve traffic. The user-provided container failed to start and listen on the port defined provided by the PORT=8080 environment variable. Logs for this revision might contain more information.

Logs URL: https://console.cloud.google.com/logs/viewer?project=unified-runner-411615&resource=cloud_run_revision/service_name/monolith/revision_name/monolith-00001-sb7&advancedFilter=resource.type%3D%22cloud_run_revision%22%0Aresource.labels.service_name%3D%22monolith%22%0Aresource.labels.revision_name%3D%22monolith-00001-sb7%22 
For more troubleshooting guidance, see https://cloud.google.com/run/docs/troubleshooting#container-failed-to-start
```
comtw2006@cloudshell:~ (unified-runner-411615)$ 


![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/5af01fed-af1d-4e3d-b2bf-4fd43dbd4f76)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/dd48d132-83cf-4644-aec7-e1abce3732bd)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/fd039921-d86f-4d2d-8cc0-1da98ae02970)

IAM 權限控管

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/f3bbb8c2-a9d0-4852-9700-4dd646c0c0a4)

用手動輸入

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/26b71515-8dce-4781-8388-026bf52cfd94)

結果不行
無法部署修訂版本

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/c26f8089-f0e1-4540-9db1-206e2d178386)

建立新的服務帳戶

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/fe1d2bd4-5da9-41e4-8110-49ae98d154c8)

服務帳戶詳細資料

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/0eda270a-6122-4744-a6a7-0b3fe972457a)

將專案存取權授予這個服務帳戶 (選用)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/1ff4fb8b-b0cb-439e-872c-ee2c1171b4a4)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/c11e49fa-921b-412e-ab2d-139926a6abe3)

又有問題

 Revision 'monolith-00002-xp9' is not ready and cannot serve traffic. The user-provided container failed to start and listen on the port defined provided by the PORT=8080 environment variable. Logs for this revision might contain more information. Logs URL: 開啟 Cloud Logging  For more troubleshooting guidance, see https://cloud.google.com/run/docs/troubleshooting#container-failed-to-start 

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/83fe8d83-5ec2-4bdc-8b70-e06754a90362)

















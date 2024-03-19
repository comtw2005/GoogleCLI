# Dataproc

https://cloud.google.com/dataproc?hl=zh-TW

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/750e8ac3-a0eb-4f53-9ea8-4d4f9b33f0d4)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/beecec42-176e-4928-a3c6-7a62e9eeead4)

Cloud Dataproc API

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/07b69421-bf43-45b2-8292-ad99def12246)

Create Cluster

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/c29e01d0-7ce4-416c-8a4d-8f366abfc741)

建立 Dataproc 叢集
=> Compute Engine 上的叢集
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/888265d2-998f-4cec-b0dc-79ea5ab77fa5)

設定叢集

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/fb5821ed-acc1-4390-8d26-33b5840b418e)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/76df92f2-373b-43dd-9f06-4a6797d0f21f)

設定節點

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/a7a9ecfc-921f-4cf6-ba16-b8623d9ad6f0)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/da2ee9ab-965a-4c22-aaef-c0f622eb3f17)

自訂叢集 (選擇性步驟)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/e9536dbb-e5a6-41eb-ab85-fa2cbaa1a13d)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/392297fb-5676-428e-817e-bad57f6c250d)

處裡錯誤訊息
不知道是不是測試用所以資源不足, 全部用最低階才過

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/7f058181-fb92-469a-87f6-97f2ad6ff88a)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/4db07803-94d5-41df-9cc5-1d8c75947b5e)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/140dddcf-a24e-497e-99c2-cd7f0d883842)

錯誤處理結束

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/4c4cc237-09e6-4384-9e7b-885c5b48b1a5)

叢集警告

Failed to validate permissions required for google cloud dataproc service agent service account: 'service-661587143193@dataproc-accounts.iam.gserviceaccount.com'. Cluster creation could still be successful if required permissions have been granted to the respective service accounts as mentioned in the document https://cloud.google.com/dataproc/docs/concepts/configuring-clusters/service-accounts#dataproc_service_accounts_2.
For PD-Standard without local SSDs, we strongly recommend provisioning 1TB or larger to ensure consistently high I/O performance. See https://cloud.google.com/compute/docs/disks/performance for information on disk I/O performance.
Permissions are missing for the default service account '661587143193-compute@developer.gserviceaccount.com', missing permissions: [storage.buckets.get, storage.objects.create, storage.objects.delete, storage.objects.get, storage.objects.list, storage.objects.update] on the project 'projects/unified-runner-411615'. This usually happens when a custom resource (ex: custom staging bucket) or a user-managed VM Service account has been provided and the default/user-managed service account hasn't been granted enough permissions on the resource. See https://cloud.google.com/dataproc/docs/concepts/configuring-clusters/service-accounts#VM_service_account.
The firewall rules for specified network or subnetwork would allow ingress traffic from 0.0.0.0/0, which could be a security risk.


















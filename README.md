# GoogleCLI


Windows (Zip)
https://cloud.google.com/sdk/docs/downloads-interactive?hl=zh-cn#windows

設定環境變數 CLOUDSDK_PYTHON
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/cfbe2961-0e3b-4407-a37e-300c9fc7864e)

執行 install.bat
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/7db1acbc-70ae-407f-b7f3-0b8fa94411da)

```
To help improve the quality of this product, we collect anonymized usage data
and anonymized stacktraces when crashes are encountered; additional information
is available at <https://cloud.google.com/sdk/usage-statistics>. This data is
handled in accordance with our privacy policy
<https://cloud.google.com/terms/cloud-privacy-notice>. You may choose to opt in this
collection now (by choosing 'Y' at the below prompt), or at any time in the
future by running the following command:

    gcloud config set disable_usage_reporting false

Do you want to help improve the Google Cloud CLI (y/N)?  N


This will install all the core command line tools necessary for working with
the Google Cloud Platform.

Beginning update. This process may take several minutes.

This will install all the core command line tools necessary for working with
the Google Cloud Platform.

Beginning update. This process may take several minutes.


Your current Google Cloud CLI version is: 466.0.0
Installing components from version: 466.0.0

┌─────────────────────────────────────────────────────────────────────────────┐
│                     These components will be installed.                     │
├─────────────────────────────────────────────────────┬────────────┬──────────┤
│                         Name                        │  Version   │   Size   │
├─────────────────────────────────────────────────────┼────────────┼──────────┤
│ BigQuery Command Line Tool                          │    2.0.101 │  1.6 MiB │
│ BigQuery Command Line Tool (Platform Specific)      │    2.0.101 │  < 1 MiB │
│ Cloud Storage Command Line Tool                     │       5.27 │ 11.3 MiB │
│ Cloud Storage Command Line Tool (Platform Specific) │       5.27 │  < 1 MiB │
│ Google Cloud CLI Core Libraries (Platform Specific) │ 2024.02.26 │  < 1 MiB │
│ Google Cloud CRC32C Hash Tool                       │      1.0.0 │  1.3 MiB │
│ Windows command line ssh tools                      │            │  3.3 MiB │
│ anthoscli                                           │     0.2.48 │ 69.5 MiB │
│ gcloud cli dependencies                             │ 2021.04.16 │  < 1 MiB │
└─────────────────────────────────────────────────────┴────────────┴──────────┘

For the latest full release notes, please visit:
  https://cloud.google.com/sdk/release_notes

Performing in place update...

╔════════════════════════════════════════════════════════════╗
╠═ Installing: BigQuery Command Line Tool                   ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: BigQuery Command Line Tool (Platform Spec... ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Cloud Storage Command Line Tool              ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Cloud Storage Command Line Tool (Platform... ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Default set of gcloud commands               ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Google Cloud CLI Core Libraries (Platform... ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Google Cloud CRC32C Hash Tool                ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Google Cloud CRC32C Hash Tool                ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Windows command line ssh tools               ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: Windows command line ssh tools               ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: anthoscli                                    ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: anthoscli                                    ═╣
╠════════════════════════════════════════════════════════════╣
╠═ Installing: gcloud cli dependencies                      ═╣
╚════════════════════════════════════════════════════════════╝

Performing post processing steps...done.

Update done!
Update %PATH% to include Cloud SDK binaries? (Y/n)?  Y

The installer is unable to automatically update your system PATH. Please add
  D:\google-cloud-sdk\bin
to your system PATH to enable easy use of the Cloud SDK Command Line Tools.


For more information on how to get started, please visit:
  https://cloud.google.com/sdk/docs/quickstarts


Google Cloud CLI installer will now exit.
Press any key to continue . . .
```

4. 執行 gcloud init：
```
C:\Users\Macro>gcloud init
Welcome! This command will take you through the configuration of gcloud.

Your current configuration has been set to: [default]

You can skip diagnostics next time by using the following flag:
  gcloud init --skip-diagnostics

Network diagnostic detects and fixes local network connection issues.
Checking network connection...done.
Reachability Check passed.
Network diagnostic passed (1/1 checks passed).

You must log in to continue. Would you like to log in (Y/n)?  Y

Your browser has been opened to visit:

    https://accounts.google.com/o/oauth2/auth?response_type=code&client_id=32555940559.apps.googleusercontent.com&redirect_uri=http%3A%2F%2Flocalhost%3A8085%2F&scope=openid+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fsqlservice.login+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Faccounts.reauth&state=GspSGdlvjhjMcpdHjzuKpEvsL64lTF&access_type=offline&code_challenge=OMW3LTQ5WZVfV59_wEN_RDI80AQLEFAFy6zvzAJxoUk&code_challenge_method=S256
```
![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/c8caa44a-2415-468c-aefe-e5d18ac8a96a)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/7ec4c37f-fe4a-4c15-b6ac-3a2599adfee3)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/f725523e-1d98-4c7a-a514-e5973b5cc008)

![圖片](https://github.com/comtw2005/GoogleCLI/assets/46416652/d7c31b02-a3a7-4819-9bdd-02a1d1d1e9e9)







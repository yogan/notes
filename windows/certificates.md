# Certificates

## Import a Certificate

If a custom certificate (e.g. from LetsEncrypt) is shown as not trusted,
you can import it into Windows' certificate store from PowerShell:

```ps
Import-Certificate -FilePath mycert.cer -CertStoreLocation cert:\CurrentUser\Root
```

See [Import-Certificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/import-certificate?view=windowsserver2019-ps)
documentation for more details.

*Note:* Browsers might need to be restarted so that they pick up a new
certificate.


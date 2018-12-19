# https

---

## testfile中的原有内容为
```
 javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
 
framework类InstallCert，替换URL执行，生成文件jssecacerts
系统加载
System.setProperty("javax.net.ssl.trustStore", "jssecacerts")
```






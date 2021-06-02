# Digitally Sign Files (PowerShell Example)

From:
- https://sid-500.com/2017/10/26/how-to-digitally-sign-powershell-scripts/

---

### Creating a self-signed Certificate
Open Windows PowerShell and run the following One-Liner to create a signing certificate.
```
New-SelfSignedCertificate -DnsName patrick@sid-500.com -CertStoreLocation Cert:\CurrentUser\My\ -Type Codesigning
```

You can find your certificate in your certificate store. Run certmgr.msc.
```
C:\> certmgr.msc
```

### Import the Certifcate in Trusted Root Certification Autorities and Trusted Publisher
Now the certificate must be exported and then imported into the Trusted Root Certification Authorities and Trusted Publishers.

![8ab02b88ef77cc3546efeee221572d2e.png](01c755616c37409d9a91f8fc28a223bd.png)

Double click on the certificate and select Details and Copy to file …
![7da14c9eb1d42a665ffae8244e61bf1c.png](85856ae7e84f4fe89154a499edc43773.png)

Do not export the private key. No need for.
![4240f7f1c67a23c0acf1fa744440ce76.png](a8be732fd6d44e879f928508be4bb621.png)

Select CER Format.
![a17b4ff14cc80167800b1d0a245218d5.png](cbaf5715e50e49b4b1f7ea1054de699f.png)

Save the file wherever you want.
Now import the certificate to the Trusted Root Authorities and Trusted Publishers.
![c79078e168a1d1c4504bce07cd58afd3.png](82f69142dabb4869b26d4f67012e37a1.png)

### Sign a file
Next, we use Set-Authenticodesignature to sign our file. In this example, it is a. ps1 file, thus a PowerShell script.
```
Set-AuthenticodeSignature -FilePath C:\Temp\script1.ps1 -Certificate (Get-ChildItem -Path Cert:\CurrentUser\My\ -CodeSigningCert)
```
![0cb6fed0f5db13b2943b1a837a962d06.png](0a9bae45476446168bd4f25df62a8683.png)

Don’t worry about the Status Unknown Error. The next time you do it valid comes up. Crazy Stuff. Ok, we don’t care about this now.

![df6e6cb7c6cd61d70e212b8460172018.png](b3854b51c85d4b9e96e84915a301a9ab.png)

Nice. Finally, see what happened. Open Windows Explorer, right click on your file, select properties and click on Digital Signatures.

![2abe4c022a4bb94a20940d9c50a6d563.png](f1260c871f424085b77029787866c60e.png)

### Testing your script
For testing your script, make sure the execution policy allows the running of PS1 scripts.
```
Get-ExecutionPolicy
```
Remotesigned, AllSigned and Unrestricted are your friends … If the policy is set to restricted then set it – for this testing environment – to AllSigned.
```
Set-ExecutionPolicy AllSigned
```
![e51fab04194a66b4edb32ee902ff341b.png](e922a3614f8c4974bdc2e402fba6a81f.png)

---

#powershell
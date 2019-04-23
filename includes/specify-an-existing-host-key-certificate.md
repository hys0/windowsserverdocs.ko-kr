또는 사용자 고유의 인증서를 사용 하려는 경우 지문을 지정할 수 있습니다. 이 여러 컴퓨터에 인증서를 공유 하거나 TPM 또는 HSM에 바인딩된 인증서를 사용 하려는 경우에 유용할 수 있습니다. TPM 바인딩된 인증서 (개인 키를 도난당 하 고 다른 컴퓨터에서 사용할 수 없도록 방지 및 TPM 1.2만 필요)을 만드는 예제는 다음과 같습니다.

```powersehll
$tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
```


<!-- Appears in set-up-hgs-for-always-encrypted-in-sql-server.md and guarded-fabric-create-host-key.md
-->
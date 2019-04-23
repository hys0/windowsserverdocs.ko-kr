먼저 인증 기관에서 HGS에 대 한 SSL 인증서를 가져옵니다. 각 호스트 컴퓨터 되므로 회사의 공용 키 인프라 또는 타사 CA에서에서 SSL 인증서를 발급 하는 것이 좋습니다. SSL 인증서를 신뢰 해야 합니다. 그러나 IIS에서 지 원하는 모든 SSL 인증서가 지 HGS **인증서의 주체 이름은 정규화 된 HGS 서비스 이름과 일치 해야** (클러스터 분산된 네트워크 이름). 예를 들어 HGS 도메인 "bastion.local" 이며 HGS 서비스 이름을 "hgs"을 하는 경우 "hgs.bastion.local"에 대 한 SSL 인증서를 발급 해야 합니다. 추가 DNS 이름이 필요한 경우 인증서의 주체 대체 이름 필드를 추가할 수 있습니다.

SSL 인증서, 관리자 권한 PowerShelll 세션 열기를 해야 하 고 실행 하는 경우 인증서 경로 제공 하거나 [집합 HgsServer](https://technet.microsoft.com/itpro/powershell/windows/host-guardian-service/server/set-hgsserver):


```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

또는 로컬 인증서 저장소로 인증서를 이미 설치한 경우 문으로 참조할 수 있습니다.

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

> [!IMPORTANT]
> SSL 인증서를 사용 하 여 HGS를 구성 하는 HTTP 끝점을 해제 되지 않습니다.
> HTTPS 끝점을 사용 하 여 허용 하려는 경우 포트 80에 인바운드 연결을 차단 하도록 Windows 방화벽을 구성 합니다.
> **IIS 바인딩을 수정 하지 마십시오** HTTP 끝점을 제거할 HGS 웹 사이트에 대 한 것은 지원 되지 않습니다 이렇게 하려면.

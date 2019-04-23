호스트 보호 서비스는 별도 Active Directory 포리스트에 설치 되어야 합니다.
HGS 컴퓨터 인지 확인 **되지** 시작 및 청구서는 로컬 컴퓨터와 로그인 하기 전에 도메인에 가입 합니다.

호스트 보호자 서비스를 설치 하 고 해당 도메인을 구성 하려면 다음 명령을 실행 합니다.
여기에서 지정한 암호; Active Directory 디렉터리 서비스 복구 모드 암호에만 적용 됩니다. 됩니다 *되지* 관리자 계정의 로그인 암호를 변경 합니다.
-HgsDomainName 원하는 도메인 이름을 제공할 수 있습니다.

```powershell
$adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force

Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
```

<!-- Appears in guarded-fabric-install-hgs-default.md and set-up-hgs-for-always-encrypted-in-sql-server.md
-->

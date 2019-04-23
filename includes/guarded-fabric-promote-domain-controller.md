1.  실행할 [설치 HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/install-hgsserver) 도메인에 가입 하 여 노드를 도메인 컨트롤러로 승격 합니다.

    ```powershell
    $adSafeModePassword = ConvertTo-SecureString -AsPlainText '<password>' -Force

    $cred = Get-Credential 'relecloud\Administrator'

    Install-HgsServer -HgsDomainName 'bastion.local' -HgsDomainCredential $cred -SafeModeAdministratorPassword $adSafeModePassword -Restart
    ```

2.  서버가 다시 부팅 하는 경우 도메인 관리자 계정으로 로그인 합니다.

<!-- Appears twice in guarded-fabric-configure-additional-hgs-nodes.md 
-->
지문을 사용 하 여 HGS를 인증서를 제공 하면 HGS 해당 인증서의 개인 키에 대 한 읽기 액세스를 부여 하 라는 지침이 나타납니다. 설치 하는 데스크톱 환경 포함 서버에서 다음 단계를 수행 합니다.

1.  로컬 컴퓨터 인증서 관리자를 엽니다 (**certlm.msc**)
2.  인증서를 찾을 > 마우스 오른쪽 단추로 클릭 > 모든 작업 > 개인 키 관리
3.  **추가**를 클릭합니다.
4.  개체 선택 창에서 클릭 **개체 유형** 높이고 **서비스 계정**
5.  경고 텍스트에 언급 된 서비스 계정의 이름을 입력 합니다. `Initialize-HgsServer`
6.  GMSA에 개인 키에 대 한 "읽기" 액세스 확인 합니다.

Server core에서 개인 키 사용 권한을 설정 하는 데 도움이 되는 PowerShell 모듈을 다운로드 해야 합니다.

1.  실행할 `Install-Module GuardedFabricTools` HGS 서버에 인터넷 연결 또는 실행 하는 경우에 `Save-Module GuardedFabricTools` 다른 컴퓨터에 모듈을 통해 HGS 서버에 복사 합니다.
2.  `Import-Module GuardedFabricTools`을 실행합니다. 이렇게 하면 추가 속성에에서 있는 인증서 개체에 추가 됩니다.
3.  인증서 지문을 사용 하 여 PowerShell에서 찾기 `Get-ChildItem Cert:\LocalMachine\My`
4.  ACL을 업데이트, 경고 텍스트에 나열 된 고유한 지문 및 계정 사용 하 여 다음 코드에서 gMSA 계정 교체 `Initialize-HgsServer`합니다.

    ```powershell
    $certificate = Get-Item "Cert:\LocalMachine\1A2B3C..."
    $certificate.Acl = $certificate.Acl | Add-AccessRule "HgsSvc_1A2B3C" Read Allow
    ```

HSM 기반 인증서를 사용 하는 또는 인증서에 저장 하는 경우 타사 키 저장소 공급자를를 이러한 단계가 적용 되지 않을 수 있습니다. 개인 키에 대 한 권한을 관리 하는 방법을 알아보려면 키 저장소 공급자의 설명서를 참조 하세요. 일부 경우에는 권한이 부여 되지 않습니다 또는 권한 부여 인증서를 설치할 때 컴퓨터 전체에 제공 됩니다.

<!-- Appears in guarded-fabric-initialize-hgs-ad-mode-default.md and guarded-fabric-initialize-hgs-tpm-mode-default.md
-->
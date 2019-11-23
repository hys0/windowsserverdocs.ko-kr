---
title: 보호 된 호스트가 증명할 수 있는지 확인
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 7485796b-b840-4678-9b33-89e9710fbbc7
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: 2bab2b653127ae13d27dea76225ada91b3ee8ecc
ms.sourcegitcommit: de71970be7d81b95610a0977c12d456c3917c331
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71940692"
---
# <a name="confirm-guarded-hosts-can-attest"></a>보호 된 호스트가 증명할 수 있는지 확인

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

패브릭 관리자는 Hyper-v 호스트가 보호 된 호스트로 실행 될 수 있는지 확인 해야 합니다. 하나 이상의 보호 된 호스트에서 다음 단계를 완료 합니다.

1. Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능을 아직 설치 하지 않은 경우 다음 명령을 사용 하 여 설치 합니다.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2. HGS 서버에서 Hyper-v 호스트가 HGS DNS 이름을 확인 하 고 포트 80 (또는 HTTPS를 설정한 경우 443)에 연결할 네트워크 연결을 사용할 수 있는지 확인 합니다.

3. 호스트의 키 보호 및 증명 Url을 구성 합니다.

    - **Windows powershell을 통해**: 관리자 권한 windows powershell 콘솔에서 다음 명령을 실행 하 여 키 보호 및 증명 url을 구성할 수 있습니다. &lt;FQDN&gt;의 경우 HGS 클러스터의 FQDN (정규화 된 도메인 이름) (예: HgsServer)을 사용 하거나, hgs 관리자에 게 hgs 서버에서 cmdlet을 실행 하 여 url을 검색 하도록 요청 합니다.

        ```PowerShell
        Set-HgsClientConfiguration -AttestationServerUrl 'http://<FQDN>/Attestation' -KeyProtectionServerUrl 'http://<FQDN>/KeyProtection'
         ```

        대체 HGS 서버를 구성 하려면이 명령을 반복 하 고 키 보호 및 증명 서비스에 대 한 대체 (fallback) Url을 지정 합니다. 자세한 내용은 [대체 구성](guarded-fabric-manage-branch-office.md#fallback-configuration)을 참조 하세요.

    - **Vmm을 통해**: Vmm (System Center 2016-Virtual Machine Manager)을 사용 하는 경우 Vmm에서 증명 및 키 보호 url을 구성할 수 있습니다. 자세한 내용은 **VMM에서 보호 된 호스트 프로 비전**에서 [전역 HGS 설정 구성](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts#configure-global-hgs-settings) 을 참조 하세요.

    >**참고**
    > - Hgs 관리자가 [hgs 서버에서 HTTPS를 사용 하도록 설정한](guarded-fabric-configure-hgs-https.md)경우 `https://`를 사용 하 여 url을 시작 합니다.
    > - Hgs 관리자가 HGS 서버에서 HTTPS를 사용 하도록 설정 하 고 자체 서명 된 인증서를 사용 하는 경우 모든 호스트의 신뢰할 수 있는 루트 인증 기관 저장소로 인증서를 가져와야 합니다. 이렇게 하려면 각 호스트에서 다음 명령을 실행 합니다.
       ```PowerShell
       Import-Certificate -FilePath "C:\temp\HttpsCertificate.cer" -CertStoreLocation Cert:\LocalMachine\Root
       ```
    > - HTTPS를 사용 하도록 HGS 클라이언트를 구성 하 고 TLS 1.0을 사용 하지 않도록 설정한 경우 [최신 tls 지침](guarded-fabric-troubleshoot-hosts.md#modern-tls) 을 참조 하세요.

4. 호스트에서 증명 시도를 시작 하 고 증명 상태를 확인 하려면 다음 명령을 실행 합니다.

    ```powershell
    Get-HgsClientConfiguration
    ```

    명령의 출력은 호스트가 증명을 통과 했으며 이제 보호 되는지 여부를 나타냅니다. `IsHostGuarded`에서 **True**를 반환 하지 않는 경우에는 HGS 진단 도구인 [HgsTrace](https://technet.microsoft.com/library/mt718831.aspx)를 실행 하 여 조사할 수 있습니다. 진단을 실행 하려면 호스트의 관리자 권한 Windows PowerShell 프롬프트에서 다음 명령을 입력 합니다.

    ```powershell
    Get-HgsTrace -RunDiagnostics -Detailed
    ```

    > [!IMPORTANT]
    > Windows Server 2019 또는 Windows 10 버전 1809을 사용 중이 고 코드 무결성 정책을 사용 하는 경우 `Get-HgsTrace` **코드 무결성 정책 활성** 진단에 대 한 오류를 반환 합니다.
    > 오류가 유일한 진단 인 경우에는이 결과를 무시 해도 안전 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

## <a name="see-also"></a>참고 항목

- [HGS (호스트 보호 서비스) 배포](guarded-fabric-deploying-hgs-overview.md)
- [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

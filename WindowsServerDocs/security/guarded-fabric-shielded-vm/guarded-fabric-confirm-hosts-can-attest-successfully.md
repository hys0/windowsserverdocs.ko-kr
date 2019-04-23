---
title: 보호 된 호스트 증명할 수 확인
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7485796b-b840-4678-9b33-89e9710fbbc7
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 02/05/2019
ms.openlocfilehash: 6b67208176b426f52d3c5106f8de09ad334d3b01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829534"
---
# <a name="confirm-guarded-hosts-can-attest"></a>보호 된 호스트 증명할 수 확인 

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019


패브릭 관리자는 Hyper-v 호스트 보호 된 호스트로 실행 될 수 있는지 확인 해야 합니다. 하나 이상의 보호 된 호스트에서 다음 단계를 완료 합니다.

1.  하지 이미 설치한 경우 Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능, 다음 명령을 사용 하 여 설치 합니다.

        Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart

2.  Hyper-v 호스트가 HGS DNS 이름을 확인할 수 있고 네트워크에 연결 포트 80 (또는 HTTPS를 설정한 경우 443)에 연결할 HGS 서버에 있는지 확인 합니다.

2.  호스트의 키 보호 및 증명 Url을 구성 합니다.

    - **Windows PowerShell을 통해**: 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 하 여 키 보호 및 증명 Url을 구성할 수 있습니다. 에 대 한 &lt;FQDN&gt;를 완전히 정규화 된 도메인 이름 (FQDN) HGS 클러스터를 사용 하 여 (예를 들어 hgs.bastion.local 실행 HGS 관리자에 게 문의 하거나를 **Get HgsServer** 검색할 HGS 서버에는 cmdlet를 Url)입니다.

        `Set-HgsClientConfiguration -AttestationServerUrl 'http://<FQDN>/Attestation' -KeyProtectionServerUrl 'http://<FQDN>/KeyProtection'`

        대체 HGS 서버를 구성 하려면이 명령을 반복 하 고 증명 및 키 보호 서비스에 대 한 대체 (fallback) Url을 지정 합니다. 자세한 내용은 [대체 (fallback) 구성](guarded-fabric-manage-branch-office.md#fallback-configuration)합니다. 

    - **VMM을 통해**: System Center 2016-Virtual Machine Manager (VMM)를 사용 하는 경우 VMM에서 증명 및 키 보호 Url을 구성할 수 있습니다. 세부 정보를 참조 하세요 [전역 HGS 설정 구성](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts#configure-global-hgs-settings) 에 **프로 비전에서에서 보호 된 호스트 VMM**합니다.
    
    >**참고**
    > - 경우 HGS 관리자 [HGS 서버에 HTTPS를 활성화](guarded-fabric-configure-hgs-https.md)를 사용 하 여 Url을 시작 `https://`합니다.
    > - HGS 관리자 HGS 서버에 HTTPS를 활성화 하는 자체 서명 된 인증서를 사용 하는 경우에 모든 호스트에 있는 신뢰할 수 있는 루트 인증 기관 저장소에 인증서를 가져올 해야 합니다. 이렇게 하려면 각 호스트에서 다음 명령을 실행 합니다.<br>
        `Import-Certificate -FilePath "C:\temp\HttpsCertificate.cer" -CertStoreLocation Cert:\LocalMachine\Root`
    
3.  호스트에서 증명 시도 시작 하 고 증명 상태를 확인 하는 다음 명령을 실행 합니다.

        Get-HgsClientConfiguration

    명령의 출력 호스트 증명을 전달 하 고는 이제 보호 하는지 여부를 나타냅니다. 하는 경우 `IsHostGuarded` 반환 하지 않는 **True**, HGS 진단 도구를 실행할 수 있습니다 [Get HgsTrace](https://technet.microsoft.com/library/mt718831.aspx)를 조사 합니다. 진단 유틸리티를 실행 하려면 호스트에서 관리자 권한 Windows PowerShell 프롬프트에서 다음 명령을 입력 합니다.

        Get-HgsTrace -RunDiagnostics -Detailed

    > [!IMPORTANT]
    > Windows Server 2019 또는 Windows 10 버전 1809 사용 하는 코드 무결성 정책을 사용 하는 경우 `Get-HgsTrace` 에 대 한 오류를 반환할 수 있습니다 합니다 **코드 무결성 정책 Active** 진단 합니다.
    > 이 결과 실패 한 진단 하는 것이 상태일 때에 안전 하 게 무시할 수 있습니다.

## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[보호 된 Vm 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

## <a name="see-also"></a>참조

- [호스트 보호 서비스 (HGS) 배포](guarded-fabric-deploying-hgs-overview.md)
- [보호 된 Vm 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)


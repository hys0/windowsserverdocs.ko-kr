---
title: HGS에 필요한 TPM 모드 정보 캡처
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 915b1338-5085-481b-8904-75d29e609e93
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 04/01/2019
ms.openlocfilehash: ba67cb80a405cd1c6d368a52798e3dec4d9861cb
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371376"
---
# <a name="authorize-guarded-hosts-using-tpm-based-attestation"></a>TPM 기반 증명을 사용 하 여 보호 된 호스트에 권한 부여

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

TPM 모드는 TPM 식별자 (플랫폼 식별자 또는 인증 키 \[EKpub\])를 사용 하 여 특정 호스트가 "보호"로 인증 되었는지 여부를 확인 하기 시작 합니다. 이 증명 모드는 보안 부팅 및 코드 무결성 측정을 사용 하 여 지정 된 Hyper-v 호스트가 정상 상태이 고 신뢰할 수 있는 코드만 실행 되는지 확인 합니다. 증명에서 정상이 고 정상이 아닌 것을 이해 하려면 다음 아티팩트를 캡처해야 합니다.

1.  TPM 식별자 (EKpub)

    -  이 정보는 각 Hyper-v 호스트에 대해 고유 합니다.

2.  TPM 기준 (부팅 측정)

    -  이는 동일한 하드웨어 클래스에서 실행 되는 모든 Hyper-v 호스트에 적용할 수 있습니다.

3.  코드 무결성 정책 (허용 되는 이진 파일의 허용 목록)

    -  이는 일반적인 하드웨어 및 소프트웨어를 공유 하는 모든 Hyper-v 호스트에 적용 됩니다.

데이터 센터 내에서 각각의 고유한 Hyper-v 하드웨어 구성 클래스를 대표 하는 "참조 호스트"에서 기준 및 CI 정책을 캡처하는 것이 좋습니다. Windows Server 버전 1709부터 샘플 CI 정책은 C:\Windows\schemas\CodeIntegrity\ExamplePolicies.에 포함 되어 있습니다. 

## <a name="versioned-attestation-policies"></a>버전 증명 정책

Windows Server 2019에서는 EKPub를 HGS에 추가 하기 위해 TPM 인증서가 있어야 하는 *v2 증명*이라는 증명에 대 한 새로운 방법을 소개 합니다. Windows Server 2016에서 사용 되는 v1 증명 방법을 사용 하면 HgsAttestationTpmHost 또는 기타 TPM 증명 cmdlet을 실행 하 여 아티팩트를 캡처할 때-Force 플래그를 지정 하 여이 안전 검사를 재정의할 수 있습니다. Windows Server 2019부터 v2 증명은 기본적으로 사용 되며, 인증서 없이 TPM을 등록 해야 하는 경우 HgsAttestationTpmHost를 실행 하면-PolicyVersion v1 플래그를 지정 해야 합니다. -Force 플래그는 v2 증명에서 작동 하지 않습니다. 

호스트는 모든 아티팩트 (EKPub + TPM 기준 + CI 정책)에서 동일한 증명 버전을 사용 하는 경우에만 증명할 수 있습니다. V2 증명을 먼저 시도한 후 실패 하면 v1 증명이 사용 됩니다. 즉, v1 증명을 사용 하 여 TPM 식별자를 등록 해야 하는 경우에는 TPM 기준을 캡처하고 CI 정책을 만들 때 v1 증명을 사용 하도록-PolicyVersion v1 플래그를 지정 해야 합니다. V2 증명을 사용 하 여 TPM 기준 및 CI 정책을 만든 다음 나중에 TPM 인증서 없이 보호 된 호스트를 추가 해야 하는 경우-PolicyVersion v1 플래그를 사용 하 여 각 아티팩트를 다시 만들어야 합니다. 

## <a name="capture-the-tpm-identifier-platform-identifier-or-ekpub-for-each-host"></a>각 호스트에 대 한 TPM 식별자 (플랫폼 식별자 또는 EKpub)를 캡처합니다.

1.  패브릭 도메인에서 각 호스트의 TPM을 사용할 준비가 되었는지 확인 합니다. 즉, TPM이 초기화 되 고 소유권이 획득 됩니다. Tpm 관리 콘솔 (services.msc)을 열거나 관리자 권한 Windows PowerShell 창 **에서 tpm을 실행 하** 여 tpm의 상태를 확인할 수 있습니다. TPM이 **준비** 상태가 아닌 경우 초기화 하 고 소유권을 설정 해야 합니다. TPM 관리 콘솔에서 또는 **Tpm 초기화**를 실행 하 여이 작업을 수행할 수 있습니다.

2.  보호 된 각 호스트에서 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 하 여 해당 EKpub를 가져옵니다. `<HostName>`의 경우 고유한 호스트 이름을이 호스트를 식별 하는 데 적합 한 것으로 대체 합니다. 즉, 해당 호스트 이름이 나 패브릭 인벤토리 서비스에서 사용 하는 이름 (있는 경우)이 될 수 있습니다. 편의를 위해 호스트 이름을 사용 하 여 출력 파일의 이름을로 합니다.

    ```powershell
    (Get-PlatformIdentifier -Name '<HostName>').InnerXml | Out-file <Path><HostName>.xml -Encoding UTF8
    ```
3.  보호 된 호스트가 될 각 호스트에 대해 위의 단계를 반복 하 여 각 XML 파일에 고유한 이름을 지정 해야 합니다.

4.  결과 XML 파일을 HGS 관리자에 게 제공 합니다.

5.  HGS 도메인에서, HGS 서버에서 관리자 권한 Windows PowerShell 콘솔을 열고 다음 명령을 실행 합니다. 각 XML 파일에 대해이 명령을 반복 합니다.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > EKCert (신뢰할 수 없는 인증 키 인증서)와 관련 된 TPM 식별자를 추가할 때 오류가 발생 하는 경우 [신뢰할 수 있는 tpm 루트 인증서가](guarded-fabric-install-trusted-tpm-root-certificates.md) HGS 노드에 추가 되었는지 확인 합니다.
    > 또한 일부 TPM 공급 업체는 EKCerts을 사용 하지 않습니다.
    > 메모장과 같은 편집기에서 XML 파일을 열고 EKCert를 찾지 못했음을 나타내는 오류 메시지를 확인 하 여 EKCert이 누락 되었는지 확인할 수 있습니다.
    > 이 경우 컴퓨터의 TPM이 인증 된 것을 신뢰 하는 경우 `-Force` 매개 변수를 사용 하 여 호스트 식별자를 HGS에 추가할 수 있습니다. Windows Server 2019에서는 `-Force`사용 하는 경우에도 `-PolicyVersion v1` 매개 변수를 사용 해야 합니다. 그러면 Windows Server 2016 동작과 일치 하는 정책이 생성 되며, CI 정책 및 TPM 기준도 등록할 때 `-PolicyVersion v1`을 사용 해야 합니다.

## <a name="create-and-apply-a-code-integrity-policy"></a>코드 무결성 정책 만들기 및 적용

코드 무결성 정책을 사용 하면 호스트에서 실행 하는 데 신뢰할 수 있는 실행 파일만 실행할 수 있습니다. 신뢰할 수 있는 실행 파일 외부의 맬웨어 및 기타 실행 파일을 실행할 수 없습니다.

보호 된 각 호스트에는 TPM 모드에서 보호 된 Vm을 실행 하기 위해 코드 무결성 정책이 적용 되어 있어야 합니다. HGS에 추가 하 여 신뢰할 수 있는 정확한 코드 무결성 정책을 지정 합니다. 정책을 적용 하거나, 정책을 준수 하지 않는 소프트웨어를 차단 하거나, 정책에 정의 되지 않은 소프트웨어가 실행 될 때 이벤트 기록을 수행 하도록 코드 무결성 정책을 구성할 수 있습니다. 

Windows Server 버전 1709부터 샘플 코드 무결성 정책은 Windows에 C:\Windows\schemas\CodeIntegrity\ExamplePolicies.에 포함 되어 있습니다. Windows Server에는 두 가지 정책이 권장 됩니다.

- **Allowmicrosoft**: microsoft에서 서명한 모든 파일을 허용 합니다. 이 정책은 SQL 또는 Exchange와 같은 서버 응용 프로그램에 권장 되며, Microsoft에서 게시 한 에이전트가 서버를 모니터링 하는 경우에 권장 됩니다.
- **DefaultWindows_Enforced**: Windows에서 제공 된 파일만 허용 하 고 Office와 같이 Microsoft에서 릴리스된 다른 응용 프로그램을 허용 하지 않습니다. 이 정책은 Hyper-v와 같은 기본 제공 서버 역할 및 기능만 실행 하는 서버에 권장 됩니다. 

먼저 감사 (로깅) 모드에서 CI 정책을 만들어 무엇이 누락 되었는지 확인 한 다음 호스트 프로덕션 워크 로드에 대 한 정책을 적용 하는 것이 좋습니다. 

[새-cipolicy](https://docs.microsoft.com/powershell/module/configci/new-cipolicy?view=win10-ps) cmdlet을 사용 하 여 사용자 고유의 코드 무결성 정책을 생성 하는 경우 사용할 규칙 수준을 결정 해야 합니다. **해시**에 대 한 대체 (fallback)를 사용 하는 기본 수준의 **게시자** 를 사용 하는 것이 좋습니다 .이를 통해 대부분의 디지털 서명 된 소프트웨어는 CI 정책을 변경 하지 않고 업데이트
CI 정책을 변경 하지 않고 동일한 게시자가 작성 한 새 소프트웨어를 서버에 설치할 수도 있습니다.
디지털 서명 되지 않은 실행 파일은 해시 됩니다. 이러한 파일에 대 한 업데이트를 수행 하려면 새 CI 정책을 만들어야 합니다.
사용 가능한 CI 정책 규칙 수준에 대 한 자세한 내용은 [코드 무결성 정책 배포: 정책 규칙 및 파일 규칙](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create#windows-defender-application-control-policy-rules) 및 cmdlet 도움말을 참조 하세요.

1.  참조 호스트에서 새 코드 무결성 정책을 생성 합니다. 다음 명령은 **Hash**에 대 한 대체 (fallback)를 사용 하 여 **게시자** 수준에서 정책을 만듭니다. 그런 다음 XML 파일을 Windows 및 HGS가 CI 정책을 적용 하 고 측정 해야 하는 이진 파일 형식으로 변환 합니다.

    ```powershell
    New-CIPolicy -Level Publisher -Fallback Hash -FilePath 'C:\temp\HW1CodeIntegrity.xml' -UserPEs

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity.p7b'
    ```

    >[!NOTE]
    >위의 명령은 감사 모드 에서만 CI 정책을 만듭니다. 호스트에서 권한이 없는 이진 파일이 실행 되는 것을 차단 하지 않습니다. 프로덕션 에서만 적용 되는 정책을 사용 해야 합니다.

2.  쉽게 찾을 수 있는 코드 무결성 정책 파일 (XML 파일)을 유지 합니다. 나중에이 파일을 편집 하 여 CI 정책을 적용 하거나 나중에 시스템에 적용 되는 업데이트의 변경 내용을 병합 해야 합니다.

3.  참조 호스트에 CI 정책을 적용 합니다.

    1.  다음 명령을 실행 하 여 CI 정책을 사용 하도록 컴퓨터를 구성 합니다. [그룹 정책](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy) 또는 [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/guarded-deploy-host?view=sc-vmm-2019#manage-and-deploy-code-integrity-policies-with-vmm)를 사용 하 여 CI 정책을 배포할 수도 있습니다.

        ```powershell
        Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
        ```

    2.  호스트를 다시 시작 하 여 정책을 적용 합니다.

3.  일반적인 워크 로드를 실행 하 여 코드 무결성 정책을 테스트 합니다. 여기에는 실행 중인 Vm, 패브릭 관리 에이전트, 백업 에이전트 또는 컴퓨터의 문제 해결 도구가 포함 될 수 있습니다. 코드 무결성 위반이 있는지 확인 하 고 필요한 경우 CI 정책을 업데이트 합니다.

4.  업데이트 된 CI 정책 XML 파일에 대해 다음 명령을 실행 하 여 CI 정책을 적용 모드로 변경 합니다.

    ```powershell
    Set-RuleOption -FilePath 'C:\temp\HW1CodeIntegrity.xml' -Option 3 -Delete

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity_enforced.p7b'
    ```

5.  다음 명령을 사용 하 여 모든 호스트 (동일한 하드웨어 및 소프트웨어 구성)에 CI 정책을 적용 합니다.

    ```powershell
    Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
    
    Restart-Computer
    ```

    >[!NOTE]
    >CI 정책을 호스트에 적용 하 고 이러한 컴퓨터에서 소프트웨어를 업데이트할 때 주의 해야 합니다. CI 정책과 호환 되지 않는 모든 커널 모드 드라이버를 사용 하면 컴퓨터가 시작 되지 않을 수 있습니다. 

6.  HGS 관리자에 게 이진 파일 (이 예제에서는 HW1CodeIntegrity\_)을 제공 합니다.

7.  HGS 도메인에서 코드 무결성 정책을 HGS 서버에 복사 하 고 다음 명령을 실행 합니다.

    `<PolicyName>`의 경우 적용 되는 호스트의 유형을 설명 하는 CI 정책 이름을 지정 합니다. 컴퓨터의 제조업체/모델과 해당 컴퓨터에서 실행 되는 특수 소프트웨어 구성의 이름을 지정 하는 것이 가장 좋습니다.<br>`<Path>`의 경우 코드 무결성 정책의 경로와 파일 이름을 지정 합니다.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

## <a name="capture-the-tpm-baseline-for-each-unique-class-of-hardware"></a>고유한 각 하드웨어 클래스에 대 한 TPM 기준선 캡처

데이터 센터 패브릭의 고유한 각 하드웨어 클래스에 대해 TPM 기준이 필요 합니다. "참조 호스트"를 다시 사용 합니다. 

1. 참조 호스트에서 Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능이 설치 되어 있는지 확인 합니다.

    >[!WARNING]
    >호스트 보호자 Hyper-v 지원 기능을 사용 하면 일부 장치와 호환 되지 않을 수 있는 코드 무결성을 가상화 기반으로 보호할 수 있습니다. 이 기능을 사용 하도록 설정 하기 전에 랩에서이 구성을 테스트 하는 것이 좋습니다. 이렇게 하지 않으면 데이터 손실이나 블루 스크린 오류(중지 오류라고도 함)를 비롯한 예기치 않은 실패가 발생할 수 있습니다.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```
        
2. 기준 정책을 캡처하려면 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 합니다.
        
    ```powershell
    Get-HgsAttestationBaselinePolicy -Path 'HWConfig1.tcglog'
    ```

    >[!NOTE]
    >참조 호스트에서 보안 부팅을 사용 하지 않거나, IOMMU가 있거나, 가상화 기반 보안이 활성화 되 고 실행 되거나, 코드 무결성 정책이 적용 되지 않은 경우 **-skipvalidation** 플래그를 사용 해야 합니다. 이러한 유효성 검사는 호스트에서 보호 된 VM을 실행 하는 최소 요구 사항을 인식 하도록 설계 되었습니다. -SkipValidation 플래그를 사용 해도 cmdlet의 출력이 변경 되지 않습니다. 단지 오류가 silences.

3.  HGS 관리자에 게 TPM 기준 (TCGlog 파일)을 제공 합니다.

4.  HGS 도메인에서 TCGlog 파일을 HGS 서버에 복사 하 고 다음 명령을 실행 합니다. 일반적으로 정책 이름은 표시 하는 하드웨어 클래스 (예: "제조업체 모델 수정 버전") 다음에 표시 됩니다.

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [증명 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

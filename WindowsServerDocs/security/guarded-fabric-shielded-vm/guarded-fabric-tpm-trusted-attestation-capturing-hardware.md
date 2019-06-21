---
title: HGS에 필요한 TPM 모드 정보 캡처
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 915b1338-5085-481b-8904-75d29e609e93
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 04/01/2019
ms.openlocfilehash: 24d81e3d2c31b3493563f3f3e2ab3f92afff2c06
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284135"
---
# <a name="authorize-guarded-hosts-using-tpm-based-attestation"></a>TPM 기반 증명을 사용 하 여 보호 된 호스트를 권한 부여

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

TPM 모드 TPM 식별자를 사용 하 여 (플랫폼 식별자 또는 인증 키를 라고도 \[EKpub\]) 특정 호스트 "보호 합니다." 대로 권한이 있는지 확인 하려면 이 증명 모드는 보안 부팅 및 코드 무결성 측정을 사용 하 여 지정된 된 Hyper-v 호스트의 상태가 정상 이며 신뢰할 수 있는 코드만 실행 되도록 합니다. 이란 무엇 이며 정상이 아님을 이해 하는 증명에 대 한 순서 대로 다음 아티팩트를 캡처해야 합니다.

1.  TPM 식별자 (EKpub)

    -  이 정보는 각 Hyper-v 호스트에 고유한

2.  TPM 기준 (부팅 측정값이)

    -  동일한 클래스의 하드웨어에서 실행 되는 모든 Hyper-v 호스트에 적용 됩니다.

3.  코드 무결성 정책 (허용 된 이진 파일의 화이트 리스트)

    -  일반적인 하드웨어 및 소프트웨어를 공유 하는 모든 Hyper-v 호스트에 적용 됩니다.

기준 및 CI 정책 "참조 호스트"에서 캡처하는 것이 좋습니다 데이터 센터 내의 Hyper-v 하드웨어 구성의 각 고유 클래스의 특징입니다. Windows Server 버전 1709 부터는 샘플 CI 정책 C:\Windows\schemas\CodeIntegrity\ExamplePolicies 포함 됩니다. 

## <a name="versioned-attestation-policies"></a>버전이 지정 된 증명 정책

Windows Server 2019 증명, 호출에 대 한 새로운 방법이 도입 되었습니다 *v2 증명*TPM 인증서 EKPub HGS를 추가 하려면 있는 여야 합니다. Windows Server 2016에서 사용 되는 v1 증명 메서드를 사용할 수를 지정 하 여이 안전 검사를 재정의할 수 있습니다 아티팩트를 캡처할 추가 HgsAttestationTpmHost 또는 다른 TPM 증명 cmdlet을 실행 하면-Force 플래그입니다. Windows Server 2019 부터는 v2 증명 기본적으로 사용 되 고 인증서 없이 TPM 등록 해야 하는 경우 추가 HgsAttestationTpmHost를 실행할 때-있습니다 v1 플래그를 지정 해야 합니다. -Force 플래그 v2 증명을 사용 하 여 작동 하지 않습니다. 

모든 경우에 호스트를 증명할 수 아티팩트 (EKPub + TPM 기준 + CI 정책) 증명의 동일한 버전을 사용 합니다. V2 증명 먼저 시도 됩니다 하 고 실패 하는 하는 경우 v1 증명을 사용 합니다. 즉, 또한 TPM 기준선을 캡처하고 CI 정책을 만드는 경우 v1 증명을 사용 하려면-있습니다 v1 플래그를 지정 해야 하는 v1 증명을 사용 하 여 TPM 식별자를 등록 해야 할 경우. V2 증명을 사용 하 여 TPM 기준 및 CI 정책을 만든 다음 나중에 추가 해야 TPM 인증서 없이도 보호 된 호스트를 다시-있습니다 v1 플래그를 사용 하 여 각 아티팩트를 만드는 데 필요 합니다. 

## <a name="capture-the-tpm-identifier-platform-identifier-or-ekpub-for-each-host"></a>각 호스트에 대 한 TPM 식별자 (플랫폼 식별자 또는 EKpub) 캡처

1.  Fabric 도메인에 각 호스트의 TPM을 사용 하 여 준비가 되었다고-즉, TPM이 초기화 하 고 소유권을 가져온 있는지 확인 합니다. TPM Management Console (tpm.msc)를 열어 또는 실행 하 여 TPM의 상태를 확인할 수 있습니다 **Get Tpm** 관리자 권한 Windows PowerShell 창에서. TPM에 없는 경우는 **준비** 상태를 초기화 하 고 소유권을 설정 해야 합니다. TPM 관리 콘솔에서 또는 실행 하 여이 수행할 수 있습니다 **Initialize Tpm**합니다.

2.  각 보호 된 호스트에서 해당 EKpub를 가져오려면 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 합니다. 에 대 한 `<HostName>`,이 호스트를 식별 하는 데 적합 한 항목을 사용 하 여 고유한 호스트 이름으로 대체-이 해당 호스트 또는 패브릭 인벤토리 서비스 (있는 경우) 사용 하는 이름 수 있습니다. 편의 위해 호스트의 이름을 사용 하 여 출력 파일을 이름을 지정 합니다.

    ```powershell
    (Get-PlatformIdentifier -Name '<HostName>').InnerXml | Out-file <Path><HostName>.xml -Encoding UTF8
    ```
3.  각 XML 파일에 고유한 이름을 지정 하 여 보호 된 호스트 될 각 호스트에 대해 위의 단계를 반복 합니다.

4.  생성 된 XML 파일을 HGS 관리자에 게 제공 합니다.

5.  HGS 도메인에서 HGS 서버에서 관리자 권한 Windows PowerShell 콘솔을 열고 다음 명령을 실행 합니다. 각 XML 파일에 대해 명령을 반복 합니다.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > 신뢰할 수 없는 인증 키 인증서 (EKCert)에 대 한 TPM 식별자를 추가 하는 경우 오류가 발생 하면 확인 합니다 [TPM 루트 인증서가 추가 되어 신뢰할 수 있는](guarded-fabric-install-trusted-tpm-root-certificates.md) HGS 노드에 있습니다.
    > 또한 일부 TPM 공급 업체는 되도록 EKCerts를 사용 하지 마세요.
    > 메모장과 같은 편집기에서 XML 파일을 열어 EKCert 없습니다 및 찾을 수 없는 EKCert를 나타내는 오류 메시지를 확인 하는 경우를 확인할 수 있습니다.
    > 이 경우 컴퓨터의 TPM은 인증에 사용할 수 있습니다를 신뢰 하 경우는 `-Force` 호스트 식별자를 HGS에 추가할 매개 변수입니다. Windows Server 2019에도 사용 해야 합니다 `-PolicyVersion v1` 매개 변수를 사용할 때 `-Force`합니다. Windows Server 2016 동작과 일치 정책을 만듭니다.이 사용 하 여 필요가 `-PolicyVersion v1` CI 정책 및 TPM 기준도 등록할 때.

## <a name="create-and-apply-a-code-integrity-policy"></a>코드 무결성 정책 만들기 및 적용

코드 무결성 정책을 사용 하면 호스트에서 실행 되도록 신뢰 실행 파일만 실행할 수 있습니다. 맬웨어 및 기타 실행 파일 외부의 신뢰할 수 있는 실행 파일 실행에서 차단 됩니다.

보호 된 각 호스트에 TPM 모드에서 보호 된 Vm을 실행 하기 위해 적용 되는 코드 무결성 정책이 있어야 합니다. HGS를 추가 하 여 신뢰 정확한 코드 무결성 정책을 지정할 수 있습니다. 코드 무결성 정책 (정책에 정의 되지 않은 소프트웨어 실행 될 때 이벤트 로그)를 차단 하는 정책을 준수 하지 않거나 단순히 감사 하는 모든 소프트웨어 정책 적용을 구성할 수 있습니다. 

Windows Server 버전 1709부터 샘플 코드 무결성 정책을 Windows C:\Windows\schemas\CodeIntegrity\ExamplePolicies에 포함 되어 있습니다. Windows Server에 대 한 정책 두 개를 사용 하는 것이 좋습니다.

- **AllowMicrosoft**: Microsoft에서 서명 하는 모든 파일을 허용 합니다. 이 정책을 SQL 또는 Exchange와 같은 서버 응용 프로그램에 대 한 권장 또는 Microsoft에서 게시 하는 에이전트에서 서버를 모니터링 하는 경우.
- **DefaultWindows_Enforced**: Windows에서 제공 하 고 Office 등 Microsoft에서 릴리스한 다른 응용 프로그램을 허용 하지 않습니다 하는 파일에만 허용 합니다. 이 정책은 기본 제공 서버 역할 및 Hyper-v와 같은 기능을 실행 하는 서버에 권장 됩니다. 

먼저 CI 정책 항목을 누락 하는 경우를 확인 하려면 (로깅) 감사 모드에서 만든 다음 프로덕션 워크 로드를 호스트에 대 한 정책을 적용할 것이 좋습니다. 

사용 하는 경우는 [새로 만들기-CIPolicy](https://docs.microsoft.com/powershell/module/configci/new-cipolicy?view=win10-ps) 직접 생성 하는 cmdlet 코드 무결성 정책, 해야 사용 하는 규칙 수준을 결정 합니다. 기본 수준의 것이 좋습니다 **게시자** 대체를 사용 하 여 **해시**, CI 정책을 변경 하지 않고 업데이트할 소프트웨어 로그온을 허용 하는 디지털 가장 합니다.
또한 동일한 게시자가 작성 한 새 소프트웨어 CI 정책을 변경 하지 않고 서버에 설치할 수 있습니다.
디지털 서명 되지 않은 실행 파일 해시 됩니다. 즉 이러한 파일에 대 한 업데이트를 사용 해야 새 CI 정책을 만들 수 있습니다.
사용 가능한 CI 정책 규칙 수준에 대 한 자세한 내용은 참조 하세요. [코드 무결성 정책을 배포 합니다: 정책 규칙 및 파일 규칙](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create#windows-defender-application-control-policy-rules) 및 cmdlet 도움말입니다.

1.  참조 호스트에 새 코드 무결성 정책을 생성 합니다. 다음 명령에서 정책 만들기는 **게시자** 대체를 사용 하 여 수준 **해시**합니다. 다음 XML 파일을 적용 하 고 CI 정책의 각각 측정 해야 하는 Windows 및 HGS 이진 파일 형식으로 변환 합니다.

    ```powershell
    New-CIPolicy -Level Publisher -Fallback Hash -FilePath 'C:\temp\HW1CodeIntegrity.xml' -UserPEs

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity.p7b'
    ```

    >[!NOTE]
    >위의 명령은 감사 모드 에서만 CI 정책을 만듭니다. 호스트에서 실행 되는 허가 되지 않은 이진 파일을 차단 하지는 않습니다. 프로덕션 환경에서 강제 적용된 정책만 사용 해야 합니다.

2.  쉽게 찾을 수 있는 코드 무결성 정책 파일 (XML 파일)를 유지 합니다. CI 정책 또는 병합에 시스템에 대 한 향후 업데이트에서 변경 내용 적용 하는 나중에이 파일을 편집 해야 합니다.

3.  CI 정책을 참조 호스트에 적용 됩니다.

    1.  CI 정책을 사용 하 여 컴퓨터를 구성 하려면 다음 명령을 실행 합니다. 사용 하 여 CI 정책을 배포할 수도 있습니다 [그룹 정책](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy) 하거나 [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/guarded-deploy-host?view=sc-vmm-2019#manage-and-deploy-code-integrity-policies-with-vmm)합니다.

        ```powershell
        Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
        ```

    2.  정책을 적용 하려면 호스트를 다시 시작 합니다.

3.  일반적인 워크 로드를 실행 하 여 코드 무결성 정책을 테스트 합니다. 이 실행 중인 Vm에 모든 패브릭 관리 에이전트, 백업 에이전트 또는 컴퓨터에 도구 문제 해결에 포함할 수 있습니다. 코드 무결성 위반 사항이 있는지 확인 하 고 필요한 경우 CI 정책 업데이트 합니다.

4.  업데이트 된 CI 정책 XML 파일에 대해 다음 명령을 실행 하 여 CI 정책 적용된 모드로 변경 합니다.

    ```powershell
    Set-RuleOption -FilePath 'C:\temp\HW1CodeIntegrity.xml' -Option 3 -Delete

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity_enforced.p7b'
    ```

5.  다음 명령을 사용 하 여 모든 호스트 (동일한 하드웨어 및 소프트웨어 구성 사용)에 CI 정책에 적용 됩니다.

    ```powershell
    Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
    
    Restart-Computer
    ```

    >[!NOTE]
    >호스트에 CI 정책을 적용 하는 경우 및이 컴퓨터에 소프트웨어를 업데이트 하는 경우 주의 해야 합니다. CI 정책을 준수 하는 모든 커널 모드 드라이버를 컴퓨터를 못할 수 있습니다. 

6.  이진 파일 제공 (이 예제에서는 HW1CodeIntegrity\_enforced.p7b) HGS 관리자에 게 합니다.

7.  HGS 도메인에서 코드 무결성 정책을 HGS 서버에 복사한 다음 명령을 실행 합니다.

    에 대 한 `<PolicyName>`를 적용 하는 호스트의 형식을 설명 하는 CI 정책에 대 한 이름을 지정 합니다. 실행 중인 모든 특별 한 소프트웨어가 구성 및 컴퓨터의 메이커/모델 후 이름을 지정 하는 것이 좋습니다.<br>에 대 한 `<Path>`, 경로 및 코드 무결성 정책의 파일 이름을 지정 합니다.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

## <a name="capture-the-tpm-baseline-for-each-unique-class-of-hardware"></a>하드웨어의 각 고유 클래스에 대 한 TPM 기준 캡처

TPM 기본 하드웨어에 데이터 센터 패브릭의 각 고유 클래스에 대 한 필요합니다. "참조 호스트"를 다시 사용 합니다. 

1. 참조 호스트에 Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능 설치 되어 있는지 확인 합니다.

    >[!WARNING]
    >호스트 보호 Hyper-v 지원 기능에는 일부 장치와 호환 되지 않을 수 있는 코드 무결성 보호를 가상화 기반 수 있습니다. 이 기능을 활성화 하기 전에 랩에이 구성을 테스트 하는 것이 좋습니다. 이렇게 하지 않으면 데이터 손실이나 블루 스크린 오류(중지 오류라고도 함)를 비롯한 예기치 않은 실패가 발생할 수 있습니다.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```
        
2. 기본 정책을 캡처하려면 승격된 된 Windows PowerShell 콘솔에서 다음 명령을 실행 합니다.
        
    ```powershell
    Get-HgsAttestationBaselinePolicy -Path 'HWConfig1.tcglog'
    ```

    >[!NOTE]
    >사용 해야 합니다는 **-SkipValidation** 존재는 IOMMU "," 가상화 기반 보안 "및" 실행 "또는" 적용 코드 무결성 정책을 참조 호스트에서 보안 부팅 되지 않은 경우 플래그를 사용할 수 있습니다. 이러한 유효성 검사는 보호 된 VM 호스트에서 실행의 최소 요구 사항을 알려 주기 위해 설계 되었습니다. -SkipValidation 플래그를 사용 하 여 cmdlet의 출력을 변경 되지 않습니다. 단순히 오류를 지정 합니다.

3.  HGS 관리자에 게 TPM 기준 (TCGlog 파일)를 제공 합니다.

4.  HGS 도메인에서 HGS 서버에 TCGlog 파일을 복사한 다음 명령을 실행 합니다. 일반적으로 (예: "제조업체 모델 버전") 나타냅니다 하드웨어 클래스 뒤 정책을 이름을 있습니다.

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [증명 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

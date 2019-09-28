---
title: TPM에서 신뢰할 수 있는 증명에 대 한 호스트 정보 추가
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: 35efca71278c288189819d6c9fc49ba8195d18a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386825"
---
>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

### <a name="add-host-information-for-tpm-trusted-attestation"></a>TPM에서 신뢰할 수 있는 증명에 대 한 호스트 정보 추가

TPM 모드의 경우 패브릭 관리자는 각각 HGS 구성에 추가 해야 하는 세 가지 종류의 호스트 정보를 캡처합니다.

- 각 Hyper-v 호스트에 대 한 TPM 식별자 (EKpub)
- 코드 무결성 정책, Hyper-v 호스트에 대해 허용 되는 이진 파일 목록
- 동일한 하드웨어 클래스에서 실행 되는 Hyper-v 호스트 집합을 나타내는 TPM 기준 (부팅 측정)

패브릭 관리자가 정보를 캡처한 후에는 다음 절차에 설명 된 대로 해당 정보를 HGS 구성에 추가 합니다.

1. EKpub 정보를 포함 하는 XML 파일을 가져와 HGS 서버에 복사 합니다. 호스트 마다 하나의 XML 파일이 있습니다. 그런 다음, HGS 서버의 관리자 권한 Windows PowerShell 콘솔에서 아래 명령을 실행 합니다. 각 XML 파일에 대해이 명령을 반복 합니다.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > EKCert (신뢰할 수 없는 인증 키 인증서)와 관련 된 TPM 식별자를 추가할 때 오류가 발생 하는 경우 [신뢰할 수 있는 tpm 루트 인증서가](guarded-fabric-install-trusted-tpm-root-certificates.md) HGS 노드에 추가 되었는지 확인 합니다.
    > 또한 일부 TPM 공급 업체는 EKCerts을 사용 하지 않습니다.
    > 메모장과 같은 편집기에서 XML 파일을 열고 EKCert를 찾지 못했음을 나타내는 오류 메시지를 확인 하 여 EKCert이 누락 되었는지 확인할 수 있습니다.
    > 이 경우 컴퓨터의 TPM이 인증 된 것을 신뢰 하는 경우 `-Force` 플래그를 사용 하 여이 안전 검사를 재정의 하 고 호스트 식별자를 HGS에 추가할 수 있습니다.

2. 패브릭 관리자가 호스트에 대해 만든 코드 무결성 정책을 이진 형식 (@no__t 64,)으로 가져옵니다. HGS 서버에 복사 합니다. 그런 후 다음 명령을 실행 합니다.

    @No__t-0에 대해 적용 되는 호스트의 유형을 설명 하는 CI 정책 이름을 지정 합니다. 컴퓨터의 제조업체/모델과 해당 컴퓨터에서 실행 되는 특수 소프트웨어 구성의 이름을 지정 하는 것이 가장 좋습니다.<br>@No__t-0의 경우 코드 무결성 정책의 경로와 파일 이름을 지정 합니다.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```
    
    > [!NOTE]
    > 서명 된 코드 무결성 정책을 사용 하는 경우 HGS와 동일한 정책에 대 한 서명 되지 않은 복사본을 등록 합니다.
    > 코드 무결성 정책에 대 한 서명은 정책에 대 한 업데이트를 제어 하는 데 사용 되지만 호스트 TPM으로 측정 되지 않으므로 HGS로 증명 된 수 없습니다.

3. 패브릭 관리자가 참조 호스트에서 캡처한 TCGlog 파일을 가져옵니다. HGS 서버에 파일을 복사 합니다. 그런 후 다음 명령을 실행 합니다. 일반적으로 정책 이름은 표시 하는 하드웨어 클래스 (예: "제조업체 모델 수정 버전") 다음에 표시 됩니다.

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

TPM 모드에 대 한 HGS 클러스터 구성 프로세스를 완료 합니다. 패브릭 관리자는 해당 호스트에 대 한 구성을 완료 하기 전에 HGS에서 두 개의 Url을 제공 해야 할 수 있습니다. 이러한 Url을 가져오려면 HGS 서버에서 [HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps)를 실행 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [증명 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

---
title: 신뢰할 수 있는 TPM 증명에 대 한 호스트 정보를 추가 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 3647c9708ad68dec0ac13c85fced2b12150ccf60
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447192"
---
>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

### <a name="add-host-information-for-tpm-trusted-attestation"></a>신뢰할 수 있는 TPM 증명에 대 한 호스트 정보를 추가 합니다.

TPM 모드의 경우 패브릭 관리자는 세 가지 종류의 호스트 정보를 캡처합니다 HGS 구성에 추가 해야 하는 각:

- 각 Hyper-v 호스트에 대 한 TPM 식별자 (EKpub)
- 코드 무결성 정책, Hyper-v 호스트에 대해 허용 된 이진 파일의 허용 목록
- 동일한 클래스의 하드웨어에서 실행 되는 Hyper-v의 집합을 나타내는 TPM 기준 (부팅 측정값이) 호스트

패브릭 후 관리자는 정보를 캡처하는 다음 절차에 설명 된 대로 HGS 구성에 추가 합니다.

1.  HGS 서버에 복사 및는 EKpub 정보를 포함 하는 XML 파일을 가져옵니다. 호스트당 하나의 XML 파일이 됩니다. 그런 다음 HGS 서버에서 관리자 권한 Windows PowerShell 콘솔에서 아래 명령을 실행 합니다. 각 XML 파일에 대해 명령을 반복 합니다.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > 신뢰할 수 없는 인증 키 인증서 (EKCert)에 대 한 TPM 식별자를 추가 하는 경우 오류가 발생 하면 확인 합니다 [TPM 루트 인증서가 추가 되어 신뢰할 수 있는](guarded-fabric-install-trusted-tpm-root-certificates.md) HGS 노드에 있습니다.
    > 또한 일부 TPM 공급 업체는 되도록 EKCerts를 사용 하지 마세요.
    > 메모장과 같은 편집기에서 XML 파일을 열어 EKCert 없습니다 및 찾을 수 없는 EKCert를 나타내는 오류 메시지를 확인 하는 경우를 확인할 수 있습니다.
    > 경우 이며 컴퓨터에서 TPM은 인증에 사용할 수 있습니다를 신뢰 하는 경우는 `-Force` 이 안전 검사를 무시 하 고 호스트 식별자를 HGS에 추가 하는 플래그입니다.

2. 이진 형식 (*.p7b) 호스트에 대 한 패브릭 관리자가 만든 코드 무결성 정책을 가져옵니다. HGS 서버에 복사 합니다. 다음 명령을 실행 합니다.

    에 대 한 `<PolicyName>`를 적용 하는 호스트의 형식을 설명 하는 CI 정책에 대 한 이름을 지정 합니다. 실행 중인 모든 특별 한 소프트웨어가 구성 및 컴퓨터의 메이커/모델 후 이름을 지정 하는 것이 좋습니다.<br>에 대 한 `<Path>`, 경로 및 코드 무결성 정책의 파일 이름을 지정 합니다.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

3. 참조 호스트에서 패브릭 관리자 캡처된 TCGlog 파일을 가져옵니다. HGS 서버에 파일을 복사 합니다. 다음 명령을 실행 합니다. 일반적으로 (예: "제조업체 모델 버전") 나타냅니다 하드웨어 클래스 뒤 정책을 이름을 있습니다.

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

이 TPM 모드용 HGS 클러스터를 구성 하는 과정을 완료 합니다. 패브릭 관리자 호스트에 대 한 구성을 완료 될 수 있으려면 HGS에서 두 개의 Url을 제공 하는 것을 요구할 수 있습니다. 이러한 Url을 HGS 서버를 가져오려면 실행 [Get HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps)합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [증명 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)
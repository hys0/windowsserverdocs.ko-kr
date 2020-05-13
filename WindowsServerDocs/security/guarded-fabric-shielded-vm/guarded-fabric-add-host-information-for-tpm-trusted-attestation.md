---
title: TPM에서 신뢰할 수 있는 증명에 대 한 호스트 정보 추가
ms.prod: windows-server
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: f1c25cc88c577ccb1bc0e8cc690114471e86b6ba
ms.sourcegitcommit: 32f810c5429804c384d788c680afac427976e351
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83203399"
---
# <a name="add-host-information-for-tpm-trusted-attestation"></a>TPM에서 신뢰할 수 있는 증명에 대 한 호스트 정보 추가

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

TPM 모드의 경우 패브릭 관리자는 각각 HGS 구성에 추가 해야 하는 세 가지 종류의 호스트 정보를 캡처합니다.

- 각 Hyper-v 호스트에 대 한 TPM 식별자 (EKpub)
- 코드 무결성 정책, Hyper-v 호스트에 대해 허용 되는 이진 파일 목록
- 동일한 하드웨어 클래스에서 실행 되는 Hyper-v 호스트 집합을 나타내는 TPM 기준 (부팅 측정)

패브릭 관리자는 다음 절차에 설명 된 대로 정보를 캡처하여 HGS 구성에 추가 합니다.

1. EKpub 정보를 포함 하는 XML 파일을 가져와 HGS 서버에 복사 합니다. 호스트 마다 하나의 XML 파일이 있습니다. 그런 다음, HGS 서버의 관리자 권한 Windows PowerShell 콘솔에서 아래 명령을 실행 합니다. 각 XML 파일에 대해이 명령을 반복 합니다.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
       ```

    > [!NOTE]
    > If you encounter an error when adding a TPM identifier regarding an untrusted Endorsement Key Certificate (EKCert), ensure that the [trusted TPM root certificates have been added](guarded-fabric-install-trusted-tpm-root-certificates.md) to the HGS node.
    > Additionally, some TPM vendors do not use EKCerts.
    > You can check if an EKCert is missing by opening the XML file in an editor such as Notepad and checking for an error message indicating no EKCert was found.
    > If this is the case, and you trust that the TPM in your machine is authentic, you can use the `-Force` flag to override this safety check and add the host identifier to HGS.

2. Obtain the code integrity policy that the fabric administrator created for the hosts, in binary format (\*.p7b). Copy it to an HGS server. Then run the following command.

    For `<PolicyName>`, specify a name for the CI polic" that describes the type of host it appl"es to. A be"t practice is to name it after the"make/model of your machine and any special software configuration running on it.<br>For `<Path>`, specify the path and filename of the code integrity policy.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
       ```

    > [!NOTE]
    > If you're using a signed code integrity policy, register an unsigned copy of the same policy with HGS.
    > The signature on code integrity policies is used to control updates to the policy, but is not measured into the host TPM and therefore cannot be attested to by HGS.

3.    Obtain the TCGlog file that the fabric administrator captured from a reference host. Copy the file to an HGS server. Then run the following command. Typically, you will name the policy after the class of hardware it represents (for example, "Manufacturer Model Revision").

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

TPM 모드에 대 한 HGS 클러스터 구성 프로세스를 완료 합니다. 패브릭 관리자는 해당 호스트에 대 한 구성을 완료 하기 전에 HGS에서 두 개의 Url을 제공 해야 할 수 있습니다. 이러한 Url을 가져오려면 HGS 서버에서 [HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps)를 실행 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [증명 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

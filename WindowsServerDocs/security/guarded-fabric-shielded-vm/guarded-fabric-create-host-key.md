---
title: 호스트 키를 만들어 HGS에 추가
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 655ebae66b234d62e5863e2a22e785d5a0028da7
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870544"
---
# <a name="create-a-host-key-and-add-it-to-hgs"></a>호스트 키를 만들어 HGS에 추가

>적용 대상: Windows Server 2019


이 항목에서는 호스트 키 증명 (키 모드)을 사용 하 여 보호 된 호스트가 되도록 Hyper-v 호스트를 준비 하는 방법을 설명 합니다. 호스트 키 쌍을 만들고 (기존 인증서 사용), 키의 공개 절반을 HGS에 추가 합니다.

## <a name="create-a-host-key"></a>호스트 키 만들기

1.  Hyper-v 호스트 컴퓨터에 Windows Server 2019을 설치 합니다.
2.  Hyper-v 및 호스트 보호 Hyper-v 지원 기능을 설치 합니다.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ``` 

3.  호스트 키를 자동으로 생성 하거나 기존 인증서를 선택 합니다. 사용자 지정 인증서를 사용 하는 경우 적어도 2048 비트 RSA 키, 클라이언트 인증 EKU 및 디지털 서명 키 사용이 있어야 합니다.

    ```powershell
    Set-HgsClientHostKey
    ```

    또는 고유한 인증서를 사용 하려는 경우 지문을 지정할 수 있습니다. 
    이는 여러 컴퓨터에서 인증서를 공유 하거나 TPM 또는 HSM에 바인딩된 인증서를 사용 하려는 경우에 유용할 수 있습니다. 다음은 TPM 바인딩된 인증서를 만드는 예제입니다 (개인 키를 도난당 하 고 다른 컴퓨터에서 사용 하 고 TPM 1.2만 필요).

    ```powershell
    $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
    Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
    ```

4.  HGS 서버에 제공할 키의 공개 절반을 가져옵니다. 다음 cmdlet을 사용할 수도 있고, 다른 위치에 저장 된 인증서가 있는 경우 키의 공개 절반을 포함 하는 .cer을 제공할 수도 있습니다. HGS의 공개 키만 저장 하 고 유효성을 검사 합니다. 인증서 정보를 유지 하거나 인증서 체인이 나 만료 날짜의 유효성을 검사 하지 않습니다.

    ```powershell
    Get-HgsClientHostKey -Path "C:\temp\$env:hostname-HostKey.cer"
    ```

5.  .Cer 파일을 HGS 서버에 복사 합니다.

## <a name="add-the-host-key-to-the-attestation-service"></a>증명 서비스에 호스트 키를 추가 합니다.

이 단계는 HGS 서버에서 수행 되며 호스트가 보호 된 Vm을 실행할 수 있도록 합니다. 이름을 호스트 컴퓨터의 FQDN 또는 리소스 식별자로 설정 하는 것이 좋습니다. 그러면 키가 설치 된 호스트를 쉽게 참조할 수 있습니다.

```powershell
Add-HgsAttestationHostKey -Name MyHost01 -Path "C:\temp\MyHost01-HostKey.cer"
``` 

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [호스트가 성공적으로 증명 될 수 있는지 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## <a name="see-also"></a>참조

- [보호 된 호스트 및 보호 된 Vm에 대 한 호스트 보호자 서비스 배포](guarded-fabric-deploying-hgs-overview.md)

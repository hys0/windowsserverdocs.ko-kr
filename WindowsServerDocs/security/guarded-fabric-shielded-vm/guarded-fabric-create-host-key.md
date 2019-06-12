---
title: 호스트 키를 만들고 HGS에 추가
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 0526831fb0648e7f8f6fb1a081180f2e2aa9f09f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447492"
---
# <a name="create-a-host-key-and-add-it-to-hgs"></a>호스트 키를 만들고 HGS에 추가

>적용 대상: Windows Server 2019


이 항목에서는 호스트 키 증명 (키 모드)를 사용 하 여 보호 된 호스트를 Hyper-v 호스트를 준비 하는 방법에 설명 합니다. 에서는 호스트 키 쌍 (만들거나 기존 인증서를 사용 하 여) HGS 키의 공개 키 부분을 추가 합니다.

## <a name="create-a-host-key"></a>호스트 키 만들기

1.  Hyper-v 호스트 컴퓨터에서 Windows Server 2019를 설치 합니다.
2.  Hyper-v 및 호스트 보호 Hyper-v 지원 기능을 설치 합니다.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ``` 

3.  호스트 키를 자동으로 생성 하거나 기존 인증서를 선택 합니다. 사용자 지정 인증서를 사용 하는 경우에 최소한 2048 비트 RSA 키, 클라이언트 인증 EKU 및 디지털 서명 키를 사용이이 있어야 합니다.

    ```powershell
    Set-HgsClientHostKey
    ```

    또는 사용자 고유의 인증서를 사용 하려는 경우 지문을 지정할 수 있습니다. 
    이 여러 컴퓨터에 인증서를 공유 하거나 TPM 또는 HSM에 바인딩된 인증서를 사용 하려는 경우에 유용할 수 있습니다. TPM 바인딩된 인증서 (개인 키를 도난당 하 고 다른 컴퓨터에서 사용할 수 없도록 방지 및 TPM 1.2만 필요)을 만드는 예제는 다음과 같습니다.

    ```powershell
    $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
    Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
    ```

4.  HGS 서버에 제공할 키의 절반 공용을 가져옵니다. 다음 cmdlet을 사용 하거나 입력할 수 있습니다, 다른 곳에 저장 된 인증서를 해야 하는 경우 공용을 포함 하는.cer 키의 절반입니다. 참고는만 저장 하 고 HGS;에 있는 공개 키 유효성 검사 인증서 정보를 유지 하지 않는 것도 인증서 체인 또는 만료 날짜를 확인 했습니다.

    ```powershell
    Get-HgsClientHostKey -Path "C:\temp\$env:hostname-HostKey.cer"
    ```

5.  HGS 서버에.cer 파일을 복사 합니다.

## <a name="add-the-host-key-to-the-attestation-service"></a>호스트 키 증명 서비스에 추가

이 단계는 HGS 서버에서 수행 되 고 호스트가 보호 된 Vm을 실행할 수 있도록 합니다. FQDN 이름을 설정한 나 쉽게 참조할 수 있는 호스트에 키 있도록 호스트 컴퓨터의 리소스 식별자 설치 되는 것이 좋습니다.

```powershell
Add-HgsAttestationHostKey -Name MyHost01 -Path "C:\temp\MyHost01-HostKey.cer"
``` 

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [호스트는 성공적으로 증명할 수 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## <a name="see-also"></a>참조

- [보호 된 호스트 및 차폐 Vm에 대 한 호스트 보호 서비스 배포](guarded-fabric-deploying-hgs-overview.md)

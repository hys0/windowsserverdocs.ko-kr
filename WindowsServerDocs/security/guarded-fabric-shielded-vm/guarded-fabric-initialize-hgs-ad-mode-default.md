---
title: 새 전용 포리스트에서 AD 모드를 사용 하 여 HGS 클러스터 초기화 (기본값)
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4dd10efecf391f7087962e514db7a59135bd93e8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403647"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-a-new-dedicated-forest-default"></a>새 전용 포리스트에서 AD 모드를 사용 하 여 HGS 클러스터 초기화 (기본값)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

>[!IMPORTANT]
>관리자가 신뢰할 수 있는 증명 (AD 모드)은 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode-default.md)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다. 

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)] 
2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  첫 번째 HGS 노드의 관리자 권한 PowerShell 창에서 [HgsServer](https://technet.microsoft.com/library/mt652185.aspx) 를 실행 합니다. 이 cmdlet의 구문은 다양 한 입력을 지원 하지만, 가장 일반적인 두 가지 호출은 다음과 같습니다.

    -   서명 및 암호화 인증서에 PFX 파일을 사용 하는 경우 다음 명령을 실행 합니다.

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
        ```

    -   로컬 인증서 저장소에 설치 된 내보낼 수 없는 인증서를 사용 하는 경우 다음 명령을 실행 합니다. 인증서 지문을 모르는 경우 `Get-ChildItem Cert:\LocalMachine\My`을 실행 하 여 사용 가능한 인증서를 나열할 수 있습니다.

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' --TrustActiveDirectory
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]  

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns-ad.md)
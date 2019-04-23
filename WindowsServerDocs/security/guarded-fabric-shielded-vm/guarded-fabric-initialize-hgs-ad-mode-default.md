---
title: AD 모드를 사용 하 여 새 전용된 포리스트로, (기본값)에서 HGS 클러스터를 초기화 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4ef70ab9ce8150a9a3ed774d6df407da097880e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865674"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-a-new-dedicated-forest-default"></a>AD 모드를 사용 하 여 새 전용된 포리스트로, (기본값)에서 HGS 클러스터를 초기화 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

>[!IMPORTANT]
>관리자-신뢰할 수 있는 증명 (AD 모드)는 Windows Server 2019로 시작 하는 사용 되지 않습니다. TPM 증명 수 없는 환경에 대 한 구성 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode-default.md)합니다. 호스트 키 증명 AD 모드에 유사한 보증을 제공 하며 간단 하 게 설정 합니다. 

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)] 
2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  실행할 [Initialize HgsServer](https://technet.microsoft.com/library/mt652185.aspx) 첫 번째 HGS 노드에서 관리자 권한 PowerShell 창에서. 이 cmdlet의 구문을 많은 다양 한 입력을 지원 하지만 2 가장 일반적인 호출은 다음과 같습니다.

    -   PFX 파일에 서명 및 암호화 인증서를 사용 하는 경우에 다음 명령을 실행 합니다.

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
        ```

    -   로컬 인증서 저장소에 설치 되는 내보낼 수 없는 인증서를 사용 하는 경우 다음 명령을 실행 합니다. 인증서의 지문을 모르는 경우 실행 하 여 사용 가능한 인증서를 나열할 수 있습니다 `Get-ChildItem Cert:\LocalMachine\My`합니다.

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' --TrustActiveDirectory
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]  

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns-ad.md)
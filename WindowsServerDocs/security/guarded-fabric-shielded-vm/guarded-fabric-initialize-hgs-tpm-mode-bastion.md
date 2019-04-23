---
title: 배스 천 포리스트의 TPM 모드를 사용 하 여 HGS 클러스터를 초기화 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ac6407f9f23780dc62ff7d99fe0daf0f81f79f72
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832144"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-an-existing-bastion-forest"></a>TPM 모드를 사용 하 여 기존 배스 천 포리스트의 HGS 클러스터를 초기화 합니다.

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

Active Directory Domain Services가 컴퓨터에 설치 되지만 구성 되지 않은 상태로 유지 해야 합니다.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

계속 하기 전에 호스트 보호 서비스에 대 한 클러스터 개체를 사전 준비 된 하 고 로그온 한 사용자에 부여 했는지 확인 **전면적인** Active Directory에서 VCO 및 CNO 개체입니다.
가상 컴퓨터 개체 이름에 전달 해야 합니다 `-HgsServiceName` 매개 변수 및 클러스터 이름을 `-ClusterName` 매개 변수입니다.

> [!TIP]
> 이중 확인 AD 도메인 컨트롤러가 클러스터 개체를 확인 하려면 계속 하기 전에 모든 Dc에 복제 않았습니다.

PFX 기반 인증서를 사용 하는 경우에 HGS 서버에 다음 명령을 실행 합니다.

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
```

(예: HSM 지원 인증서 및 인증서를 내보낼 수 없는) 로컬 컴퓨터에 설치 된 인증서를 사용 하는 경우 사용 합니다 `-SigningCertificateThumbprint` 및 `-EncryptionCertificateThumbprint` 매개 변수 대신 합니다.

## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[TPM 루트 인증서를 설치 합니다.](guarded-fabric-install-trusted-tpm-root-certificates.md)
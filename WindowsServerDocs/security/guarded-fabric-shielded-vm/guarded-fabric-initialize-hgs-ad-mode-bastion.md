---
title: 요새 포리스트에서 AD 모드를 사용 하 여 HGS 클러스터 초기화
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c69561f7d17bb1d36d90fc66cf4c1a196072fc72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402371"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-an-existing-bastion-forest"></a>기존 요새 포리스트에서 AD 모드를 사용 하 여 HGS 클러스터 초기화

>적용 대상: Windows Server(반기 채널), Windows Server 2016


>[!IMPORTANT]
>관리자가 신뢰할 수 있는 증명 (AD 모드)은 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode-bastion.md)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다. 

Active Directory Domain Services는 컴퓨터에 설치 되지만 구성 되지 않은 상태로 유지 되어야 합니다.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

계속 하기 전에 호스트 보호자 서비스에 대 한 클러스터 개체를 미리 준비 하 고 Active Directory의 VCO 및 CNO 개체에 대 한 **모든 권한을** 로그인 한 사용자에 게 부여 했는지 확인 합니다.
가상 컴퓨터 개체 이름을 `-HgsServiceName` 매개 변수로 전달 하 고 클러스터 이름을 `-ClusterName` 매개 변수에 전달 해야 합니다.

> [!TIP]
> 계속 하기 전에 AD 도메인 컨트롤러를 두 번 확인 하 여 클러스터 개체가 모든 Dc에 복제 되었는지 확인 합니다.

PFX 기반 인증서를 사용 하는 경우 HGS 서버에서 다음 명령을 실행 합니다.

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
```

로컬 컴퓨터에 설치 된 인증서 (예: HSM 지원 인증서 및 내보낼 수 없는 인증서)를 사용 하는 경우 `-SigningCertificateThumbprint` 및 `-EncryptionCertificateThumbprint` 매개 변수를 대신 사용 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns-ad.md)


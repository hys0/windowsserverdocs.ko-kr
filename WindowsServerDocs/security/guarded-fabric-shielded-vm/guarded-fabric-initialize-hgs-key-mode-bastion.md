---
title: 요새 포리스트의 키 모드를 사용 하 여 HGS 클러스터 초기화
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 45f0f587c17e90251da2632f034fe03e2dc1c083
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856656"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>기존 요새 포리스트의 키 모드를 사용 하 여 HGS 클러스터 초기화

> 적용 대상: Windows Server 2019
> 
> [!div class="step-by-step"]
> [«새 포리스트에 HGS 설치](guarded-fabric-install-hgs-in-a-bastion-forest.md)
> [호스트 키 만들기»](guarded-fabric-create-host-key.md)

Active Directory Domain Services는 컴퓨터에 설치 되지만 구성 되지 않은 상태로 유지 되어야 합니다.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

계속 하기 전에 호스트 보호자 서비스에 대 한 클러스터 개체를 미리 준비 하 고 Active Directory의 VCO 및 CNO 개체에 대 한 **모든 권한을** 로그인 한 사용자에 게 부여 했는지 확인 합니다.
가상 컴퓨터 개체 이름을 `-HgsServiceName` 매개 변수에 전달 하 고 클러스터 이름을 `-ClusterName` 매개 변수에 전달 해야 합니다.

> [!TIP]
> 계속 하기 전에 AD 도메인 컨트롤러를 두 번 확인 하 여 클러스터 개체가 모든 Dc에 복제 되었는지 확인 합니다.

PFX 기반 인증서를 사용 하는 경우 HGS 서버에서 다음 명령을 실행 합니다.

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

로컬 컴퓨터에 설치 된 인증서 (예: HSM 지원 인증서 및 내보낼 수 없는 인증서)를 사용 하는 경우 `-SigningCertificateThumbprint` 및 `-EncryptionCertificateThumbprint` 매개 변수를 대신 사용 합니다.

